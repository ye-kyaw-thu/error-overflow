# Image Captioning (Image2Text) Small Experiment Log

Internship ကျောင်းသားများအတွက် အိုက်ဒီယာရဖို့ Flickr30K dataset ကို သုံးပြီး experiment အကြမ်း လုပ်ထားတဲ့ log ဖိုင်ပါ။  

## Dataset Information

https://datasets.activeloop.ai/docs/ml/datasets/flickr30k-dataset/  

## Python Libraries Installation

```
$ python3.10 -m pip install tensorflow
```

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ python3.10 -m pip install opencv-python
Collecting opencv-python
  Downloading opencv_python-4.11.0.86-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (20 kB)
Requirement already satisfied: numpy>=1.21.2 in /home/ye/miniforge3/envs/py3.10/lib/python3.10/site-packages (from opencv-python) (1.24.3)
Downloading opencv_python-4.11.0.86-cp37-abi3-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (63.0 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 63.0/63.0 MB 75.0 MB/s eta 0:00:00
Installing collected packages: opencv-python
Successfully installed opencv-python-4.11.0.86
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ time python3.10 ./image_captioning.py --train --epochs 20 --batch_size 32 --data_dir ./data --model_dir ./model | tee train.log
2025-06-20 21:28:25.733988: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2025-06-20 21:28:25.802322: I tensorflow/tsl/cuda/cudart_stub.cc:28] Could not find cuda drivers on your machine, GPU will not be used.
2025-06-20 21:28:26.184580: I tensorflow/tsl/cuda/cudart_stub.cc:28] Could not find cuda drivers on your machine, GPU will not be used.
2025-06-20 21:28:26.187733: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2025-06-20 21:28:28.989872: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
Traceback (most recent call last):
  File "/home/ye/intern3/img2txt/./image_captioning.py", line 35, in <module>
    from nltk.translate.bleu_score import corpus_bleu
ModuleNotFoundError: No module named 'nltk'

real    0m7.645s
user    0m4.924s
sys     0m1.952s
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ python3.10 -m pip install nltk
Collecting nltk
  Using cached nltk-3.9.1-py3-none-any.whl.metadata (2.9 kB)
Collecting click (from nltk)
  Using cached click-8.2.1-py3-none-any.whl.metadata (2.5 kB)
Requirement already satisfied: joblib in /home/ye/miniforge3/envs/py3.10/lib/python3.10/site-packages (from nltk) (1.4.2)
Requirement already satisfied: regex>=2021.8.3 in /home/ye/miniforge3/envs/py3.10/lib/python3.10/site-packages (from nltk) (2024.11.6)
Requirement already satisfied: tqdm in /home/ye/miniforge3/envs/py3.10/lib/python3.10/site-packages (from nltk) (4.67.1)
Using cached nltk-3.9.1-py3-none-any.whl (1.5 MB)
Using cached click-8.2.1-py3-none-any.whl (102 kB)
Installing collected packages: click, nltk
Successfully installed click-8.2.1 nltk-3.9.1
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

## Some Error Examples

```
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$ time python3.10 ./image_captioning.py --predict ./data/flickr30k_images/Images/1000092795.jpg --model_dir ./model/
...
...
...
    model = saving_utils.model_from_config(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/legacy/saving/saving_utils.py", line 88, in model_from_config
    return serialization.deserialize_keras_object(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/legacy/saving/serialization.py", line 495, in deserialize_keras_object
    deserialized_obj = cls.from_config(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/models/model.py", line 651, in from_config
    return functional_from_config(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/models/functional.py", line 560, in functional_from_config
    process_layer(layer_data)
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/models/functional.py", line 523, in process_layer
    layer = saving_utils.model_from_config(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/legacy/saving/saving_utils.py", line 88, in model_from_config
    return serialization.deserialize_keras_object(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/legacy/saving/serialization.py", line 504, in deserialize_keras_object
    deserialized_obj = cls.from_config(cls_config)
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/layers/rnn/lstm.py", line 692, in from_config
    return cls(**config)
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/layers/rnn/lstm.py", line 499, in __init__
    super().__init__(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/layers/rnn/rnn.py", line 199, in __init__
    super().__init__(**kwargs)
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/keras/src/layers/layer.py", line 291, in __init__
    raise ValueError(
ValueError: Unrecognized keyword arguments passed to LSTM: {'time_major': False}

real    0m6.485s
user    0m6.127s
sys     0m2.224s
```

```
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$ python3.10 -m pip uninstall tensorflow keras -y
Found existing installation: tensorflow 2.19.0
Uninstalling tensorflow-2.19.0:
  Successfully uninstalled tensorflow-2.19.0
Found existing installation: keras 3.10.0
Uninstalling keras-3.10.0:
  Successfully uninstalled keras-3.10.0
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

```
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$ python3.10 -m pip install tensorflow==2.8.0
...
...
...
Collecting pyasn1<0.7.0,>=0.6.1 (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard<2.9,>=2.8->tensorflow==2.8.0)
  Using cached pyasn1-0.6.1-py3-none-any.whl.metadata (8.4 kB)
Collecting oauthlib>=3.0.0 (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard<2.9,>=2.8->tensorflow==2.8.0)
  Downloading oauthlib-3.3.1-py3-none-any.whl.metadata (7.9 kB)
Downloading tensorflow-2.8.0-cp310-cp310-manylinux2010_x86_64.whl (497.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 497.6/497.6 MB 3.1 MB/s eta 0:00:00
Downloading tf_estimator_nightly-2.8.0.dev2021122109-py2.py3-none-any.whl (462 kB)
Downloading keras-2.8.0-py2.py3-none-any.whl (1.4 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.4/1.4 MB 4.1 MB/s eta 0:00:00
Downloading Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Downloading tensorboard-2.8.0-py3-none-any.whl (5.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.8/5.8 MB 16.3 MB/s eta 0:00:00
Downloading google_auth-2.40.3-py2.py3-none-any.whl (216 kB)
Using cached google_auth_oauthlib-0.4.6-py2.py3-none-any.whl (18 kB)
Using cached tensorboard_data_server-0.6.1-py3-none-manylinux2010_x86_64.whl (4.9 MB)
Using cached tensorboard_plugin_wit-1.8.1-py3-none-any.whl (781 kB)
Downloading cachetools-5.5.2-py3-none-any.whl (10 kB)
Downloading pyasn1_modules-0.4.2-py3-none-any.whl (181 kB)
Using cached requests_oauthlib-2.0.0-py2.py3-none-any.whl (24 kB)
Downloading rsa-4.9.1-py3-none-any.whl (34 kB)
Downloading oauthlib-3.3.1-py3-none-any.whl (160 kB)
Using cached pyasn1-0.6.1-py3-none-any.whl (83 kB)
Installing collected packages: tf-estimator-nightly, tensorboard-plugin-wit, keras, tensorboard-data-server, pyasn1, oauthlib, keras-preprocessing, cachetools, rsa, requests-oauthlib, pyasn1-modules, google-auth, google-auth-oauthlib, tensorboard, tensorflow
  Attempting uninstall: tensorboard-data-server
    Found existing installation: tensorboard-data-server 0.7.2
    Uninstalling tensorboard-data-server-0.7.2:
      Successfully uninstalled tensorboard-data-server-0.7.2
  Attempting uninstall: tensorboard
    Found existing installation: tensorboard 2.19.0
    Uninstalling tensorboard-2.19.0:
      Successfully uninstalled tensorboard-2.19.0
Successfully installed cachetools-5.5.2 google-auth-2.40.3 google-auth-oauthlib-0.4.6 keras-2.8.0 keras-preprocessing-1.1.2 oauthlib-3.3.1 pyasn1-0.6.1 pyasn1-modules-0.4.2 requests-oauthlib-2.0.0 rsa-4.9.1 tensorboard-2.8.0 tensorboard-data-server-0.6.1 tensorboard-plugin-wit-1.8.1 tensorflow-2.8.0 tf-estimator-nightly-2.8.0.dev2021122109
```

```
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$ time python3.10 ./image_captioning.py --predict ./data/flickr30k_images/Images/1000092795.jpg --model_dir ./model/
...
...
...
    from tensorflow.keras.applications.vgg16 import VGG16, preprocess_input
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/__init__.py", line 37, in <module>
    from tensorflow.python.tools import module_util as _module_util
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/python/__init__.py", line 37, in <module>
    from tensorflow.python.eager import context
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/python/eager/context.py", line 29, in <module>
    from tensorflow.core.framework import function_pb2
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/core/framework/function_pb2.py", line 16, in <module>
    from tensorflow.core.framework import attr_value_pb2 as tensorflow_dot_core_dot_framework_dot_attr__value__pb2
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/core/framework/attr_value_pb2.py", line 16, in <module>
    from tensorflow.core.framework import tensor_pb2 as tensorflow_dot_core_dot_framework_dot_tensor__pb2
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/core/framework/tensor_pb2.py", line 16, in <module>
    from tensorflow.core.framework import resource_handle_pb2 as tensorflow_dot_core_dot_framework_dot_resource__handle__pb2
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/core/framework/resource_handle_pb2.py", line 16, in <module>
    from tensorflow.core.framework import tensor_shape_pb2 as tensorflow_dot_core_dot_framework_dot_tensor__shape__pb2
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/tensorflow/core/framework/tensor_shape_pb2.py", line 36, in <module>
    _descriptor.FieldDescriptor(
  File "/home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages/google/protobuf/descriptor.py", line 621, in __new__
    _message.Message._CheckCalledFromGeneratedFile()
TypeError: Descriptors cannot be created directly.
If this call came from a _pb2.py file, your generated code is out of date and must be regenerated with protoc >= 3.19.0.
If you cannot immediately regenerate your protos, some other possible workarounds are:
 1. Downgrade the protobuf package to 3.20.x or lower.
 2. Set PROTOCOL_BUFFERS_PYTHON_IMPLEMENTATION=python (but this will use pure-Python parsing and will be much slower).

More information: https://developers.google.com/protocol-buffers/docs/news/2022-05-06#python-updates

real    0m0.853s
user    0m1.139s
sys     0m1.523s
```

```
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$ python3.10 -m pip install protobuf==3.20.*
Collecting protobuf==3.20.*
  Downloading protobuf-3.20.3-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl.metadata (679 bytes)
Downloading protobuf-3.20.3-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (1.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 14.4 MB/s eta 0:00:00
Installing collected packages: protobuf
  Attempting uninstall: protobuf
    Found existing installation: protobuf 5.29.5
    Uninstalling protobuf-5.29.5:
      Successfully uninstalled protobuf-5.29.5
Successfully installed protobuf-3.20.3
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

```
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$ python3.10 -m pip uninstall tensorflow keras -y
Found existing installation: tensorflow 2.8.0
Uninstalling tensorflow-2.8.0:
  Successfully uninstalled tensorflow-2.8.0
Found existing installation: keras 2.8.0
Uninstalling keras-2.8.0:
  Successfully uninstalled keras-2.8.0
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

```
(pytorch_py3.10) ye@lst-hpc3090:~/intern3/img2txt$ python3.10 -m pip install tensorflow==2.9.0 protobuf==3.20.*
...
...
...
Requirement already satisfied: idna<4,>=2.5 in /home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages (from requests<3,>=2.21.0->tensorboard<2.10,>=2.9->tensorflow==2.9.0) (3.10)
Requirement already satisfied: urllib3<3,>=1.21.1 in /home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages (from requests<3,>=2.21.0->tensorboard<2.10,>=2.9->tensorflow==2.9.0) (2.3.0)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages (from requests<3,>=2.21.0->tensorboard<2.10,>=2.9->tensorflow==2.9.0) (2024.12.14)
Requirement already satisfied: MarkupSafe>=2.1.1 in /home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages (from werkzeug>=1.0.1->tensorboard<2.10,>=2.9->tensorflow==2.9.0) (3.0.2)
Requirement already satisfied: pyasn1<0.7.0,>=0.6.1 in /home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages (from pyasn1-modules>=0.2.1->google-auth<3,>=1.6.3->tensorboard<2.10,>=2.9->tensorflow==2.9.0) (0.6.1)
Requirement already satisfied: oauthlib>=3.0.0 in /home/ye/miniforge3/envs/pytorch_py3.10/lib/python3.10/site-packages (from requests-oauthlib>=0.7.0->google-auth-oauthlib<0.5,>=0.4.1->tensorboard<2.10,>=2.9->tensorflow==2.9.0) (3.3.1)
Downloading tensorflow-2.9.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (511.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 511.7/511.7 MB 2.6 MB/s eta 0:00:00
Downloading flatbuffers-1.12-py2.py3-none-any.whl (15 kB)
Using cached gast-0.4.0-py3-none-any.whl (9.8 kB)
Downloading keras-2.9.0-py2.py3-none-any.whl (1.6 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.6/1.6 MB 27.3 MB/s eta 0:00:00
Downloading tensorboard-2.9.0-py3-none-any.whl (5.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 5.8/5.8 MB 3.7 MB/s eta 0:00:00
Downloading tensorflow_estimator-2.9.0-py2.py3-none-any.whl (438 kB)
Installing collected packages: keras, flatbuffers, tensorflow-estimator, gast, tensorboard, tensorflow
  Attempting uninstall: flatbuffers
    Found existing installation: flatbuffers 25.2.10
    Uninstalling flatbuffers-25.2.10:
      Successfully uninstalled flatbuffers-25.2.10
  Attempting uninstall: gast
    Found existing installation: gast 0.6.0
    Uninstalling gast-0.6.0:
      Successfully uninstalled gast-0.6.0
  Attempting uninstall: tensorboard
    Found existing installation: tensorboard 2.8.0
    Uninstalling tensorboard-2.8.0:
      Successfully uninstalled tensorboard-2.8.0
Successfully installed flatbuffers-1.12 gast-0.4.0 keras-2.9.0 tensorboard-2.9.0 tensorflow-2.9.0 tensorflow-estimator-2.9.0
```

```
conda create -n img2txt python=3.8
conda activate img2txt
pip install tensorflow==2.8.0 protobuf==3.20.* numpy==1.21.0 pillow matplotlib opencv-python tqdm nltk pandas
```

## Check with --help

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ python3.8 ./image_captioning.py --help
2025-06-21 09:51:51.016068: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 09:51:51.016114: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
usage: image_captioning.py [-h] [--data_dir DATA_DIR] [--model_dir MODEL_DIR] [--epochs EPOCHS] [--batch_size BATCH_SIZE] [--train]
                           [--evaluate] [--predict PREDICT] [--language {english,myanmar}] [--model_name MODEL_NAME]
                           [--skip_download]

Image Captioning with Flickr30k Dataset

optional arguments:
  -h, --help            show this help message and exit
  --data_dir DATA_DIR   Directory to store dataset (default: ./data)
  --model_dir MODEL_DIR
                        Directory to save/load models (default: ./models)
  --epochs EPOCHS       Number of training epochs (default: 15)
  --batch_size BATCH_SIZE
                        Training batch size (default: 64)
  --train               Train the model
  --evaluate            Evaluate on test set
  --predict PREDICT     Path to single image for prediction
  --language {english,myanmar}
                        Caption language (default: english)
  --model_name MODEL_NAME
                        Model filename (default: best_model.h5)
  --skip_download       Skip dataset download (for prediction mode)
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$
```

## Flickr30K Data Folder

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ tree ./data/ | head -n 30
./data/
├── captions.txt
└── flickr30k_images
    ├── captions.txt
    └── Images
        ├── 1000092795.jpg
        ├── 10002456.jpg
        ├── 1000268201.jpg
        ├── 1000344755.jpg
        ├── 1000366164.jpg
        ├── 1000523639.jpg
        ├── 1000919630.jpg
        ├── 10010052.jpg
        ├── 1001465944.jpg
        ├── 1001545525.jpg
        ├── 1001573224.jpg
        ├── 1001633352.jpg
        ├── 1001773457.jpg
        ├── 1001896054.jpg
        ├── 100197432.jpg
        ├── 100207720.jpg
        ├── 1002674143.jpg
        ├── 1003163366.jpg
        ├── 1003420127.jpg
        ├── 1003428081.jpg
        ├── 100444898.jpg
        ├── 1005216151.jpg
        ├── 100577935.jpg
        ├── 1006452823.jpg
        ├── 100652400.jpg
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ cd data
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data$ head -n 30 ./captions.txt
1000268201_693b08cb0e.jpg#0     A child in a pink dress is climbing up a set of stairs in an entry way .
1000268201_693b08cb0e.jpg#1     A girl going into a wooden building .
1000268201_693b08cb0e.jpg#2     A little girl climbing into a wooden playhouse .
1000268201_693b08cb0e.jpg#3     A little girl climbing the stairs to her playhouse .
1000268201_693b08cb0e.jpg#4     A little girl in a pink dress going into a wooden cabin .
1001773457_577c3a7d70.jpg#0     A black dog and a spotted dog are fighting
1001773457_577c3a7d70.jpg#1     A black dog and a tri-colored dog playing with each other on the road .
1001773457_577c3a7d70.jpg#2     A black dog and a white dog with brown spots are staring at each other in the street .
1001773457_577c3a7d70.jpg#3     Two dogs of different breeds looking at each other on the road .
1001773457_577c3a7d70.jpg#4     Two dogs on pavement moving toward each other .
1002674143_1b742ab4b8.jpg#0     A little girl covered in paint sits in front of a painted rainbow with her hands in a bowl .
1002674143_1b742ab4b8.jpg#1     A little girl is sitting in front of a large painted rainbow .
1002674143_1b742ab4b8.jpg#2     A small girl in the grass plays with fingerpaints in front of a white canvas with a rainbow on it .
1002674143_1b742ab4b8.jpg#3     There is a girl with pigtails sitting in front of a rainbow painting .
1002674143_1b742ab4b8.jpg#4     Young girl with pigtails painting outside in the grass .
1003163366_44323f5815.jpg#0     A man lays on a bench while his dog sits by him .
1003163366_44323f5815.jpg#1     A man lays on the bench to which a white dog is also tied .
1003163366_44323f5815.jpg#2     a man sleeping on a bench outside with a white and black dog sitting next to him .
1003163366_44323f5815.jpg#3     A shirtless man lies on a park bench with his dog .
1003163366_44323f5815.jpg#4     man laying on bench holding leash of dog sitting on ground
1007129816_e794419615.jpg#0     A man in an orange hat starring at something .
1007129816_e794419615.jpg#1     A man wears an orange hat and glasses .
1007129816_e794419615.jpg#2     A man with gauges and glasses is wearing a Blitz hat .
1007129816_e794419615.jpg#3     A man with glasses is wearing a beer can crocheted hat .
1007129816_e794419615.jpg#4     The man with pierced ears is wearing glasses and an orange hat .
1007320043_627395c3d8.jpg#0     A child playing on a rope net .
1007320043_627395c3d8.jpg#1     A little girl climbing on red roping .
1007320043_627395c3d8.jpg#2     A little girl in pink climbs a rope bridge at the park .
1007320043_627395c3d8.jpg#3     A small child grips onto the red ropes at the playground .
1007320043_627395c3d8.jpg#4     The small child climbs on a red ropes on a playground .
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data$
```

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data$ wc captions.txt
  40460  517166 3395237 captions.txt
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data$
```

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data/flickr30k_images$ head -n 30 ./captions.txt
image,caption
1000092795.jpg, Two young guys with shaggy hair look at their hands while hanging out in the yard .
1000092795.jpg," Two young , White males are outside near many bushes ."
1000092795.jpg, Two men in green shirts are standing in a yard .
1000092795.jpg, A man in a blue shirt standing in a garden .
1000092795.jpg, Two friends enjoy time spent together .
10002456.jpg, Several men in hard hats are operating a giant pulley system .
10002456.jpg, Workers look down from up above on a piece of equipment .
10002456.jpg, Two men working on a machine wearing hard hats .
10002456.jpg, Four men on top of a tall structure .
10002456.jpg, Three men on a large rig .
1000268201.jpg, A child in a pink dress is climbing up a set of stairs in an entry way .
1000268201.jpg, A little girl in a pink dress going into a wooden cabin .
1000268201.jpg, A little girl climbing the stairs to her playhouse .
1000268201.jpg, A little girl climbing into a wooden playhouse
1000268201.jpg, A girl going into a wooden building .
1000344755.jpg, Someone in a blue shirt and hat is standing on stair and leaning against a window .
1000344755.jpg, A man in a blue shirt is standing on a ladder cleaning a window .
1000344755.jpg, A man on a ladder cleans the window of a tall building .
1000344755.jpg, man in blue shirt and jeans on ladder cleaning windows
1000344755.jpg, a man on a ladder cleans a window
1000366164.jpg," Two men , one in a gray shirt , one in a black shirt , standing near a stove ."
1000366164.jpg, Two guy cooking and joking around with the camera .
1000366164.jpg, Two men in a kitchen cooking food on a stove .
1000366164.jpg, Two men are at the stove preparing food .
1000366164.jpg, Two men are cooking a meal .
1000523639.jpg, Two people in the photo are playing the guitar and the other is poking at him .
1000523639.jpg, A man in green holds a guitar while the other man observes his shirt .
1000523639.jpg, A man is fixing the guitar players costume .
1000523639.jpg, a guy stitching up another man 's coat .
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data/flickr30k_images$
```

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data/flickr30k_images$ wc captions.txt
  158916  2286682 12901863 captions.txt
(py3.10) ye@lst-hpc3090:~/intern3/img2txt/data/flickr30k_images$
```

## Training After Data Downloaded

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ time python3.10 ./image_captioning.py --train --epochs 20 --batch_size 32 --data_dir ./data --model_dir ./model | tee train.log
2025-06-20 22:49:05.945001: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2025-06-20 22:49:05.946342: I tensorflow/tsl/cuda/cudart_stub.cc:28] Could not find cuda drivers on your machine, GPU will not be used.
2025-06-20 22:49:05.974639: I tensorflow/tsl/cuda/cudart_stub.cc:28] Could not find cuda drivers on your machine, GPU will not be used.
2025-06-20 22:49:05.974953: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2025-06-20 22:49:06.467650: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
2025-06-20 22:49:07.434598: I tensorflow/compiler/xla/stream_executor/cuda/cuda_gpu_executor.cc:995] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero. See more at https://github.com/torvalds/linux/blob/v6.0/Documentation/ABI/testing/sysfs-bus-pci#L344-L355
2025-06-20 22:49:07.454544: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1960] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
Dataset download complete.
Extracting features with VGG16...
Extracting features: 100%|█████████████████████████████████████████████████████████████████████| 31783/31783 [1:03:00<00:00,  8.41it/s]
Saved features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Training model for 20 epochs...
227/227 [==============================] - 147s 636ms/step - loss: 5.1919
227/227 [==============================] - 145s 636ms/step - loss: 3.8921
227/227 [==============================] - 145s 637ms/step - loss: 3.4364
227/227 [==============================] - 144s 634ms/step - loss: 3.1565
227/227 [==============================] - 144s 633ms/step - loss: 2.9525
227/227 [==============================] - 144s 635ms/step - loss: 2.7984
227/227 [==============================] - 144s 636ms/step - loss: 2.6865
227/227 [==============================] - 144s 635ms/step - loss: 2.5919
227/227 [==============================] - 144s 635ms/step - loss: 2.5120
227/227 [==============================] - 145s 636ms/step - loss: 2.4494
227/227 [==============================] - 144s 634ms/step - loss: 2.3919
227/227 [==============================] - 144s 634ms/step - loss: 2.3355
227/227 [==============================] - 144s 632ms/step - loss: 2.2853
227/227 [==============================] - 144s 633ms/step - loss: 2.2365
227/227 [==============================] - 144s 634ms/step - loss: 2.1922
227/227 [==============================] - 119s 525ms/step - loss: 2.1531
227/227 [==============================] - 122s 535ms/step - loss: 2.1146
227/227 [==============================] - 133s 588ms/step - loss: 2.0813
227/227 [==============================] - 145s 637ms/step - loss: 2.0531
227/227 [==============================] - 144s 633ms/step - loss: 2.0237
/home/ye/miniforge3/envs/py3.10/lib/python3.10/site-packages/keras/src/engine/training.py:3000: UserWarning: You are saving your model as an HDF5 file via `model.save()`. This file format is considered legacy. We recommend using instead the native Keras format, e.g. `model.save('my_model.keras')`.
  saving_api.save_model(
Model saved to ./model/best_model.h5

real    110m17.002s
user    1019m2.364s
sys     21m11.316s
```

## Check Folders  

```
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ ls
data  download_dataset.sh  image2text  image_captioning.py  inspect_flickr30k.py  model  tmp.log  train.log
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$ ls ./model
best_model.h5  features.pkl
(py3.10) ye@lst-hpc3090:~/intern3/img2txt$
```

## Train Again Under New Environment

I updated the code for skipping downloading and also feature extraction steps.  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 ./image_captioning.py --train --epochs 20 --batch_size 32 --data data --model_dir ./model | tee train_with_py3.8.log
2025-06-21 10:32:58.459275: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 10:32:58.459295: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 10:32:59.986433: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 10:32:59.986580: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 10:32:59.986613: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 10:32:59.986639: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 10:32:59.986662: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 10:33:00.006861: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 10:33:00.006927: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 10:33:00.006941: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 10:33:00.007179: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in data/flickr30k_images/Images
Sample image paths: ['data/flickr30k_images/Images/435802277.jpg', 'data/flickr30k_images/Images/216594524.jpg', 'data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Training model for 20 epochs...
227/227 [==============================] - 156s 680ms/step - loss: 5.2065
227/227 [==============================] - 153s 673ms/step - loss: 3.9045
227/227 [==============================] - 151s 666ms/step - loss: 3.4503
227/227 [==============================] - 150s 661ms/step - loss: 3.1759
227/227 [==============================] - 150s 661ms/step - loss: 2.9764
227/227 [==============================] - 150s 660ms/step - loss: 2.8267
227/227 [==============================] - 150s 658ms/step - loss: 2.7108
227/227 [==============================] - 150s 659ms/step - loss: 2.6118
227/227 [==============================] - 135s 593ms/step - loss: 2.5304
227/227 [==============================] - 121s 532ms/step - loss: 2.4592
227/227 [==============================] - 127s 557ms/step - loss: 2.3985
227/227 [==============================] - 148s 653ms/step - loss: 2.3455
227/227 [==============================] - 150s 660ms/step - loss: 2.2951
227/227 [==============================] - 150s 661ms/step - loss: 2.2475
227/227 [==============================] - 149s 656ms/step - loss: 2.2043
227/227 [==============================] - 147s 649ms/step - loss: 2.1671
227/227 [==============================] - 149s 657ms/step - loss: 2.1296
227/227 [==============================] - 149s 655ms/step - loss: 2.0942
227/227 [==============================] - 148s 651ms/step - loss: 2.0646
227/227 [==============================] - 147s 649ms/step - loss: 2.0362
Model saved to ./model/best_model.h5
Tokenizer saved to ./model/tokenizer.pkl

real    48m56.106s
user    611m50.061s
sys     31m25.596s
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$

```

## Prediction with Input Image  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 image_captioning.py --predict ./data/flickr30k_images/Images/1000092795.jpg --model_dir ./model
2025-06-21 11:29:10.340867: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:29:10.340889: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
Skipping dataset download for prediction mode
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
2025-06-21 11:29:11.931562: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 11:29:11.931692: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:29:11.931720: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:29:11.931745: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:29:11.931771: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:29:11.952716: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:29:11.952781: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:29:11.952790: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 11:29:11.953018: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Model loaded from ./model/best_model.h5
Extracting features: 100%|███████████████████████████████████████████████████████████████████████████████| 1/1 [00:00<00:00,  2.84it/s]

Predicted Caption: startseq two young girls are walking on a bench in the park and eat cones on a bench and a tree and a red blanket in the background are sitting on a bench in the background one has a

real    0m7.279s
user    0m8.989s
sys     0m4.564s

```

Check Reference Captions:  

```
image,caption
1000092795.jpg, Two young guys with shaggy hair look at their hands while hanging out in the yard .
1000092795.jpg," Two young , White males are outside near many bushes ."
1000092795.jpg, Two men in green shirts are standing in a yard .
1000092795.jpg, A man in a blue shirt standing in a garden .
1000092795.jpg, Two friends enjoy time spent together .

```

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 image_captioning.py --predict ./data/flickr30k_images/Images/1000268201.jpg --model_dir ./model
2025-06-21 11:37:53.153580: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:37:53.153602: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
Skipping dataset download for prediction mode
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
2025-06-21 11:37:54.765328: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 11:37:54.765505: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:37:54.765551: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:37:54.765582: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:37:54.765650: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:37:54.786989: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:37:54.787068: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:37:54.787081: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 11:37:54.787371: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Model loaded from ./model/best_model.h5
Extracting features: 100%|███████████████████████████████████████████████████████████████████████████████| 1/1 [00:00<00:00,  3.27it/s]

Predicted Caption: startseq older woman wearing a red shirt and red pants is sitting on a red bench in front of a wooden cabin set of a wooden cabin with a trashcan on a porch door nearby a trashcan to the

real    0m7.105s
user    0m9.036s
sys     0m5.115s

```

Check Reference Captions:  

```
1000268201.jpg, A child in a pink dress is climbing up a set of stairs in an entry way .
1000268201.jpg, A little girl in a pink dress going into a wooden cabin .
1000268201.jpg, A little girl climbing the stairs to her playhouse .
1000268201.jpg, A little girl climbing into a wooden playhouse
1000268201.jpg, A girl going into a wooden building .
```

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 image_captioning.py --predict ./data/flickr30k_images/Images/1000344755.jpg --model_dir ./model
2025-06-21 11:40:32.602367: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:40:32.602386: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
Skipping dataset download for prediction mode
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
2025-06-21 11:40:34.152732: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 11:40:34.152928: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:40:34.152971: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:40:34.153004: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:40:34.153043: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:40:34.179367: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:40:34.179440: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 11:40:34.179452: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 11:40:34.179711: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Model loaded from ./model/best_model.h5
Extracting features: 100%|███████████████████████████████████████████████████████████████████████████████| 1/1 [00:00<00:00,  3.42it/s]

Predicted Caption: startseq construction art beam is standing on a brick wall with a blue brick building behind him on it i upper below it is hanging off him on the sidewalk beside the ocean below it is putting his head

real    0m6.940s
user    0m8.902s
sys     0m5.106s

```

Check Reference Captions:  

```
1000344755.jpg, Someone in a blue shirt and hat is standing on stair and leaning against a window .
1000344755.jpg, A man in a blue shirt is standing on a ladder cleaning a window .
1000344755.jpg, A man on a ladder cleans the window of a tall building .
1000344755.jpg, man in blue shirt and jeans on ladder cleaning windows
1000344755.jpg, a man on a ladder cleans a window
```

## Code Updating  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ wc ./image_captioning.py
  645  2074 24961 ./image_captioning.py
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$
```

## Current Version (12:57, 21 June 2025)  

```python
#!/usr/bin/env python
# coding: utf-8

"""
Improved Flickr30k Image Captioning System

Features:
- Command-line interface with argparse
- Support for both dataset evaluation and single image prediction
- Configurable paths for data and model saving
- Modular design for easier maintenance
- Prepared for multilingual support (including Myanmar)
- Additional evaluation metrics (BLEU and chrF++)
- Enhanced hyperparameter configuration
"""

import os
import pickle
import argparse
import numpy as np
import pandas as pd
from tqdm import tqdm
import matplotlib.pyplot as plt
from PIL import Image
import cv2

# TensorFlow/Keras imports
from tensorflow.keras.applications.vgg16 import VGG16, preprocess_input
from tensorflow.keras.preprocessing.image import load_img, img_to_array
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Model, load_model
from tensorflow.keras.utils import to_categorical, plot_model
from tensorflow.keras.layers import Input, Dense, LSTM, Embedding, Dropout, add
from tensorflow.keras.optimizers import Adam

# Evaluation metrics
from nltk.translate.bleu_score import corpus_bleu
import nltk
from nltk.translate.chrf_score import corpus_chrf

def download_dataset(data_dir):
    """Download and extract Flickr30k dataset with captions"""
    if not os.path.exists(data_dir):
        os.makedirs(data_dir)
    
    # 1. Download images
    image_dir = os.path.join(data_dir, 'flickr30k_images')
    if not os.path.exists(image_dir):
        print("Downloading Flickr30k images...")
        try:
            # Download parts
            for part in ['00', '01', '02']:
                url = f"https://github.com/awsaf49/flickr-dataset/releases/download/v1.0/flickr30k_part{part}"
                if os.system(f'wget "{url}" -q --show-progress') != 0:
                    raise Exception(f"Failed to download part {part}")
            
            # Combine and extract
            if os.system('cat flickr30k_part00 flickr30k_part01 flickr30k_part02 > flickr30k.zip') != 0:
                raise Exception("Failed to combine parts")
                
            # Create target directory
            os.makedirs(image_dir, exist_ok=True)
            
            # Extract to the correct location
            if os.system(f'unzip -q flickr30k.zip -d {image_dir}') != 0:
                raise Exception("Failed to extract zip")
            
            # Cleanup
            os.system('rm flickr30k_part00 flickr30k_part01 flickr30k_part02 flickr30k.zip')
            
            # Verify extraction
            if not os.listdir(image_dir):
                raise Exception("Extracted directory is empty")
            
        except Exception as e:
            print(f"Download failed: {str(e)}")
            if os.path.exists(image_dir):
                os.rmdir(image_dir)  # Clean up empty directory
            return False
    
    # 2. Download captions (if needed)
    captions_path = os.path.join(data_dir, "captions.txt")
    if not os.path.exists(captions_path):
        print("Downloading captions...")
        try:
            if os.system(f'wget https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_text.zip -O {data_dir}/captions.zip -q --show-progress') != 0:
                raise Exception("Failed to download captions")
            if os.system(f'unzip -j {data_dir}/captions.zip "Flickr8k.token.txt" -d {data_dir}') != 0:
                raise Exception("Failed to extract captions")
            os.system(f'mv {data_dir}/Flickr8k.token.txt {captions_path}')
            os.system(f'rm {data_dir}/captions.zip')
            
            # Verify captions file
            if not os.path.exists(captions_path):
                raise Exception("Captions file not created")
                
        except Exception as e:
            print(f"Caption download failed: {str(e)}")
            return False
    
    print("Dataset download complete.")
    return True

def load_and_preprocess_captions(caption_path, clean_func=None):
    """Load and preprocess captions from file"""
    mapping = {}
    
    with open(caption_path, 'r', encoding='utf-8') as f:
        # Handle both CSV and Flickr8k formats
        first_line = f.readline()
        f.seek(0)  # Rewind to start
        
        if first_line.startswith('image,caption'):  # Flickr30k format
            next(f)  # Skip header
            for line in f:
                tokens = line.strip().split(',')
                if len(line) < 2:
                    continue
                # MODIFIED: Remove everything after last underscore
                image_id = tokens[0].split('.')[0].rsplit('_', 1)[0]
                image_desc = tokens[1].strip()
                
                if clean_func:
                    image_desc = clean_func(image_desc)
                
                if image_id not in mapping:
                    mapping[image_id] = []
                mapping[image_id].append(image_desc)
        else:  # Flickr8k format
            for line in f:
                if not line.strip():
                    continue
                parts = line.strip().split('\t')
                if len(parts) < 2:
                    continue
                # MODIFIED: Remove everything after last underscore
                image_id = parts[0].split('.')[0].split('#')[0].rsplit('_', 1)[0]
                image_desc = parts[1].strip()
                
                if clean_func:
                    image_desc = clean_func(image_desc)
                
                if image_id not in mapping:
                    mapping[image_id] = []
                mapping[image_id].append(image_desc)
    
    return mapping

def clean_english_text(text):
    """Basic English text cleaning"""
    text = text.lower()
    # Add more cleaning as needed
    return text

def clean_myanmar_text(text):
    """Basic Myanmar text cleaning"""
    # Add Myanmar-specific cleaning here
    return text

def extract_image_features(image_paths, model, feature_size=4096):
    """Extract features from images using pre-trained model"""
    features = {}
    
    for img_path in tqdm(image_paths, desc="Extracting features"):
        try:
            img = load_img(img_path, target_size=(224, 224))
            img = img_to_array(img)
            img = img.reshape((1, img.shape[0], img.shape[1], img.shape[2]))
            img = preprocess_input(img)
            
            feature = model.predict(img, verbose=0).reshape(feature_size,)
            image_id = os.path.splitext(os.path.basename(img_path))[0]
            features[image_id] = feature
        except Exception as e:
            print(f"Error processing {img_path}: {str(e)}")
    
    return features

def create_tokenizer(captions):
    """Create tokenizer from captions"""
    all_captions = []
    for key in captions:
        for caption in captions[key]:
            all_captions.append(caption)
    
    tokenizer = Tokenizer()
    tokenizer.fit_on_texts(all_captions)
    
    vocab_size = len(tokenizer.word_index) + 1
    max_length = max(len(caption.split()) for caption in all_captions)
    
    return tokenizer, vocab_size, max_length

def data_generator(data_keys, features, mapping, tokenizer, max_length, vocab_size, batch_size):
    """Generator for training data"""
    X1, X2, y = [], [], []
    n = 0
    
    # Filter keys to only those with both features and captions
    valid_keys = [k for k in data_keys if k in features and k in mapping]
    
    while True:
        for key in valid_keys:
            n += 1
            captions = mapping[key]
            
            for caption in captions:
                seq = tokenizer.texts_to_sequences([caption])[0]
                
                for i in range(1, len(seq)):
                    in_seq, out_seq = seq[:i], seq[i]
                    in_seq = pad_sequences([in_seq], maxlen=max_length)[0]
                    out_seq = to_categorical([out_seq], num_classes=vocab_size)[0]
                    
                    X1.append(features[key])
                    X2.append(in_seq)
                    y.append(out_seq)
            
            if n == batch_size:
                X1 = np.array(X1)
                X2 = np.array(X2)
                y = np.array(y)
                yield [X1, X2], y
                X1, X2, y = [], [], []
                n = 0
def build_model(vocab_size, max_length, feature_size=4096, lstm_units=256, dropout_rate=0.4, learning_rate=0.001):
    """Build the image captioning model with configurable hyperparameters"""
    # Image feature layers
    inputs1 = Input(shape=(feature_size,))
    fe1 = Dropout(dropout_rate)(inputs1)
    fe2 = Dense(lstm_units, activation='relu')(fe1)
    
    # Sequence feature layers
    inputs2 = Input(shape=(max_length,))
    se1 = Embedding(vocab_size, lstm_units, mask_zero=True)(inputs2)
    se2 = Dropout(dropout_rate)(se1)
    se3 = LSTM(lstm_units)(se2)
    
    # Decoder model
    decoder1 = add([fe2, se3])
    decoder2 = Dense(lstm_units, activation='relu')(decoder1)
    outputs = Dense(vocab_size, activation='softmax')(decoder2)
    
    model = Model(inputs=[inputs1, inputs2], outputs=outputs)
    optimizer = Adam(learning_rate=learning_rate)
    model.compile(loss='categorical_crossentropy', optimizer=optimizer)
    
    return model

def idx_to_word(integer, tokenizer):
    """Convert index to word using tokenizer"""
    for word, index in tokenizer.word_index.items():
        if index == integer:
            return word
    return None

def predict_caption(model, image, tokenizer, max_length):
    """Generate caption for an image"""
    in_text = 'startseq'
    
    for _ in range(max_length):
        seq = tokenizer.texts_to_sequences([in_text])[0]
        seq = pad_sequences([seq], maxlen=max_length)
        yhat = model.predict([image, seq], verbose=0)
        yhat = np.argmax(yhat)
        
        word = idx_to_word(yhat, tokenizer)
        if word is None:
            break
            
        in_text += ' ' + word
        if word == 'endseq':
            break
    
    return in_text

def evaluate_model(model, test_keys, features, mapping, tokenizer, max_length):
    """Evaluate model on test set and calculate BLEU and chrF++ scores"""
    actual, predicted = [], []
    results = []
    
    for key in tqdm(test_keys, desc="Evaluating"):
        captions = mapping[key]
        y_pred = predict_caption(model, features[key].reshape(1, -1), tokenizer, max_length)
        
        # Store results
        results.append({
            'image_id': key,
            'actual_captions': captions,
            'predicted_caption': y_pred
        })
        
        # Prepare for BLEU and chrF++ scores
        actual_captions = [caption.split() for caption in captions]
        y_pred = y_pred.split()
        
        actual.append(actual_captions)
        predicted.append(y_pred)
    
    # Calculate BLEU scores
    bleu1 = corpus_bleu(actual, predicted, weights=(1.0, 0, 0, 0))
    bleu2 = corpus_bleu(actual, predicted, weights=(0.5, 0.5, 0, 0))
    bleu3 = corpus_bleu(actual, predicted, weights=(0.33, 0.33, 0.33, 0))
    bleu4 = corpus_bleu(actual, predicted, weights=(0.25, 0.25, 0.25, 0.25))
    
    # Calculate chrF++ score
    # Convert to string format for chrF++
    actual_str = [' '.join(ref[0]) for ref in actual]  # Using first reference
    predicted_str = [' '.join(pred) for pred in predicted]
    chrfpp_score = corpus_chrf(actual_str, predicted_str, beta=2.0)
    
    return results, bleu1, bleu2, bleu3, bleu4, chrfpp_score

def save_results(results, metrics, output_dir):
    """Save evaluation results in both pickle and text formats"""
    # Save pickle file
    pickle_path = os.path.join(output_dir, 'evaluation_results.pkl')
    with open(pickle_path, 'wb') as f:
        pickle.dump({
            'results': results,
            'metrics': metrics
        }, f)
    
    # Save text file
    txt_path = os.path.join(output_dir, 'evaluation_results.txt')
    with open(txt_path, 'w', encoding='utf-8') as f:
        f.write("Evaluation Metrics:\n")
        f.write(f"BLEU-1: {metrics['bleu1']:.4f}\n")
        f.write(f"BLEU-2: {metrics['bleu2']:.4f}\n")
        f.write(f"BLEU-3: {metrics['bleu3']:.4f}\n")
        f.write(f"BLEU-4: {metrics['bleu4']:.4f}\n")
        f.write(f"chrF++: {metrics['chrfpp']:.4f}\n\n")
        
        f.write("Sample Results:\n")
        for i, result in enumerate(results[:100]):  # Save first 100 results for readability
            f.write(f"\nImage ID: {result['image_id']}\n")
            f.write("Actual Captions:\n")
            for j, caption in enumerate(result['actual_captions'], 1):
                f.write(f"{j}. {caption}\n")
            f.write(f"Predicted Caption: {result['predicted_caption']}\n")
    
    print(f"Evaluation results saved to {pickle_path} (binary) and {txt_path} (text)")

def visualize_results(image_path, actual_captions, predicted_caption):
    """Visualize image with actual and predicted captions"""
    image = Image.open(image_path)
    plt.imshow(image)
    plt.axis('off')
    
    print("\nActual Captions:")
    for i, caption in enumerate(actual_captions, 1):
        print(f"{i}. {caption}")
    
    print(f"\nPredicted Caption: {predicted_caption}")
    plt.show()

def find_caption_file(data_dir):
    """Find the caption file in directory"""
    possible_names = [
        'captions.txt',
        'results.csv', 
        'Flickr8k.token.txt',
        'annotations/captions.txt'
    ]
    
    for name in possible_names:
        path = os.path.join(data_dir, name)
        if os.path.exists(path):
            return path
    return None

def main():
    parser = argparse.ArgumentParser(description='Image Captioning with Flickr30k Dataset')
    parser.add_argument('--data_dir', type=str, default='./data', 
                       help='Directory to store dataset (default: ./data)')
    parser.add_argument('--model_dir', type=str, default='./models', 
                       help='Directory to save/load models (default: ./models)')
    parser.add_argument('--epochs', type=int, default=15, 
                       help='Number of training epochs (default: 15)')
    parser.add_argument('--batch_size', type=int, default=64, 
                       help='Training batch size (default: 64)')
    parser.add_argument('--train', action='store_true', 
                       help='Train the model')
    parser.add_argument('--evaluate', action='store_true', 
                       help='Evaluate on test set')
    parser.add_argument('--predict', type=str, 
                       help='Path to single image for prediction')
    parser.add_argument('--language', type=str, default='english', 
                       choices=['english', 'myanmar'], help='Caption language (default: english)')
    parser.add_argument('--model_name', type=str, default='best_model.h5', 
                       help='Model filename (default: best_model.h5)')
    parser.add_argument('--skip_download', action='store_true',
                      help='Skip dataset download (for prediction mode)')
    parser.add_argument('--skip_feature_extraction', action='store_true',
                      help='Skip feature extraction if features file exists')
    
    parser.add_argument('--lstm_units', type=int, default=256,
                       help='Number of units in LSTM layer (default: 256)')
    parser.add_argument('--dropout_rate', type=float, default=0.4,
                       help='Dropout rate (default: 0.4)')
    parser.add_argument('--learning_rate', type=float, default=0.001,
                       help='Learning rate (default: 0.001)')
    parser.add_argument('--early_stopping', type=int, default=None,
                       help='Patience for early stopping (default: None)')
    parser.add_argument('--feature_size', type=int, default=4096,
                       help='Size of image features (default: 4096)')

    args = parser.parse_args()
    
    # Create necessary directories
    os.makedirs(args.model_dir, exist_ok=True)
    model_path = os.path.join(args.model_dir, args.model_name)
    
    # Download dataset if needed (skip if in predict mode or --skip_download specified)
    if not (args.skip_download or args.predict):
        if not download_dataset(args.data_dir):
            return
    elif args.predict:
        print("Skipping dataset download for prediction mode")
    
    # Set paths
    image_dir = os.path.join(args.data_dir, 'flickr30k_images', 'Images')
    
    # Verify image directory exists
    if not os.path.exists(image_dir):
        print(f"Error: Image directory not found at {image_dir}")
        print("Please ensure the dataset downloaded correctly")
        return
    
    # Find caption file
    caption_path = find_caption_file(args.data_dir)
    if caption_path is None:
        print("Error: Could not find captions file in data directory")
        return

    # Load and preprocess captions
    clean_func = clean_english_text if args.language == 'english' else clean_myanmar_text
    mapping = load_and_preprocess_captions(caption_path, clean_func)
    
    # Get image paths
    image_paths = [os.path.join(image_dir, f) for f in os.listdir(image_dir) 
                  if f.lower().endswith(('.jpg', '.jpeg', '.png'))]

    # Load or extract image features
    features_path = os.path.join(args.model_dir, 'features.pkl')
    
    # Skip feature extraction if --skip_feature_extraction is set and features exist
    if args.skip_feature_extraction and os.path.exists(features_path):
        print("--skip_feature_extraction flag set and features file exists, skipping feature extraction")
        with open(features_path, 'rb') as f:
            features = pickle.load(f)
        print(f"Loaded features for {len(features)} images")
    else:
        if os.path.exists(features_path):
            try:
                print("Loading precomputed features...")
                with open(features_path, 'rb') as f:
                    features = pickle.load(f)
                print(f"Loaded features for {len(features)} images")
            except Exception as e:
                print(f"Error loading features: {str(e)}")
                print("Will re-extract features...")
                features = {}
        else:
            features = {}

        if not features:
            print("Extracting features with VGG16...")
            vgg_model = VGG16(weights='imagenet')
            vgg_model = Model(inputs=vgg_model.inputs, outputs=vgg_model.layers[-2].output)
            
            # Only extract features for images we don't already have
            existing_ids = set(features.keys())
            new_image_paths = [p for p in image_paths 
                             if os.path.splitext(os.path.basename(p))[0] not in existing_ids]
            
            if new_image_paths:
                new_features = extract_image_features(new_image_paths, vgg_model)
                features.update(new_features)
                print(f"Added features for {len(new_features)} new images")
            
            # Save features if we have any
            if features:
                with open(features_path, 'wb') as f:
                    pickle.dump(features, f)
                print(f"Saved features for {len(features)} images total")
            else:
                print("Error: No features extracted")
                return

    print(f"Found {len(image_paths)} images in {image_dir}")
    print("Sample image paths:", image_paths[:3])

    # Find common keys
    common_keys = set(features.keys()) & set(mapping.keys())
    print(f"Common images with both features and captions: {len(common_keys)}")

    if not common_keys:
        print("Error: No matching images between features and captions!")
        print("Sample feature keys:", list(features.keys())[:5])
        print("Sample mapping keys:", list(mapping.keys())[:5])
        return

    # Filter mappings to only include images we have features for
    mapping = {k: v for k, v in mapping.items() if k in features}

    # Create tokenizer
    tokenizer, vocab_size, max_length = create_tokenizer(mapping)
    
    # Split data
    image_ids = list(mapping.keys())
    split = int(len(image_ids) * 0.9)  # 90% train, 10% test
    train_keys = image_ids[:split]
    test_keys = image_ids[split:]
        
    if args.train:
        # Build and train model
        model = build_model(
            vocab_size, 
            max_length,
            feature_size=args.feature_size,
            lstm_units=args.lstm_units,
            dropout_rate=args.dropout_rate,
            learning_rate=args.learning_rate
        )
        steps = len(train_keys) // args.batch_size
        
        print(f"Training model for {args.epochs} epochs with:")
        print(f"- LSTM units: {args.lstm_units}")
        print(f"- Dropout rate: {args.dropout_rate}")
        print(f"- Learning rate: {args.learning_rate}")
        print(f"- Batch size: {args.batch_size}")

        for epoch in range(args.epochs):
            generator = data_generator(
                train_keys, features, mapping, tokenizer, 
                max_length, vocab_size, args.batch_size
            )
            model.fit(
                generator, 
                steps_per_epoch=steps, 
                epochs=1, 
                verbose=1
            )
        
        # Save model
        model.save(model_path)
        print(f"Model saved to {model_path}")
    
        # Save tokenizer and max_length for prediction
        tokenizer_path = os.path.join(args.model_dir, 'tokenizer.pkl')
        with open(tokenizer_path, 'wb') as f:
            pickle.dump((tokenizer, max_length), f)
        print(f"Tokenizer saved to {tokenizer_path}")

    # Load model for evaluation/prediction
    if args.evaluate or args.predict:
        if os.path.exists(model_path):
            model = load_model(model_path)
            print(f"Model loaded from {model_path}")
        else:
            print("Error: Model not found. Please train first or check path.")
            return
    
    if args.evaluate:
        # Evaluate on test set with new metrics
        results, bleu1, bleu2, bleu3, bleu4, chrfpp = evaluate_model(
            model, test_keys, features, mapping, tokenizer, max_length
        )
        
        print("\nEvaluation Metrics:")
        print(f"BLEU-1: {bleu1:.4f}")
        print(f"BLEU-2: {bleu2:.4f}")
        print(f"BLEU-3: {bleu3:.4f}")
        print(f"BLEU-4: {bleu4:.4f}")
        print(f"chrF++: {chrfpp:.4f}")
        
        # Save results with new format
        metrics = {
            'bleu1': bleu1,
            'bleu2': bleu2,
            'bleu3': bleu3,
            'bleu4': bleu4,
            'chrfpp': chrfpp
        }
        save_results(results, metrics, args.model_dir)
    
    if args.predict:
        # Predict for single image
        if not os.path.exists(args.predict):
            print(f"Error: Image file not found at {args.predict}")
            return
    
        # Verify image directory exists
        if not os.path.exists(image_dir):
            print(f"Error: Image directory not found at {image_dir}")
            print("Please ensure the dataset downloaded correctly")
            return
    
        # Load tokenizer and max_length
        tokenizer_path = os.path.join(args.model_dir, 'tokenizer.pkl')
        if os.path.exists(tokenizer_path):
            with open(tokenizer_path, 'rb') as f:
                tokenizer, max_length = pickle.load(f)
        else:
            print("Error: Tokenizer not found. Please train first.")
            return
        
        # Extract features for the image
        vgg_model = VGG16(weights='imagenet')
        vgg_model = Model(inputs=vgg_model.inputs, outputs=vgg_model.layers[-2].output)
    
        # Skip image directory check for prediction
        try:
            img_features = extract_image_features([args.predict], vgg_model)
        except Exception as e:
            print(f"Error processing image: {str(e)}")
            return
    
        if not img_features:
            print("Error: Could not extract features from image.")
            return
    
        # Get image ID (use filename without extension)
        image_id = os.path.splitext(os.path.basename(args.predict))[0]
    
        # Predict caption
        feature = img_features[image_id].reshape(1, -1)
        caption = predict_caption(model, feature, tokenizer, max_length)
    
        # Display results
        #image = Image.open(args.predict)
        #plt.imshow(image)
        #plt.axis('off')
        #plt.title("Predicted Caption: " + caption)
        #plt.show()
        #plt.savefig("hyp.png")
    
        print(f"\nPredicted Caption: {caption}")
        return  # Skip the rest of the function for prediction mode

if __name__ == '__main__':
    main()


```

ဒီ တခါ အဓိက update လုပ်တာက BLEU score တစ်ခုတည်းနဲ့ evaluation လုပ်တာ မဟုတ်ပဲ chrF++ ပါထည့်ခဲ့တယ်။
ပြီးတော့ training လုပ်တဲ့အခါမှာ hyperparameter တွေကို user အနေနဲ့ play လုပ်လို့ ရအောင် command line argument အနေနဲ့ ဖြည့်ခဲ့တယ်။ 
ပြီးတော့ evaluation result ကို .pkl ဖိုင်တစ်ခုတည်း မဟုတ်ပဲ .txt ဖိုင်အနေနဲ့ပါ သိမ်းအောင် ပြင်ရေးခဲ့တယ်။  

## Call --help  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ python3.8 ./image_captioning.py --help
2025-06-21 12:58:20.217112: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 12:58:20.217133: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
usage: image_captioning.py [-h] [--data_dir DATA_DIR] [--model_dir MODEL_DIR] [--epochs EPOCHS] [--batch_size BATCH_SIZE] [--train]
                           [--evaluate] [--predict PREDICT] [--language {english,myanmar}] [--model_name MODEL_NAME]
                           [--skip_download] [--skip_feature_extraction] [--lstm_units LSTM_UNITS] [--dropout_rate DROPOUT_RATE]
                           [--learning_rate LEARNING_RATE] [--early_stopping EARLY_STOPPING] [--feature_size FEATURE_SIZE]

Image Captioning with Flickr30k Dataset

optional arguments:
  -h, --help            show this help message and exit
  --data_dir DATA_DIR   Directory to store dataset (default: ./data)
  --model_dir MODEL_DIR
                        Directory to save/load models (default: ./models)
  --epochs EPOCHS       Number of training epochs (default: 15)
  --batch_size BATCH_SIZE
                        Training batch size (default: 64)
  --train               Train the model
  --evaluate            Evaluate on test set
  --predict PREDICT     Path to single image for prediction
  --language {english,myanmar}
                        Caption language (default: english)
  --model_name MODEL_NAME
                        Model filename (default: best_model.h5)
  --skip_download       Skip dataset download (for prediction mode)
  --skip_feature_extraction
                        Skip feature extraction if features file exists
  --lstm_units LSTM_UNITS
                        Number of units in LSTM layer (default: 256)
  --dropout_rate DROPOUT_RATE
                        Dropout rate (default: 0.4)
  --learning_rate LEARNING_RATE
                        Learning rate (default: 0.001)
  --early_stopping EARLY_STOPPING
                        Patience for early stopping (default: None)
  --feature_size FEATURE_SIZE
                        Size of image features (default: 4096)
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ 

```

## Run Evaluation Again

chrF++ score ထုတ်ပေးတာကို စစ်ရန်။
evaluation result .txt ဖိုင်ကို ကြည့်ရန်။  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 ./image_captioning.py --evaluate --model_dir ./model | tee evaluate_py3.8.result.log
2025-06-21 13:03:11.201500: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:03:11.201522: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 13:03:12.803656: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 13:03:12.803823: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:03:12.803878: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:03:12.803920: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:03:12.803958: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:03:12.825731: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:03:12.825793: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:03:12.825803: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 13:03:12.826052: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Model loaded from ./model/best_model.h5
Evaluating: 100%|████████████████████████████████████████████████████████████████████████████████████| 810/810 [18:42<00:00,  1.39s/it]

Evaluation Metrics:
BLEU-1: 0.2261
BLEU-2: 0.1292
BLEU-3: 0.0703
BLEU-4: 0.0361
chrF++: 0.2066
Evaluation results saved to ./model/evaluation_results.pkl (binary) and ./model/evaluation_results.txt (text)

real    18m46.760s
user    20m46.257s
sys     1m19.536s
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$

```

Check ".pkl" and also ".txt" file ...  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt/model$ ls
best_model.h5  evaluation_results.pkl  evaluation_results.txt  features.pkl  tokenizer.pkl
(img2txt) ye@lst-hpc3090:~/intern3/img2txt/model$ ll -h evaluation_results.pkl
-rw-rw-r-- 1 ye ye 413K Jun 21 13:21 evaluation_results.pkl
(img2txt) ye@lst-hpc3090:~/intern3/img2txt/model$
(img2txt) ye@lst-hpc3090:~/intern3/img2txt/model$ wc ./evaluation_results.txt
  908 11046 55176 ./evaluation_results.txt
(img2txt) ye@lst-hpc3090:~/intern3/img2txt/model$
```

## Evaluation Results with 20 Epochs  

အင်္ဂလိပ် လေဘယ်အတွက် epoch 20 နဲ့ ရတဲ့ အသေးစိတ် ရလဒ်က အောက်ပါအတိုင်း...  

```
Evaluation Metrics:
BLEU-1: 0.2261
BLEU-2: 0.1292
BLEU-3: 0.0703
BLEU-4: 0.0361
chrF++: 0.2066

Sample Results:

Image ID: 436015762
Actual Captions:
1. a man prepares to enter the red building .
2. a man walking around the corner of a red building .
3. a man walks past a red building with a fake rocket attached to it .
4. a man walks under a building with a large rocket shaped sculpture .
5. a person walking by a red building with a jet on top of it .
Predicted Caption: startseq red and white man dropping pole on a ramp with a red sky behind him on top of him and a pole in background watch him in background watch him in background watch a building in the background

Image ID: 436393371
Actual Captions:
1. a brown doberman is outside with a stick in its mouth .
2. a brown dog shows his teeth .
3. a dog bites a stick .
4. a dog is biting a twig .
5. a dog with sharp teeth is chewing on a stick outside .
Predicted Caption: startseq brown dog digging in the grass with a jet of water in its mouth and another dog in the background looks at another dog in the background looks at the camera 's face with a rope in its

Image ID: 436608339
Actual Captions:
1. a couple posing in front of a picture wall
2. an adult couple pose by a cardboard cut out for a movie .
3. an asian couple are standing by a fantasy poster .
4. an asian couple stands near a wax figure .
5. one person in a brown suit with his arm around another in a hat by a wall .
Predicted Caption: startseq their bald man in a black jacket speaking to a group of men who are standing in front of a brick wall with their candles in their order to their backs to a unique table in front of

Image ID: 437054333
Actual Captions:
1. a bus filled with passengers in chicago at night .
2. a bus full of people waiting at a stop .
3. people are sitting on a bus .
4. people in a bus which is heading to 84 peterson .
5. there are people sitting on a bus that is labeled 84 peterson .
Predicted Caption: startseq street busy street with people in background are looking at other people in the background are looking at a train machine in the background are looking at a train machine in the background are looking at a train

Image ID: 437404867
Actual Captions:
1. a woman is sitting on a sidewalk with a cellphone at her ear .
2. a woman rests on the curb of a city street while talking on her cellphone .
3. a woman sits on the curb while talking on her cellphone .
4. a woman sits on the edge of a sidewalk with a garbage bin beside her
5. woman sits on the curb talking on a cellphone .
Predicted Caption: startseq screen in a darkened room with a silver tiled floor behind them with a tiled floor behind him and a tiled floor behind them with lots of graffiti in the background behind them with a tiled floor behind

Image ID: 437527058
Actual Captions:
1. a caravan of snowmobile travel through the snow .
2. a pair of people in heavy winter jackets rides through the snow on a snowmobile .
3. people riding something in the snow .
4. person on a polaris ski mobile in the snow .
5. the man wearing a blue helmet is riding a polaris .
Predicted Caption: startseq snowmobiles driver in goggles and a helmet in goggles riding a snowmobiling ride through the snow while another man looks on the left of the road in the snow holds the fellow driver and the fellow watches watches

Image ID: 437917001
Actual Captions:
1. a dark colored man is laying on newspapers by a metal railing with his shoes off .
2. a homeless man is lying on the ground with his stuff strewn around .
3. a homeless man is sleeping outside at the top of a staircase .
4. an man is sleeping on top of his clothes on concrete stairs .
5. man sleeping on the street .
Predicted Caption: startseq seems to be sleeping on a patio of a tire bench and a sleeping blanket on the ground in the background watching the man is sleeping on the ground in front of him is sleeping on the ground

Image ID: 438639005
Actual Captions:
1. a boy in red and a girl pink are walking through a low cut field .
2. the little boy and little girl are walking side by side .
3. two small children walk away in a field .
4. two small children walking in a field .
5. two young children are walking across an open field .
Predicted Caption: startseq children playing soccer in a park game a game of people in the background watch him and a dog in the background watch him is playing soccer in the grass watch him at a park game away from

Image ID: 439037721
Actual Captions:
1. two men sitting on the bank of a lake with an ice chest .
2. two people having a picnic by a lake .
3. two people having a picnic by the shore .
4. two people sitting on grass in front of a lake looking at the sky .
5. two people with hats looking at a lake while sitting on a yellow-grassed hill .
Predicted Caption: startseq two men are standing on a dirt track with a lake behind him on the beach below it is looking at the edge of the water below it is standing in the distance below it passes a lake

Image ID: 439049388
Actual Captions:
1. people , possibly fishermen , with their boats in shadow on shore at an orangesunset
2. a man in an orange vest is standing next to a yellow canoe .
3. people tend canoes at the edge of a body of water during a dimly lit time of day .
4. the men are getting their kayaks secured on the beach for the night .
5. two men standing on the shore beside their kayaks at dusk .
Predicted Caption: startseq raises the ocean raises the arms as her raises his arms in the setting setting the setting sun watches to the arms below him into the water below him and the man watches him and the man watches

Image ID: 439492931
Actual Captions:
1. a cluster of four brown dogs play in a field of brown grass .
2. four dogs are together in the field of dry grass .
3. four dogs in a grassy area .
4. four medium-sized dogs wrestle with each other on a grass field .
5. four small dogs play outside .
Predicted Caption: startseq brown and brown dog playing with red dog on grass with red and red dog in the background with red dog in background stare at a dog with red and red flowers in the background with a red

Image ID: 439569646
Actual Captions:
1. a girl is hiding behind a painted wooden structure inside a building .
2. a little girl with a red dress facing a panel with her back to the camera .
3. a young blonde girl wearing a red dress kneeling on a red carpet .
4. a young girl faces a white and black wall in a red-carpeted room .
5. girl kneeling on a red carpet .
Predicted Caption: startseq jumping bed with a little girl in a red outfit jumping up on the bed of a colorful house on a blanket in the background in a bedroom stall stall on its hind legs on the floor in

Image ID: 439916996
Actual Captions:
1. brown dogs and a woman in a yard
2. a brown dog persues a frisbee across the grass as the thrower watches .
3. a woman in a blue jacket watches as her two brown dogs play with a red ball in a grassy yard .
4. a woman throws a frisbee for her two brown dogs to chase .
5. a woman watches a brown dog run away from a house across the grass .
Predicted Caption: startseq two dogs are playing with a blue ball in a yard while a dog stands in the background watching a dog that is standing by a dog in a backyard setting setting setting and a blue blanket in

Image ID: 440184957
Actual Captions:
1. a clown shares cut-out pictures of children .
2. a dirty looking clown holding up two paper cut outs of children with blond hair
3. a man wearing a balloon hat and a grassy shirt holds up two large paper dolls .
4. a man wearing a balloon hat holds up colored cut-out drawings of two men .
5. the man wears balloons on his head and holds paper people .
Predicted Caption: startseq thin girl in a red shirt and red hat is standing in front of a red building with a flag painted in the background behind her face in the background behind her face painted in the background of

Image ID: 440190907
Actual Captions:
1. a group of people walk through a shopping mall .
2. many people walk through the store .
3. people browse in a store .
4. people strolling through an indoor market .
5. the shoppers are walking in a store .
Predicted Caption: startseq people waving a frisbee in a restaurant waving lit in a restaurant in front of a building with a colorful restaurant in the background in a restaurant in a restaurant like lit restaurant in a restaurant scene in

Image ID: 440737340
Actual Captions:
1. a black man with a red mask is carrying a box .
2. a man in a domino mask carries an amplifier up a hill .
3. a man with a mask carrying a black speaker
4. a masked man in bright clothing carrying a large box .
5. black man lifting black box is watched by black dog .
Predicted Caption: startseq old man in black and white shorts and black shorts is jumping up to touch a lake with a bottle of water on the ground behind him and a woman in a red coat is running on a

Image ID: 441212506
Actual Captions:
1. the black dog runs with a ball with two smaller dogs behind it .
2. three dogs playing in a field , one with a ball in its mouth .
3. three dogs race towards the viewer over a lawn .
4. three dogs running in grass , one carrying a tennis ball in mouth .
5. two small dogs follow a larger dog with a tennis ball
Predicted Caption: startseq two dogs playing in the grass with a toy in the background and a bunch of toys in the background are playing with a toy in the background and one dog following them a toy in the background

Image ID: 44129946
Actual Captions:
1. a couple watches a boat against a skyline .
2. a man and woman sit on a bench , watching a boat go by .
3. the sun is setting while a man and woman watch a boat go by .
4. two people sit on a bench and watch a boat on the water .
5. two people watching a boat sail past .
Predicted Caption: startseq sunset in the water at sunset edge at the water with a lake in the background the city city skyline behind him and the sun sets behind him and sail sail out the horizon behind him and a

Image ID: 441398149
Actual Captions:
1. a female jogger wearing red .
2. a girl with headphones is running next to some street signs .
3. a woman in a red outfit is jogging next to several street signs .
4. a woman jogging across an intersection .
5. the lady in red shorts jogs near a stop sign while listening to music .
Predicted Caption: startseq rides a red ramp in the street with a sign saying hanging in the background and a sign in the background and a sign in the background is walking on the sidewalk in front of a bank of

Image ID: 441817653
Actual Captions:
1. a bearded man wearing a denim jacket and a hat sits on a park bench
2. a bearded man wearing a denim jacket sits on a bench .
3. a man with a bushy beard and a baseball cap sits on a park bench .
4. an old man with a long beard and jean jacket sits on a park bench .
5. an old man with a long white beard , glasses , and a hat is sitting on a park bench .
Predicted Caption: startseq work for a video game while another man looks at the camera while another man watches him the headphones smokes the video of the man in the blue shirt and headphones around the headphones behind him smiles at

Image ID: 441921713
Actual Captions:
1. a bird lands on a mans glove .
2. a man holds a bird .
3. a man holds a falcon on his arm .
4. gloved man holding a bird of prey .
5. the man is wearing gloves and holding a hawk in his hands .
Predicted Caption: startseq man in black shirt and black shirt and red shirt standing in a busy street with other people watching him and another man in a red jacket and red shirt and red shirt in front of a crowd

Image ID: 442220883
Actual Captions:
1. a brown dog has a white toy in its mouth .
2. a dog holding a white stuffed animal .
3. a tan dog hangong on to a white plushie toy .
4. a yellow dog is chewing on a white stuffed toy .
5. the dog is holding a stuffed toy in his mouth .
Predicted Caption: startseq dog with red collar licking its nose in the water with its mouth open wide wide wide wide open wide wide area in background nearby third dog 's face in the background in background are nearby themselves in

Image ID: 442594271
Actual Captions:
1. a bunch of people at the beach .
2. people are enjoying a sunny day on a sandy beach by the ocean .
3. people are on the beach and there is a kite in the air .
4. people on the beach and a kite in the sky .
5. sandy beach , people walking , laying , sitting , a kite is flying .
Predicted Caption: startseq crowded beach crowded beach at the beach raises the beach of the sun sets on the beach watching the beach comes to the beach at the beach watching the sun sets on the beach watching the sun sets

Image ID: 442918418
Actual Captions:
1. a brown dog is jumping over a fallen tree in the woods .
2. a small tan dog jumps over a small log .
3. tan colored dog jumping over a branch in the forest .
4. the dog leaps over the log in the forest .
5. the white dog is jumping over a fallen tree .
Predicted Caption: startseq bare snowy dog carries a bridge over a bridge in a wooded area in a wooded area surrounded by snowy area in fall fall leaves the leaves in the fall area in snowy area in the fall area

Image ID: 443430496
Actual Captions:
1. a brown dog swimming in murky water .
2. a brown dog swims in the murky water .
3. a dog with yellow fur swims , neck deep , in water .
4. a golden retreiver swimming in the water .
5. a yellow dog is swimming in the water .
Predicted Caption: startseq brown dog wades in water with a stick in its mouth in the water with a stick in its mouth in the background is in the water with a stick in its mouth in the background is in

Image ID: 443885436
Actual Captions:
1. a tan curly haired dog jumps in the snow with a stick in its mouth .
2. a white dog catches a stick in the snow .
3. a white dog holds a stick in its mouth while it runs through snow .
4. a white dog jumps in the snow .
5. a white dog with light brown markings has a stick in his mouth and his paws in the snow .
Predicted Caption: startseq running running in the snow with a stick in its mouth running through the snow covered ground in the snow running in the snow running in the background of snow and snow covered grass in the background running

Image ID: 444047125
Actual Captions:
1. a person hiking at the foot of snowcapped mountains .
2. a person walks in the valley between tall mountains .
3. a person with a backpack and walking stick , walking towards the mountains in the valley below .
4. people with backpacks hiking in the mountains .
5. three people walk through a valley towards snowy mountains .
Predicted Caption: startseq mountains in the mountains are sitting on a mountain mountain in the mountains and mountains below them and mountains in the background mountains behind them with mountains in the background below them with mountains in the background below

Image ID: 444057017
Actual Captions:
1. a little girl gets her picture taken while on the merry-go-round .
2. a little girl in pink clothes holding yellow rods .
3. a little girl on a piece of playground equipment
4. a little girl sitting on a playground ride .
5. a young girl looks up as she rides on a merry-go-round .
Predicted Caption: startseq eye adult boy in blue shirt and navy blue shirt is hanging off a blue pole on a playground set of tires on a playground set of tires on a brick wall with a stick in his mouth

Image ID: 444481722
Actual Captions:
1. a dark skinned man walks by a woman talking on a cellphone .
2. a male walking and a female talking on the phone beside the concrete building .
3. people stand outside near a concrete wall and a window .
4. two people standing on the sidewalk .
5. two women , one carrying a purse and papers , are standing on a sidewalk .
Predicted Caption: startseq skater kneeling on a basketball court with a backpack and a backpack and a break in the background watching him and a break in a white shirt watch them on a basketball court with a basketball in the

Image ID: 444803340
Actual Captions:
1. a guy and a girl , both wearing white shirts and jeans , stand under a flowering tree .
2. a man and a woman are talking in a park
3. a man and woman standing underneath the tree are talking .
4. a man in a white shirt is standing in the grass showing something to a woman in a white shirt .
5. a young couple both wearing white shirts and blue jeans standing in a light misty rain
Predicted Caption: startseq headphones jumping for a picture in a park setting setting a white top and a white top and red top watches him on the ground below him is checking her head up to her feet to the camera

Image ID: 444845904
Actual Captions:
1. a man in a yellow helmet climbs a cliff face , snow behind him .
2. a man is climbing up a wall with a rope
3. a man leans back while climbing a mountain tethered to a rope .
4. he is rock climbing .
5. man with helmet rock climbing in a snowy area .
Predicted Caption: startseq cross country middle eastern middle aged middle aged middle aged middle aged middle aged middle aged middle of a mountain biker getting ready to get a rope stunt in the middle of a wooded area with a collection

Image ID: 444872454
Actual Captions:
1. a group of students dressed in sweatshirts and jackets head towards the right .
2. a group of students walking on campus , some carrying books .
3. a group of students walk together .
4. a group of young people are walking through a park under blossoming trees .
5. several young women walk near blossoming cherry trees .
Predicted Caption: startseq seven boys are posing for a picture in a park with a crowd of people watching her heads in the background watching the same team looks at a party and a large crowd watching the same sticks behind

Image ID: 444881000
Actual Captions:
1. a group of college students walk in nice weather .
2. a group of people walk in the park , while some talk on phones .
3. a group of students are walking through the campus .
4. a group of young people walking with two talking on cellphones .
5. several young people walking casually around
Predicted Caption: startseq two dogs are walking on a lawn with a large rope in the background and two dogs below them a man and a black dog watch them on a leash of them with a dog in the background

Image ID: 445148321
Actual Captions:
1. a person in the distance hikes among hoodoos with stars visible in the sky .
2. a person standing on a ridge in the desert .
3. interesting rock formations in the desert landscape , with stars above .
4. the night sky in the desert .
5. there is a person standing a mountain that has some interesting shapes .
Predicted Caption: startseq climbing rocky mountain mountains with a figure is walking behind him and another figure behind him is walking on a mountain mountain in the background and mountains behind him visible behind him and another hikes on a bluff

Image ID: 445655284
Actual Captions:
1. a black and brown dog walks through the snow near a building .
2. a black dog , running in the snow .
3. a black dog running in the snow by some trees .
4. a large black and tan dog is running across the snow in a wooded area .
5. the black and brown dog is running through the snow .
Predicted Caption: startseq dog in the snow with a ball in its mouth in the background is digging in the snow with its mouth open in the snow covered ground in the snow with a red patch in the background and

Image ID: 445861800
Actual Captions:
1. three men walking on a sidewalk in a city .
2. three people are walking down the street with cars and buildings in the background .
3. three people stand along a main road .
4. three people walking on a sidewalk with 3 light colored cars in the background .
5. three people wearing winter clothes standing on the sidewalk near a street
Predicted Caption: startseq signs near a street rack with a silver hood and advertisement on the street in urban area and other people walking on the street in urban urban area and traffic area in front of a bus advertisement by

Image ID: 446138054
Actual Captions:
1. a man in an orange hat jumping .
2. a man jumps in the middle of a rocky desert .
3. a man wearing a white shirt and an orange shirt jumped into the air .
4. man in khaki pants does elaborate kick in desert
5. man jumping with a rock formation in background .
Predicted Caption: startseq cyclist wearing mud and black t shirt jumping into the air with a cloudy sky behind him in the background below him on top of the ocean below him below him on top of the ocean below below

Image ID: 446286714
Actual Captions:
1. an elderly man is sitting on a bench .
2. an older man wearing a brown coat siting on a bench .
3. an old man in a coat and hat sitting on a park bench .
4. old man in tan jacket and black cap sitting on bench
5. the older man with the shopping bag and cane is sitting on a bench .
Predicted Caption: startseq work of a man in a green shirt and sunglasses is standing in front of a brick wall with a bottle of other men in the background and a woman in a green jacket is standing in front

Image ID: 446291803
Actual Captions:
1. these woman are watching people play tennis from a bench .
2. two individuals watch a tennis match .
3. two people sit on a park bench while watching a neighborhood tennis match .
4. two people with red scarves on their heads are watching tennis .
5. two women sitting on a bench in front of a tennis court near a building complex .
Predicted Caption: startseq naked woman in black leather jacket and red boots is riding a bike on a sidewalk with a crowd of people behind him on the ground behind him and a woman in a red vest walks nearby the

Image ID: 446514680
Actual Captions:
1. two brown dogs are fighting and they are both wearing red .
2. two brown dogs rough house outside .
3. two brown dogs wearing red collars look at each other while running along a dirt field .
4. two dogs play together .
5. two large brown short haired dogs with collars play chase in a field .
Predicted Caption: startseq brown dog running on a beach with a bottle in the background on a beach in the background two other dogs run in the background and a dog in the background are running on the beach in the

Image ID: 447111935
Actual Captions:
1. the two greyhound dogs wearing sweaters are playing in the grass .
2. two dogs play in the grass .
3. two dogs wearing shirts play in the green grass .
4. two dogs wearing sweaters play in a field .
5. two dogs wearing sweaters play in the grass .
Predicted Caption: startseq dog with red collar and black collar is being held by a dog 's ground 's ground 's ground 's or clover lot of trees and weeds and a red bucket in its mouth and a dog in

Image ID: 447722389
Actual Captions:
1. a brown and white dog is jumping high and catching a blue ball .
2. a dog is jumping and catching a small , blue ball in a park surrounded by two other dogs .
3. a dog jumps and catches a blue ball in his mouth .
4. a dog jumps in the air to catch a blue ball .
5. three dogs run on grass , one leaps to catch blue ball .
Predicted Caption: startseq colored dog jumping in the grass with a puffy stuffed animal in its mouth and a dog in the background and a dog in the background and black dog running in the grass and grass and stuffed object

Image ID: 447733067
Actual Captions:
1. a girl in a skimpy bikini outfit walks and carries a helmet .
2. a scantily clad girl , in a helmet , walks away from the camera , down a busy sidewalk .
3. a woman wearing a helmet , tall boots , and short shorts walks down the street .
4. girl in bikini bottoms , boots and a helmet walking away at a street fair .
5. the woman in the purple bikini and pink top is wearing a safety helmet .
Predicted Caption: startseq wearing a black sweatshirt wave at a parade painting a parade wave on a parade wave behind her colors in the background watching a girl in a red outfit is raising her hand while another girl in a

Image ID: 447800028
Actual Captions:
1. a black dog playing with a purple toy in the snow .
2. a black dog runs through the snow carrying a blue toy .
3. a dog plays in the snow .
4. dog running with a purple toy in the snowy field .
5. the black and brown dog carries a purple toy in the snow .
Predicted Caption: startseq black dog running through snow covered ground in snow covered area in snow covered area in snow covered area in snow and snow covered area in snow and snow and snow and black dog in the snow and

Image ID: 448252603
Actual Captions:
1. a boy pointing in a direction on a dirt road .
2. a boy with a backpack sits on a trail and points .
3. a man points his finger to the path ahead as he sits on the dirt path .
4. a man with a backpack is sitting in a dirt road and pointing toward the horizon .
5. a young man sitting in the middle of a dirt road pointing up the road .
Predicted Caption: startseq long long haired boy is walking on a dirt road by a river with a lot of people nearby a river in the background and a river behind them points at the camera below him on a beach

Image ID: 448257345
Actual Captions:
1. a dog is staring at the food in the plate of a person eating .
2. a person holding a dog while they eat .
3. a person is eating a plate of pasta with a black and brown dog on his or her lap .
4. a person is eating pasta , while a dog is watching .
5. someone in a blue and white striped sweater is eating and the dog next to them is interested in their food .
Predicted Caption: startseq dog with black and black striped collar sitting on a blue floor with a pair of dogs on its nose and its mouth open open showing its nose to look up behind it is eating a pair of

Image ID: 44856031
Actual Captions:
1. a brown dog is sprayed with water .
2. a dog is being squirted with water in the face outdoors .
3. a dog stands on his hind feet and catches a stream of water .
4. a jug is jumping up it is being squirted with a jet of water .
5. a tan , male dog is jumping up to get a drink of water from a spraying bottle .
Predicted Caption: startseq dogs playing in a backyard playing lawn in the backyard playing with a chew toy in the background by a backyard building nearby a backyard building nearby a bench in the background and a dog in the backyard

Image ID: 448590900
Actual Captions:
1. a brown dog is sniffing around green grass on a hill .
2. a dog is digging a field .
3. a dog stands in a large , grassy field .
4. a dog walks alone in a field .
5. a dog with a red harness tracks a scent in a field .
Predicted Caption: startseq dogs playing in a field of dry grass and weeds in the background and weeds are in the background in a field of dry grass and weeds and green flowers and a red toy in the background and

Image ID: 448658518
Actual Captions:
1. a large man dressed in black on a street corner by a red brick building .
2. a man dressed in black is waiting at a crosswalk .
3. a man dressed in black stands at a street corner near a crossing light .
4. a man stands at a traffic light , waiting to cross the street .
5. man in black waits at crossing signal near large brick building .
Predicted Caption: startseq skater grinding a rail on a rail near a skate park ramp with a white advertisement behind him on it it is performing a stunt on his board in the city street with a white pole in the

Image ID: 448916362
Actual Captions:
1. a dog is running through a field with its tongue hanging out .
2. a dog runs with his tongue hanging out .
3. a dog with its mouth open is running .
4. brown and cream dog with tongue out
5. the white and black dog runs on the field with his tongue hanging out .
Predicted Caption: startseq dog running through a field with a red toy in its mouth in the background with a red toy in its mouth in the background one eye in the background has its mouth open in the background behind

Image ID: 449287870
Actual Captions:
1. a female toddler wearing a pink shirt is playing on a playground .
2. a little girl in pink and purple stands on a playground .
3. a very young girl is walking on a playground .
4. the little girl is playing at the playground .
5. young child in pink top and purple pants clutching a turquoise guard rail .
Predicted Caption: startseq photograph of a little girl on a red slide jumping off of a playground slide at a playground wheel on a playground slide at a park park nearby playground equipment nearby a playground poles nearby a playground and

Image ID: 449352117
Actual Captions:
1. a brown and black puppy stands by a camera .
2. a dog chews on the strap of a camera case .
3. a dog gnaws on the strap of a camera .
4. a small dog chewing on a black strap .
5. a small dog is standing behind a camera .
Predicted Caption: startseq car with red and red sweater on carpet with a stuffed animal in its mouth and its mouth wide open wide open hand to him to the right of him 's nose to the other 's nose is

Image ID: 450596617
Actual Captions:
1. man and woman walking near the ocean .
2. two people are walking alongside a decorative railing while wearing winter gear .
3. two people are walking by the ocean .
4. two people in coats walking next to a fence .
5. two people walk together on a cold day .
Predicted Caption: startseq ice asian girl in shorts and blue shorts walking across salt and rail at night with man in red shirt and blue shorts on the sidewalk with a blue pole in the background setting the woman in red

Image ID: 451081733
Actual Captions:
1. a man on the beach in jeans looking at his camera .
2. a shirtless guy turned around videotaping something at the beach .
3. barechested man filming at the beach .
4. the man is wearing rolled up blue jeans and holding a video camera on a stone beach .
5. the shirtless man used his camera while sitting on the rocky beach .
Predicted Caption: startseq spectators are playing in a lake with a crowd of people behind him and a man in a blue shirt and blue shorts and sunglasses on a narrow beach with laundry behind him and two spectators behind him

Image ID: 451326127
Actual Captions:
1. a dog jumping over a fallen tree in the forest
2. a dog leaps over a tree fallen in the forest .
3. a large dog jumping over a fallen tree in the forest .
4. large brown dog jumps over a low tree trunk in a wooded area .
5. the german shepherd is jumping over a fallen tree .
Predicted Caption: startseq plants is walking through a wooded area with fallen leaves in the background behind it flowers to it it to fallen leaves in the woods in the woods below it to fallen leaves in the woods below it

Image ID: 451597318
Actual Captions:
1. a brown dog leaps up to catch an orange toy .
2. a dog catches a disk in the air .
3. a dog is jumping in the air to catch an orange frisbee .
4. a dog leaping to catch a frisbee in the yard .
5. brown dog leaping up with orange disc in mouth with blue and yellow toy boat in background .
Predicted Caption: startseq men playing with a ball in a playground and yellow sports field with a dog in the background watching the ground in the background watching the dog in the blue outfit is playing with a ball in the

Image ID: 452345346
Actual Captions:
1. a brown and white dog chews on a tire .
2. a brown and white dog with pointy ears stands outside in sand holding a small tire in its mouth .
3. a brown , black and white dog holding a tire in its mouth while standing on sand
4. a bull terrier terrorizes an old tire in the sand .
5. a dog standing in sand , holding a tire in his mouth .
Predicted Caption: startseq dog licking its nose in the grass with its mouth wide open wide wide wide open legs in the background showing its mouth wide open wide wide open mouth wide and its mouth wide open wide open mouth

Image ID: 452363869
Actual Captions:
1. a black dog chases a ball in the grass .
2. a black dog is chasing a ball on a green grass .
3. a dog and a ball on green grass and in front of trees .
4. a dog chases a ball in the grass .
5. green grass field , a black dog running after a ball .
Predicted Caption: startseq playing a baseball lawn playing with a ball in the grass with a red ball in the background setting the background is falling rope in the background in the background setting the background of a dog tries to

Image ID: 452416075
Actual Captions:
1. a baby dressed in blue jumps outside .
2. a child is bouncing on a trampoline that is next to the house .
3. a small child jumps up on a trampoline .
4. a young boy jumping on a trampoline outside of a house .
5. the little boy with red hair jumps on the trampoline .
Predicted Caption: startseq orange and white dog in blue shorts jumping over a playground wall with a blue blanket on the ground in the background with a blue blanket in the background with a blue blanket on the ground in the

Image ID: 452419961
Actual Captions:
1. the three children are in a cage .
2. three children are locked in a cage .
3. three children in a black dog kennel .
4. three small children are in a cage .
5. three well dressed blond children in a cage .
Predicted Caption: startseq two dogs are fighting up at a table with a metal piece position in the background showing their mouths wide open in the background while two men look at him at the other in their mouths are looking

Image ID: 453473508
Actual Captions:
1. a brown dog is running though a river .
2. a brown dog jumping in a stoney brook .
3. a brown dog runs through shallow water .
4. a dog wading through shallow water .
5. a golden retriever splashes in the water .
Predicted Caption: startseq float in a lake with a lake in the background both dogs are in the water facing the side of the lake with a lake in the background both dogs are in the background both are playing in

Image ID: 453756106
Actual Captions:
1. a large , brown , fluffy dog with a small white and brown dog on a dirt surface .
2. a large dog is playing with a small dog in the dirt .
3. a small dog and a large dog play together .
4. bigg playing with little dog in dirt .
5. two dogs play with each other in the dirt .
Predicted Caption: startseq two dogs are playing roughly together on a lawn panting deep in the grass and two other dogs are playing in the grass and one is lying on the ground and another dog looks on its eye and

Image ID: 454686980
Actual Captions:
1. a girl who looks upset with her arms crossed .
2. an indian woman in a black shirt stands with her arms crossed looking at two other people talking to each other .
3. a person in a red and black shirt has their arms crossed and looks at the camera .
4. a teenage girl is standing with her arms crossed in a busy street .
5. woman in dark shirt standing alone in front of a yellow car .
Predicted Caption: startseq man in orange shirt and blue shorts holding basketball and other man in orange shirt in background watches him to other spectators in background with pride bottle bottle of them in pride court with a bottle of other

Image ID: 454691853
Actual Captions:
1. a dog carries a leash in its mouth .
2. a fluffy dog carries a black leash in its mouth .
3. a large furry brown dog is walking with a leash in his mouth .
4. a yellow dog carries a black leash .
5. dog walking with his lease in his mouth .
Predicted Caption: startseq light brown dog playing with a toy in the grass with a toy in its mouth in the background in the grass striking it to be hanging in the sky and grass striking it to the ear of

Image ID: 454709143
Actual Captions:
1. a man dressed in blue holds a sign while standing behind a couple of trees and in front of a large concrete wall with red writing on it .
2. a man holds up a cardboard sign near a wall with red graffiti .
3. a man in a black jacket is standing between two trees holding up a sign .
4. a man stands on the side of the road , holding a cardboard sign .
5. a man stands with a cardboard sign on a road
Predicted Caption: startseq fall tent in a lake with a white wall in the background looks down to the water below it is casting a bottle of water in the water to the water throws her picture in the background below

Image ID: 455611732
Actual Captions:
1. a hiker walks on rocky ground at the base of a foggy mountain .
2. a lone hiker walking on dirt with a snowy mountain background .
3. a person is hiking along rough terrain with fog and mountains in the background .
4. distant person with blue backpack hiking in rocky area , mountains in background .
5. the person is hiking .
Predicted Caption: startseq two people are walking through a field of water and weeds behind them visible on the ground below them with a cloudy sky behind them looks at the sky and mountains behind them looks at the water below

Image ID: 455856615
Actual Captions:
1. a skier flies through the air .
2. ski boot gets pulled out of the ski .
3. the feet of a skier with one boot coming out of the ski and casting a shadow .
4. two boots are on two skis moving very fast .
5. two feet wearing yellow ski boots on ski
Predicted Caption: startseq skier skiing down a snowy trail in the snow and two pine poles in the background and a pine camera trail behind them wearing a backpack skis down the trail in the background the skier is crouched on

Image ID: 456299217
Actual Captions:
1. a girl sits outside at a large fountain .
2. a woman and two others are sitting nearby a decorative water fountain .
3. a woman sits on a wall next to a large conical fountain .
4. a young woman sits near a fountain .
5. woman in black poses near a pyramid fountain .
Predicted Caption: startseq skater jumping high in the air and jumping in the air and lots of space on the ground below him and a church in the background watch him washes skate and earth higher in the city space the

Image ID: 456512643
Actual Captions:
1. a brown dog is running through a grassy field .
2. a brown dog running through grass .
3. a dog runs in a grassy field .
4. a golden-brown dog running through a green field .
5. a tan dog is running fast through tall green grass .
Predicted Caption: startseq long brown dog is running through the field with a stuffed animal in its mouth in the background stare another dog 's in the background stare another dog 's in the background stare another dog 's in the

Image ID: 457631171
Actual Captions:
1. a man extends his arms in front of a large rock formation .
2. a man in the desert .
3. a man poses in front of a large rock formation .
4. a man standing next to a huge rock formation .
5. a man stands next to a strange rock formation with his arms in the air .
Predicted Caption: startseq heavy heavy heavy heavy heavy heavy heavy heavy heavy heavy heavy man is climbing a rocky hill in the middle of a rocky area with a mountain behind him on it it is walking on a mountaintop in

Image ID: 457875937
Actual Captions:
1. two black , brown and white dogs running in green grass with ears up on heads .
2. two dogs run through a field of grass
3. two fluffy dogs run through the grass .
4. two look-alike dogs running in the green grass .
5. two small dogs run through the grass .
Predicted Caption: startseq running with a stick in its mouth running through the grass with a tennis ball in its mouth in the background with a tennis ball in its mouth in the background with a tennis ball in its mouth

Image ID: 457945610
Actual Captions:
1. a girl in striped swimsuit is jumping into the ocean .
2. a little girl in a striped bathing suit jumps in a large body of water .
3. a little girl in a striped bathing suit jumps in the ocean .
4. a young girl in a striped bathing suit jumping in the ocean .
5. girl jumping over wave
Predicted Caption: startseq two men are jumping into the water and one is falling into the water to the water to the water to the other 's head and the girl in the blue shirt is jumping into the water to

Image ID: 458004873
Actual Captions:
1. a man is sitting on a bench facing another man who is standing .
2. a man sits on a bench while another man walks toward him .
3. a person sitting on tan bench and man in green shirt standing on black and grey floor .
4. this over the top photo shows two men taking a break .
5. top-down view of a man sitting on a bench inside with a standing man facing him .
Predicted Caption: startseq pose on a brick wall surrounded by buildings in the background watch him washes structures below him and a church films him at the unique buildings behind him and a church films him behind him and one shines

Image ID: 458183774
Actual Captions:
1. a dog rolls on his back in the grass .
2. a large tan dog is rolling around on its back in a yard of grass .
3. a large , tan dog is rolling in green grass .
4. big yellow dog rolling around on the green lawn .
5. large dog rolling on its back in green grass .
Predicted Caption: startseq long long haired dog running across the grass with a stick in the background behind her visible in the background behind her dog in the background is rolling in the background in the sun setting behind them in

Image ID: 458213442
Actual Captions:
1. a black and white dog is jumping over a hurdle .
2. a black and white dog jumps over a bar in an agility test .
3. a dog jumps over a hurdle on a grass field .
4. a dog leaps over a bar on an obstacle course
5. the black and white dog jumps over an obstacle .
Predicted Caption: startseq jump over a fence with a red and white dog in its mouth jumping over a fence in its mouth between a fence in the background surrounded by white poles jump over a fence in the grass and

Image ID: 458735196
Actual Captions:
1. a brown dog indoors , with a large pink toy .
2. a dog with a wrinkled face bites on a pink toy .
3. a wrinkled dog playing with a pink chew toy
4. the dog is carrying a pink ball in its mouth .
5. this is a strange sight , a dog delivering a cookie .
Predicted Caption: startseq brown dog with red collar is falling toy in the air with food visible in its mouth and mouth open mouth open visible nearby it to reach him in the background showing its mouth open open mouth open

Image ID: 459284240
Actual Captions:
1. a toddler starting at a clown walking down a snowy sidewalk .
2. several people including a child and a clown are walking towards a snowy sidewalk
3. three adults and a toddler stand on a snowy path .
4. three adults and one child are walking along a paved path that is snow covered .
5. two adults , a child , and a clown walking down a sidewalk .
Predicted Caption: startseq men in winter clothes are standing in a city street with their backs to the camera in the background a man in a red jacket is standing in front of a group of men in a run on

Image ID: 459778335
Actual Captions:
1. a father with his two kids at the ocean with the young boy flying up in the air .
2. a little boy jumps from his fathers arms on the beach .
3. a man tosses a boy into the air at the beach .
4. an adult man is throwing a child into the air at a beach while another child watches .
5. a young boy is thrown by a man as a girl watches at the beach .
Predicted Caption: startseq two boys cartwheel on the beach with their arms in the air on the beach with a beach in the background watching the beach in the background is watching the beach in the net and the man watches

Image ID: 459814265
Actual Captions:
1. a big , shaggy dog runs in a field of dandylions .
2. a dog running in a field of daisies
3. a dog sitting in the grass , with his tongue out
4. a long haired dog frolics in a meadow of yellow flowers .
5. a shaggy dog plays in a field of grass and yellow flowers .
Predicted Caption: startseq two dogs playing with each other in a grassy area with a grassy field in the background nearby a body of water in the background and a body of water in the background there are a small dog

Image ID: 460195978
Actual Captions:
1. a black dog is in the grass with a woman in jeans .
2. a grey in a grey sweashirt running alongside of a small dog
3. a person playing with their black dog in the grass .
4. a woman and a dog are running in a field .
5. a woman flies a kite in a field while her dog watches .
Predicted Caption: startseq children playing with a ball in the grass with a flag in the background watch it to get the ball in the background watch it is catching a ball in the background and a dog in the background

Image ID: 460350019
Actual Captions:
1. a black dog and a woman in a red shirt playing tug of war .
2. a dog is pulling on one end of a rope and a girl is pulling on the other .
3. a woman plays tug-of-war with her black dog in a brown landscape surrounded by trees .
4. a woman plays with her rottweiler dog outside .
5. a woman and a dog playing outside
Predicted Caption: startseq dogs playing on a paved hill with a red rope on the ground and a rope in the background and a black and black dog walk on the grass with a red rope and red rope on it

Image ID: 460478198
Actual Captions:
1. a dog chasing another dog by a lake .
2. a husky chasing a brown spoted dog at the shore .
3. two dogs , a spaniel and a husky , chase each other across the sand by a body of water .
4. two dogs chase each other near the water .
5. two dogs playing by the shore .
Predicted Caption: startseq two dogs are playing in the water with a toy in the background and one is carrying a stick in its mouth and a stick in its mouth is carrying a stick in its mouth and a stick

Image ID: 460781612
Actual Captions:
1. a black and white dog catches a frisbee in midair .
2. a black and white dog is midjump and has a frisbee in his mouth .
3. a black and white dog jumps up in the air to catch a frisbee .
4. a dog jumps in the air , catching a frisbee in its mouth .
5. a white dog in a jump , holding a plate in his mouth .
Predicted Caption: startseq two dogs are playing in a field of grass and one is lying in the background with a red toy in the background and a dog in the background is running through the grass and a red building

Image ID: 460935487
Actual Captions:
1. a black and white dog is running up a path towards some potted plants .
2. a dog follows another dog around the corner but looks back .
3. a dog is turns back toward the camera near some potted plants .
4. a dog turning to look at the camera .
5. a white and black dog in a hallway filled with potted plants .
Predicted Caption: startseq with a black and white dog is playing with a ball in the yard with its mouth open in the background its mouth open its head in the background its head its head up its head in its

Image ID: 460973814
Actual Captions:
1. a group of people sitting around a table drinking tea or coffee
2. three individuals sit at a table , smiling .
3. three people gather around a table for beverages .
4. three people gather around the table and have their picture taken .
5. two women and a man sit at a table having coffee in a home .
Predicted Caption: startseq party sitting on a table with candles in their dinner table behind them with candles on their lap and candles on their faces in the dinner watching a desk of candles in their candles are sitting on a

Image ID: 461019788
Actual Captions:
1. a couple stands on a dock by the water hugging .
2. a stone dock and a couple hugging at the end , water behind .
3. two people are hugging at the end of a stone jetty that looks out over the ocean .
4. two people embrace on the end of a dock .
5. two people stand on the pier looking at the ocean and embrace .
Predicted Caption: startseq two men are sitting on a dock near a lake skyline below buildings below them below buildings beyond the water skyline below it to reach the water below it to reach the water below it is in the

Image ID: 461505235
Actual Captions:
1. a man repels down a cliff over water .
2. a mountain climber hangs from a cliff above the ocean .
3. a person descends a rope from a cliff into the ocean .
4. a person is climbing a cliff wall , over a rocky shore , using a rope .
5. the man is climbing up the rock .
Predicted Caption: startseq rock climbing the crag the mountain below the mountain is climbing the mountain below is hanging off the side of the mountain below the mountain is standing on the side below the mountain is climbing the mountain below

Image ID: 462080147
Actual Captions:
1. a man holding a bottle of wine with a box on his head
2. a man holding a wine bottle and wearing a box on his head is standing next to a man wearing a black hoodie .
3. one man wearing a black hoodie sweatshirt and another wearing a box over his head
4. one person is wearing a box on their head and holding a bottle while another man is standing next to him .
5. two men , one with a box on his head holding a bottle
Predicted Caption: startseq ice ice stand in a city park while a woman in a black jacket is standing in a store while a woman in a black jacket and blue shirt is standing in front of a woman in a

Image ID: 462198798
Actual Captions:
1. a big , black dog is walking along the water 's edge .
2. a black dog and its reflection are seen near a pond ringed by dry foliage .
3. a black dog is walking beside water in the woods .
4. a black dog walks along a marsh 's edge .
5. a dog is walking near a body of water .
Predicted Caption: startseq two dogs run through a river with a lake in the background and two dogs in the water is walking through the water and two dogs in the background and two dogs walking through the water by a

Image ID: 462288558
Actual Captions:
1. a pitbull dog is biting another dog on the face .
2. a tan dog opens his mouth to bite another tan dog .
3. one dog is trying to bite another .
4. one tag dog biting another tan dog while laying on a bed .
5. two brown dogs playing with each other , one has his mouth open biting the other dog .
Predicted Caption: startseq light light brown dog laying on face leg in face face with face leg in mouth and light orange outfit in face embrace in face embrace in the face of hands in the face of hands in the

Image ID: 463786229
Actual Captions:
1. a bee clings to a yellow flower .
2. a bee on top of a flower
3. a bee sits on a flower .
4. a small bee landed on a bunch of yellow flowers
5. beautiful blue sky and yellow flowers .
Predicted Caption: startseq flying flight of a rocky beach surrounded by trees in the background of trees and a parachute with a cloud of pine him in the background watching the pine distance in the background is carrying a large tree

Image ID: 463875230
Actual Captions:
1. a girl wearing pink swings on a swing .
2. a little girl is swinging high above a wooden fence on the swing .
3. a young girl in a pick shirt swinging up in the air on a swing set
4. the girl is on a swing .
5. the little girl played on the swing .
Predicted Caption: startseq extreme extreme extreme extreme extreme extreme extreme extreme extreme extreme extreme extreme extreme extreme long bike jump on a ramp with graffiti below terrain below them in the background and water below him on a roof competition one

Image ID: 463978865
Actual Captions:
1. a man sitting on the left near a man walking along the side of a street with colorful buildings .
2. a man walking by a sitting man on the street .
3. a man with dreadlocks and a backpack walks down the sidewalk with colorful buildings in the background .
4. a white man with dreadlocks walks down the sidewalk .
5. two boys are on the sidewalk as cars pass by on the road .
Predicted Caption: startseq traffic mural to traffic in the city street with lots of people in the center center looks to the left of the man in the blue shirt is crossing the street with a crowd in the center pouring

Image ID: 464116251
Actual Captions:
1. a black , brown , and white dog jumping over a pile of logs with trees in the background .
2. a dog is jumping over some logs .
3. a dog jumps over a pile of logs .
4. a dog jumps over a pile of wood .
5. a large dog is leaping over some logs in a woodland clearing .
Predicted Caption: startseq dog and a dog playing in a field with a large ball in the background watching the background of people fly down to the ground and a dog is sitting on its hind legs and a dog is

Image ID: 464251704
Actual Captions:
1. a girl in a pink top is swinging with her hair flying everywhere .
2. a girl is swinging .
3. a girl is swinging and looking down with her hair flying .
4. a girl 's hair streams behind her as she swings
5. a girl with long hair flying in the breeze while she swings .
Predicted Caption: startseq photograph of a tree with a tree in the background behind him flies through the air and a tree in the background behind him flies through the air in front of a tree with a tree in the

Image ID: 464506846
Actual Captions:
1. a black dog is running across a grassy field in front of some bushes .
2. a dog in a grassy park jumping and playing .
3. a dog with a muzzle on .
4. a muzzled greyhound leaps over grassy ground .
5. the black dog leaps into the air in the grass .
Predicted Caption: startseq large dog leaps in the air to catch a toy in the grass to another dog in the background in a field of dry grass in the background and weeds and weeds in the background in the background

Image ID: 464527562
Actual Captions:
1. a brown dog has a purple disc .
2. a brown dog has its eyes closed and a purple frisbee in its mouth .
3. the brown and black dog is holding a pink disc on a green yard .
4. the dog returns the play toy to its master .
5. this is a dog holding a frisbee .
Predicted Caption: startseq dog playing with blue toy on grass 's grass bottle bottle in mouth area in the background with mouth open mouth open mouth open open mouth open open mouth open mouth open mouth open mouth open mouth open

Image ID: 465859490
Actual Captions:
1. a group of people are listening to a man with a moustache speak into a microphone .
2. a lady with brown hair sitting at a table while someone speaks on a microphone in the background .
3. a man holds a microphone and speaks as a group of seated people watch and one woman looks down .
4. a woman at a table looking down .
5. people sit a tables while a man speaks with a microphone .
Predicted Caption: startseq people are standing in a busy street with people in the background are standing in front of them with a crowd of people in the background are standing in front of them with a crowd of people in

Image ID: 465994762
Actual Captions:
1. a brown dog jumps over a chain .
2. a dog jumps over a chain .
3. a dog leaping over a chain .
4. a greyhound jumps over a chain .
5. brown dog leaps over a chain suspended over a gravel road .
Predicted Caption: startseq puppies playing in a wooded area with a rope in the background and a stone bottle in the background and a rope in the background is pulling a rope rope in the background and a rope in the

Image ID: 466176275
Actual Captions:
1. a grey " labradoodle " jumps over another large dog .
2. one grey puddle jumping in the air in front of another tan dog
3. two dogs are chasing each other in a yard .
4. two dogs playing in grass .
5. two dogs , the gray poodle high in the air , play on the grass .
Predicted Caption: startseq light colored dog running across grass with a toy in its mouth in the background and another dog in the background and a bunch of colored dogs running past each other in the grass and one looks to
```

## Training with Epoch 50  

ဒီတခါတော့ eopch ကို 50 ထိ တိုးပြီး training လုပ်ကြည့်မယ်။  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ cp ./model_20ep/features.pkl ./model_50ep/
```

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 ./image_captioning.py --train --epoch 50 --batch_size 32 --data_dir ./data/ --model_dir ./model_50ep --dropout_rate 0.3 | tee 50ep.log
2025-06-21 13:42:55.763536: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:42:55.763558: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 13:42:57.291551: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 13:42:57.291709: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:42:57.291748: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:42:57.291778: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:42:57.291809: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:42:57.312428: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:42:57.312480: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 13:42:57.312487: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 13:42:57.312694: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Training model for 50 epochs with:
- LSTM units: 256
- Dropout rate: 0.3
- Learning rate: 0.001
- Batch size: 32
227/227 [==============================] - 157s 684ms/step - loss: 5.1626
227/227 [==============================] - 152s 671ms/step - loss: 3.8702
227/227 [==============================] - 151s 667ms/step - loss: 3.4149
227/227 [==============================] - 151s 663ms/step - loss: 3.1379
227/227 [==============================] - 129s 566ms/step - loss: 2.9328
227/227 [==============================] - 120s 530ms/step - loss: 2.7866
227/227 [==============================] - 126s 554ms/step - loss: 2.6698
227/227 [==============================] - 148s 651ms/step - loss: 2.5654
227/227 [==============================] - 150s 659ms/step - loss: 2.4785
227/227 [==============================] - 150s 660ms/step - loss: 2.4059
227/227 [==============================] - 149s 655ms/step - loss: 2.3383
227/227 [==============================] - 148s 653ms/step - loss: 2.2813
227/227 [==============================] - 149s 654ms/step - loss: 2.2288
227/227 [==============================] - 148s 650ms/step - loss: 2.1899
227/227 [==============================] - 150s 658ms/step - loss: 2.1559
227/227 [==============================] - 144s 632ms/step - loss: 2.1103
227/227 [==============================] - 148s 651ms/step - loss: 2.0665
227/227 [==============================] - 148s 652ms/step - loss: 2.0241
227/227 [==============================] - 148s 650ms/step - loss: 1.9904
227/227 [==============================] - 149s 655ms/step - loss: 1.9568
227/227 [==============================] - 147s 649ms/step - loss: 1.9289
227/227 [==============================] - 148s 651ms/step - loss: 1.9023
227/227 [==============================] - 148s 649ms/step - loss: 1.8803
227/227 [==============================] - 150s 658ms/step - loss: 1.8536
227/227 [==============================] - 149s 657ms/step - loss: 1.8309
227/227 [==============================] - 149s 655ms/step - loss: 1.8055
227/227 [==============================] - 148s 654ms/step - loss: 1.7823
227/227 [==============================] - 130s 573ms/step - loss: 1.7616
227/227 [==============================] - 120s 528ms/step - loss: 1.7436
227/227 [==============================] - 125s 551ms/step - loss: 1.7259
227/227 [==============================] - 148s 650ms/step - loss: 1.7072
227/227 [==============================] - 149s 654ms/step - loss: 1.6902
227/227 [==============================] - 149s 657ms/step - loss: 1.6690
227/227 [==============================] - 148s 650ms/step - loss: 1.6527
227/227 [==============================] - 148s 653ms/step - loss: 1.6357
227/227 [==============================] - 148s 651ms/step - loss: 1.6219
227/227 [==============================] - 148s 653ms/step - loss: 1.6051
227/227 [==============================] - 149s 655ms/step - loss: 1.5928
227/227 [==============================] - 147s 648ms/step - loss: 1.5769
227/227 [==============================] - 148s 652ms/step - loss: 1.5641
227/227 [==============================] - 147s 649ms/step - loss: 1.5528
227/227 [==============================] - 136s 600ms/step - loss: 1.5402
227/227 [==============================] - 147s 649ms/step - loss: 1.5259
227/227 [==============================] - 147s 649ms/step - loss: 1.5109
227/227 [==============================] - 148s 651ms/step - loss: 1.5027
227/227 [==============================] - 148s 651ms/step - loss: 1.4913
227/227 [==============================] - 148s 653ms/step - loss: 1.4783
227/227 [==============================] - 148s 652ms/step - loss: 1.4656
227/227 [==============================] - 148s 654ms/step - loss: 1.4594
227/227 [==============================] - 146s 641ms/step - loss: 1.4487
Model saved to ./model_50ep/best_model.h5
Tokenizer saved to ./model_50ep/tokenizer.pkl

real    121m25.072s
user    1538m57.058s
sys     69m38.379s
```

## Testing/Evaluation with 50 Epoch Model  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ ls ./model_50ep/
best_model.h5  features.pkl  tokenizer.pkl
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$
```

```
time python3.8 ./image_captioning.py --evaluate --model_dir ./model_50ep | tee evaluate_50ep.result.log
```

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 ./image_captioning.py --evaluate --model_dir ./model_50ep | tee evaluate_50ep.result.log
2025-06-21 16:11:48.412343: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 16:11:48.412366: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 16:11:50.080435: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 16:11:50.080654: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 16:11:50.080715: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 16:11:50.080763: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 16:11:50.080808: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 16:11:50.103059: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 16:11:50.103111: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 16:11:50.103118: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 16:11:50.103323: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Model loaded from ./model_50ep/best_model.h5
Evaluating: 100%|████████████████████████████████████████████████████████████████████████████████████| 810/810 [18:35<00:00,  1.38s/it]

Evaluation Metrics:
BLEU-1: 0.2167
BLEU-2: 0.1182
BLEU-3: 0.0633
BLEU-4: 0.0321
chrF++: 0.2046
Evaluation results saved to ./model_50ep/evaluation_results.pkl (binary) and ./model_50ep/evaluation_results.txt (text)

real    18m39.642s
user    20m37.264s
sys     1m19.243s

```

## Learning on Translation with 50 epochs

```
Evaluation Metrics:
BLEU-1: 0.2167
BLEU-2: 0.1182
BLEU-3: 0.0633
BLEU-4: 0.0321
chrF++: 0.2046

Sample Results:

Image ID: 436015762
Actual Captions:
1. a man prepares to enter the red building .
2. a man walking around the corner of a red building .
3. a man walks past a red building with a fake rocket attached to it .
4. a man walks under a building with a large rocket shaped sculpture .
5. a person walking by a red building with a jet on top of it .
Predicted Caption: startseq shadow are walking on a red railing while seen from the left of the rainbow barriers in the background behind him and a blue building in the background cars behind him and a blue pole on the right

Image ID: 436393371
Actual Captions:
1. a brown doberman is outside with a stick in its mouth .
2. a brown dog shows his teeth .
3. a dog bites a stick .
4. a dog is biting a twig .
5. a dog with sharp teeth is chewing on a stick outside .
Predicted Caption: startseq brown dog digging in the water with a stick in its mouth and a brown dog sits next to him has paws in the air next to him has paper out of him in the air next to

Image ID: 436608339
Actual Captions:
1. a couple posing in front of a picture wall
2. an adult couple pose by a cardboard cut out for a movie .
3. an asian couple are standing by a fantasy poster .
4. an asian couple stands near a wax figure .
5. one person in a brown suit with his arm around another in a hat by a wall .
Predicted Caption: startseq men in a line band are making faces gestures on a wall covered with computer walls of soda in their hands and a casual city stand behind them and one is in the background wearing open hair and

Image ID: 437054333
Actual Captions:
1. a bus filled with passengers in chicago at night .
2. a bus full of people waiting at a stop .
3. people are sitting on a bus .
4. people in a bus which is heading to 84 peterson .
5. there are people sitting on a bus that is labeled 84 peterson .
Predicted Caption: startseq out of booths at a restaurant seen from behind a window doors to a window display while a glass doors and a big neon colored circle to the right of the back to the right window behind them

Image ID: 437404867
Actual Captions:
1. a woman is sitting on a sidewalk with a cellphone at her ear .
2. a woman rests on the curb of a city street while talking on her cellphone .
3. a woman sits on the curb while talking on her cellphone .
4. a woman sits on the edge of a sidewalk with a garbage bin beside her
5. woman sits on the curb talking on a cellphone .
Predicted Caption: startseq filled structure at marketplace at birthday dark building full of soda in alley watch a man in a red shirt is amid winston beer while he jumped in a dark blue bag of a wave at night at

Image ID: 437527058
Actual Captions:
1. a caravan of snowmobile travel through the snow .
2. a pair of people in heavy winter jackets rides through the snow on a snowmobile .
3. people riding something in the snow .
4. person on a polaris ski mobile in the snow .
5. the man wearing a blue helmet is riding a polaris .
Predicted Caption: startseq children sit on the snow in the snow with head out of the frame in the head behind them with a red hat and a red backpack behind them and red and red snowmobiles to the side of

Image ID: 437917001
Actual Captions:
1. a dark colored man is laying on newspapers by a metal railing with his shoes off .
2. a homeless man is lying on the ground with his stuff strewn around .
3. a homeless man is sleeping outside at the top of a staircase .
4. an man is sleeping on top of his clothes on concrete stairs .
5. man sleeping on the street .
Predicted Caption: startseq blue hat with blue jacket and blue hat climbing paper while hands in blue shirt and shirt behind metal look out in park with bags in background of metal metal bags in the background metal wall behind him

Image ID: 438639005
Actual Captions:
1. a boy in red and a girl pink are walking through a low cut field .
2. the little boy and little girl are walking side by side .
3. two small children walk away in a field .
4. two small children walking in a field .
5. two young children are walking across an open field .
Predicted Caption: startseq girl in a red shirt kicks a red stick in a field of brown grass while others chickens diving to catch him while a girl in a pink shirt watches the ball in the air with a smile

Image ID: 439037721
Actual Captions:
1. two men sitting on the bank of a lake with an ice chest .
2. two people having a picnic by a lake .
3. two people having a picnic by the shore .
4. two people sitting on grass in front of a lake looking at the sky .
5. two people with hats looking at a lake while sitting on a yellow-grassed hill .
Predicted Caption: startseq red atv is flying through the air over a rock in front of a red barrel while a person stands on the ground looking at it and the sun fishing pole behind them in the background behind it

Image ID: 439049388
Actual Captions:
1. people , possibly fishermen , with their boats in shadow on shore at an orangesunset
2. a man in an orange vest is standing next to a yellow canoe .
3. people tend canoes at the edge of a body of water during a dimly lit time of day .
4. the men are getting their kayaks secured on the beach for the night .
5. two men standing on the shore beside their kayaks at dusk .
Predicted Caption: startseq cyclist performing on a beach with people fly by it and it runs alongside the ocean in the background like a lake behind it below the sun bleachers like the background watch the sun below the background cyclist

Image ID: 439492931
Actual Captions:
1. a cluster of four brown dogs play in a field of brown grass .
2. four dogs are together in the field of dry grass .
3. four dogs in a grassy area .
4. four medium-sized dogs wrestle with each other on a grass field .
5. four small dogs play outside .
Predicted Caption: startseq small brown dog chasing a small brown dog while a small brown dog in the background in the background is standing in front of a small dog with small red and white dog in mouth while standing by

Image ID: 439569646
Actual Captions:
1. a girl is hiding behind a painted wooden structure inside a building .
2. a little girl with a red dress facing a panel with her back to the camera .
3. a young blonde girl wearing a red dress kneeling on a red carpet .
4. a young girl faces a white and black wall in a red-carpeted room .
5. girl kneeling on a red carpet .
Predicted Caption: startseq smiles with two girls in pink and pink are standing in front of a red door with a pink blanket on its back with a color in the background wearing red clothes and red skirt and pink boots

Image ID: 439916996
Actual Captions:
1. brown dogs and a woman in a yard
2. a brown dog persues a frisbee across the grass as the thrower watches .
3. a woman in a blue jacket watches as her two brown dogs play with a red ball in a grassy yard .
4. a woman throws a frisbee for her two brown dogs to chase .
5. a woman watches a brown dog run away from a house across the grass .
Predicted Caption: startseq golden dog in snow covered with orange dog stands next to which is golden dog that makes food out in front of him spread spread its left hand for help by two other people outside on a path

Image ID: 440184957
Actual Captions:
1. a clown shares cut-out pictures of children .
2. a dirty looking clown holding up two paper cut outs of children with blond hair
3. a man wearing a balloon hat and a grassy shirt holds up two large paper dolls .
4. a man wearing a balloon hat holds up colored cut-out drawings of two men .
5. the man wears balloons on his head and holds paper people .
Predicted Caption: startseq kids playing on a playground outside with a yellow stick in front of them holding orange flowers in their hands and their playhouse it open and hand the other in the background behind them holding a stick in

Image ID: 440190907
Actual Captions:
1. a group of people walk through a shopping mall .
2. many people walk through the store .
3. people browse in a store .
4. people strolling through an indoor market .
5. the shoppers are walking in a store .
Predicted Caption: startseq lights make lights out of a restaurant lit soda hanging out on a brightly colored outdoor outdoor restaurant with lights hanging out of it hanging out of a hanging hanging out of the back of it past it

Image ID: 440737340
Actual Captions:
1. a black man with a red mask is carrying a box .
2. a man in a domino mask carries an amplifier up a hill .
3. a man with a mask carrying a black speaker
4. a masked man in bright clothing carrying a large box .
5. black man lifting black box is watched by black dog .
Predicted Caption: startseq horse in a park with flowers stretched out to the right of it and a man in the background walk around it boots and the backs of a tree in the background below a tree in the background

Image ID: 441212506
Actual Captions:
1. the black dog runs with a ball with two smaller dogs behind it .
2. three dogs playing in a field , one with a ball in its mouth .
3. three dogs race towards the viewer over a lawn .
4. three dogs running in grass , one carrying a tennis ball in mouth .
5. two small dogs follow a larger dog with a tennis ball
Predicted Caption: startseq two dogs are playing in a field of yellow flowers in the grass and a person watches them in the distance with their mouths open open mouth of the background of other dogs in the background in the

Image ID: 44129946
Actual Captions:
1. a couple watches a boat against a skyline .
2. a man and woman sit on a bench , watching a boat go by .
3. the sun is setting while a man and woman watch a boat go by .
4. two people sit on a bench and watch a boat on the water .
5. two people watching a boat sail past .
Predicted Caption: startseq sitting in a body of water with a lake in the background and two people in the lake fishing in the distance behind her sky fishing male fishing male in the distance on the beach behind them in

Image ID: 441398149
Actual Captions:
1. a female jogger wearing red .
2. a girl with headphones is running next to some street signs .
3. a woman in a red outfit is jogging next to several street signs .
4. a woman jogging across an intersection .
5. the lady in red shorts jogs near a stop sign while listening to music .
Predicted Caption: startseq kids playing in a playground structure with a playground and a painted table in the background and gold shirts and one in the background in the background behind them also with a playground painted top behind them holding

Image ID: 441817653
Actual Captions:
1. a bearded man wearing a denim jacket and a hat sits on a park bench
2. a bearded man wearing a denim jacket sits on a bench .
3. a man with a bushy beard and a baseball cap sits on a park bench .
4. an old man with a long beard and jean jacket sits on a park bench .
5. an old man with a long white beard , glasses , and a hat is sitting on a park bench .
Predicted Caption: startseq of time in for the back the elderly woman wearing a white hat and a white hat is wearing a baseball cap and wearing a white hat and wearing a white hat and wearing a white hat and

Image ID: 441921713
Actual Captions:
1. a bird lands on a mans glove .
2. a man holds a bird .
3. a man holds a falcon on his arm .
4. gloved man holding a bird of prey .
5. the man is wearing gloves and holding a hawk in his hands .
Predicted Caption: startseq rows of tent cars and talk to a fire with traffic in the background behind them behind them and flowers moves out in the background behind them advertising gloves and cars to the side behind them the man

Image ID: 442220883
Actual Captions:
1. a brown dog has a white toy in its mouth .
2. a dog holding a white stuffed animal .
3. a tan dog hangong on to a white plushie toy .
4. a yellow dog is chewing on a white stuffed toy .
5. the dog is holding a stuffed toy in his mouth .
Predicted Caption: startseq dog with green eyes with a piece of fabric hanging over it and eyes it with bottle on it and they are eating with sticks on it and eyes behind it over it and bottle of water with

Image ID: 442594271
Actual Captions:
1. a bunch of people at the beach .
2. people are enjoying a sunny day on a sandy beach by the ocean .
3. people are on the beach and there is a kite in the air .
4. people on the beach and a kite in the sky .
5. sandy beach , people walking , laying , sitting , a kite is flying .
Predicted Caption: startseq people are walking along a beach near the ocean fishing and bright boats on the beach and the ocean passes float by the beach and the ocean on the beach behind them in the ocean and the ocean

Image ID: 442918418
Actual Captions:
1. a brown dog is jumping over a fallen tree in the woods .
2. a small tan dog jumps over a small log .
3. tan colored dog jumping over a branch in the forest .
4. the dog leaps over the log in the forest .
5. the white dog is jumping over a fallen tree .
Predicted Caption: startseq which a dog jumps over a log in a wooded area with a white suv tied in his mouth and a black tied on his chest tries to eat him out of it his tongue open his tongue

Image ID: 443430496
Actual Captions:
1. a brown dog swimming in murky water .
2. a brown dog swims in the murky water .
3. a dog with yellow fur swims , neck deep , in water .
4. a golden retreiver swimming in the water .
5. a yellow dog is swimming in the water .
Predicted Caption: startseq dog with stick in mouth while wading in water by bushes in water by water by water by lake water lake side the sun lake the sunny lake waters dog takes a stick out of the water as

Image ID: 443885436
Actual Captions:
1. a tan curly haired dog jumps in the snow with a stick in its mouth .
2. a white dog catches a stick in the snow .
3. a white dog holds a stick in its mouth while it runs through snow .
4. a white dog jumps in the snow .
5. a white dog with light brown markings has a stick in his mouth and his paws in the snow .
Predicted Caption: startseq runs through snow covered with white snow covered landscape in background runs in the snow with snow covered ground in the background bushes in background the background it runs to the snow covered stream with something in the

Image ID: 444047125
Actual Captions:
1. a person hiking at the foot of snowcapped mountains .
2. a person walks in the valley between tall mountains .
3. a person with a backpack and walking stick , walking towards the mountains in the valley below .
4. people with backpacks hiking in the mountains .
5. three people walk through a valley towards snowy mountains .
Predicted Caption: startseq on a grassy grassy forest with mountains and mountains and mountains in the background hikers near the mountains and mountains watch the view of a man in the red top is riding a show on a bike in

Image ID: 444057017
Actual Captions:
1. a little girl gets her picture taken while on the merry-go-round .
2. a little girl in pink clothes holding yellow rods .
3. a little girl on a piece of playground equipment
4. a little girl sitting on a playground ride .
5. a young girl looks up as she rides on a merry-go-round .
Predicted Caption: startseq babies are playing on a playground set with a blue and blue playground set for their legs in the background and a blue playhouse is behind them holding a piece of colored poles behind them one has his

Image ID: 444481722
Actual Captions:
1. a dark skinned man walks by a woman talking on a cellphone .
2. a male walking and a female talking on the phone beside the concrete building .
3. people stand outside near a concrete wall and a window .
4. two people standing on the sidewalk .
5. two women , one carrying a purse and papers , are standing on a sidewalk .
Predicted Caption: startseq spray of water spray and big light colored stands on the sidewalk in front of them and bright clothes in the back of a staircase and spray equipment in the background with spray clothes in the background and

Image ID: 444803340
Actual Captions:
1. a guy and a girl , both wearing white shirts and jeans , stand under a flowering tree .
2. a man and a woman are talking in a park
3. a man and woman standing underneath the tree are talking .
4. a man in a white shirt is standing in the grass showing something to a woman in a white shirt .
5. a young couple both wearing white shirts and blue jeans standing in a light misty rain
Predicted Caption: startseq traffic has traffic stands by her woman wearing red and white boots holding flowers in hand and reads it and a bland and white dog in the background in the background holding stick in background behind it and

Image ID: 444845904
Actual Captions:
1. a man in a yellow helmet climbs a cliff face , snow behind him .
2. a man is climbing up a wall with a rope
3. a man leans back while climbing a mountain tethered to a rope .
4. he is rock climbing .
5. man with helmet rock climbing in a snowy area .
Predicted Caption: startseq climbers are hiking up a snowy hill on a sunny day near a building with snow covered mountains behind them behind them and snow poles behind him and a blue building behind them and a blue building behind

Image ID: 444872454
Actual Captions:
1. a group of students dressed in sweatshirts and jackets head towards the right .
2. a group of students walking on campus , some carrying books .
3. a group of students walk together .
4. a group of young people are walking through a park under blossoming trees .
5. several young women walk near blossoming cherry trees .
Predicted Caption: startseq wearing a large vest and a female poses with others walk by her and a lot of men and woman in black are posing for a photo in front of a tree and a lot of people and

Image ID: 444881000
Actual Captions:
1. a group of college students walk in nice weather .
2. a group of people walk in the park , while some talk on phones .
3. a group of students are walking through the campus .
4. a group of young people walking with two talking on cellphones .
5. several young people walking casually around
Predicted Caption: startseq three people are standing in a park and flowers of their hands in the middle of their flowers and flowers flowers in their hands and flowers to their faces to make a toast in the middle of a

Image ID: 445148321
Actual Captions:
1. a person in the distance hikes among hoodoos with stars visible in the sky .
2. a person standing on a ridge in the desert .
3. interesting rock formations in the desert landscape , with stars above .
4. the night sky in the desert .
5. there is a person standing a mountain that has some interesting shapes .
Predicted Caption: startseq climbers sit on top of a rock covered with a cloudy sky sky behind them below them the sun ridge behind them a mountain scenery with a distant view in the background behind him holds a rock in

Image ID: 445655284
Actual Captions:
1. a black and brown dog walks through the snow near a building .
2. a black dog , running in the snow .
3. a black dog running in the snow by some trees .
4. a large black and tan dog is running across the snow in a wooded area .
5. the black and brown dog is running through the snow .
Predicted Caption: startseq walking in snow of snow covered dog with black dog digging in snow covered ground with snow covered snow in background snow snow pile them in snow snow field and snow covered snow covered ground in background snow

Image ID: 445861800
Actual Captions:
1. three men walking on a sidewalk in a city .
2. three people are walking down the street with cars and buildings in the background .
3. three people stand along a main road .
4. three people walking on a sidewalk with 3 light colored cars in the background .
5. three people wearing winter clothes standing on the sidewalk near a street
Predicted Caption: startseq on a street with many people walking down the road behind them the man in the green jacket is walking on the street with the man in the green jacket and green jacket walks down the street with

Image ID: 446138054
Actual Captions:
1. a man in an orange hat jumping .
2. a man jumps in the middle of a rocky desert .
3. a man wearing a white shirt and an orange shirt jumped into the air .
4. man in khaki pants does elaborate kick in desert
5. man jumping with a rock formation in background .
Predicted Caption: startseq of people carry a high balloon of pile of several mounds of large rocks and a man in a black coat leaping into the air with a cloudy logo and the blue sky behind him on the side

Image ID: 446286714
Actual Captions:
1. an elderly man is sitting on a bench .
2. an older man wearing a brown coat siting on a bench .
3. an old man in a coat and hat sitting on a park bench .
4. old man in tan jacket and black cap sitting on bench
5. the older man with the shopping bag and cane is sitting on a bench .
Predicted Caption: startseq horse with a flower painted on it is being watched by a man in a green shirt and cap on the ground and both children are painted nearby they watch the other people who is wearing a black

Image ID: 446291803
Actual Captions:
1. these woman are watching people play tennis from a bench .
2. two individuals watch a tennis match .
3. two people sit on a park bench while watching a neighborhood tennis match .
4. two people with red scarves on their heads are watching tennis .
5. two women sitting on a bench in front of a tennis court near a building complex .
Predicted Caption: startseq two people sit on bleachers in a public park with their drinks from them the camera behind them the children in the background on the deck of it and a poster of a bike stand in front of

Image ID: 446514680
Actual Captions:
1. two brown dogs are fighting and they are both wearing red .
2. two brown dogs rough house outside .
3. two brown dogs wearing red collars look at each other while running along a dirt field .
4. two dogs play together .
5. two large brown short haired dogs with collars play chase in a field .
Predicted Caption: startseq brown dog playing with a toy in a field of clear leaves with a man in the background behind him behind him behind him of brown dog in foreground covered brush with distant camera behind them of other

Image ID: 447111935
Actual Captions:
1. the two greyhound dogs wearing sweaters are playing in the grass .
2. two dogs play in the grass .
3. two dogs wearing shirts play in the green grass .
4. two dogs wearing sweaters play in a field .
5. two dogs wearing sweaters play in the grass .
Predicted Caption: startseq dog with red collar and pink pants jumping on grass with legs in mouth and trees in background area scene in background of leaves behind him attached to leaves in the background a black dog jumps in air

Image ID: 447722389
Actual Captions:
1. a brown and white dog is jumping high and catching a blue ball .
2. a dog is jumping and catching a small , blue ball in a park surrounded by two other dogs .
3. a dog jumps and catches a blue ball in his mouth .
4. a dog jumps in the air to catch a blue ball .
5. three dogs run on grass , one leaps to catch blue ball .
Predicted Caption: startseq dog with black collar and leash jumping over a stick in a park like setting setting setting in mouth and trees in the background in mouth and trees behind him with white rope in the background in the

Image ID: 447733067
Actual Captions:
1. a girl in a skimpy bikini outfit walks and carries a helmet .
2. a scantily clad girl , in a helmet , walks away from the camera , down a busy sidewalk .
3. a woman wearing a helmet , tall boots , and short shorts walks down the street .
4. girl in bikini bottoms , boots and a helmet walking away at a street fair .
5. the woman in the purple bikini and pink top is wearing a safety helmet .
Predicted Caption: startseq woman in green shirt holding a drink poses on a cellphone with seven ornamental balls in the background behind her ornamental cloth food in ornamental clothes and ornamental boots in ornamental clothes and gold tie on the ground

Image ID: 447800028
Actual Captions:
1. a black dog playing with a purple toy in the snow .
2. a black dog runs through the snow carrying a blue toy .
3. a dog plays in the snow .
4. dog running with a purple toy in the snowy field .
5. the black and brown dog carries a purple toy in the snow .
Predicted Caption: startseq running in the snow over snow covered ground with a black dog running between them runs by snow covered ground in snow covered snow covered landscape in forest snow covered forest with orange dog runs between them in

Image ID: 448252603
Actual Captions:
1. a boy pointing in a direction on a dirt road .
2. a boy with a backpack sits on a trail and points .
3. a man points his finger to the path ahead as he sits on the dirt path .
4. a man with a backpack is sitting in a dirt road and pointing toward the horizon .
5. a young man sitting in the middle of a dirt road pointing up the road .
Predicted Caption: startseq brown and white dog walking down a dirt road in a rural forest with a long forest in the foreground behind him behind him behind a brown hat is running on a road with a small child on

Image ID: 448257345
Actual Captions:
1. a dog is staring at the food in the plate of a person eating .
2. a person holding a dog while they eat .
3. a person is eating a plate of pasta with a black and brown dog on his or her lap .
4. a person is eating pasta , while a dog is watching .
5. someone in a blue and white striped sweater is eating and the dog next to them is interested in their food .
Predicted Caption: startseq colors is sticking around something in his mouth and eats with a dog in front of it and sunny patches showing legs table with bushes in his mouth showing a large leash of it and a large dog

Image ID: 44856031
Actual Captions:
1. a brown dog is sprayed with water .
2. a dog is being squirted with water in the face outdoors .
3. a dog stands on his hind feet and catches a stream of water .
4. a jug is jumping up it is being squirted with a jet of water .
5. a tan , male dog is jumping up to get a drink of water from a spraying bottle .
Predicted Caption: startseq brown dog catching a dish in his mouth in front of a brick wall with adult on the ground behind him behind them both balls in background behind it and blue flowers in background behind him in the

Image ID: 448590900
Actual Captions:
1. a brown dog is sniffing around green grass on a hill .
2. a dog is digging a field .
3. a dog stands in a large , grassy field .
4. a dog walks alone in a field .
5. a dog with a red harness tracks a scent in a field .
Predicted Caption: startseq brown and brown dog running through a field of flowers and flowers in the background behind a brown house in the distance observes the distance of a field of orange flowers and flowers flowers in the distance behind

Image ID: 448658518
Actual Captions:
1. a large man dressed in black on a street corner by a red brick building .
2. a man dressed in black is waiting at a crosswalk .
3. a man dressed in black stands at a street corner near a crossing light .
4. a man stands at a traffic light , waiting to cross the street .
5. man in black waits at crossing signal near large brick building .
Predicted Caption: startseq girl in green shirt swinging on a swing swing above a post with a green light blue background nearby buildings in the background behind it bleachers behind it and a building light one guitar to cross the other

Image ID: 448916362
Actual Captions:
1. a dog is running through a field with its tongue hanging out .
2. a dog runs with his tongue hanging out .
3. a dog with its mouth open is running .
4. brown and cream dog with tongue out
5. the white and black dog runs on the field with his tongue hanging out .
Predicted Caption: startseq dog with tongue out close up with orange poles in mouth decorated with print collar in mouth filled with orange vest with red toy in background in mouth and collar turned to look behind it and another dog

Image ID: 449287870
Actual Captions:
1. a female toddler wearing a pink shirt is playing on a playground .
2. a little girl in pink and purple stands on a playground .
3. a very young girl is walking on a playground .
4. the little girl is playing at the playground .
5. young child in pink top and purple pants clutching a turquoise guard rail .
Predicted Caption: startseq playground little girl in girl wearing playground shirt and blue shirt smiling at the camera at playground equipment smiling while another boy looks on at the playground equipment at the park seat on the playground equipment at the

Image ID: 449352117
Actual Captions:
1. a brown and black puppy stands by a camera .
2. a dog chews on the strap of a camera case .
3. a dog gnaws on the strap of a camera .
4. a small dog chewing on a black strap .
5. a small dog is standing behind a camera .
Predicted Caption: startseq color sitting on a bench with a purple blanket on her face and purple pants 's arm and a purple collar sits behind him 's nose and watch it boots behind him while both fingers of it sits

Image ID: 450596617
Actual Captions:
1. man and woman walking near the ocean .
2. two people are walking alongside a decorative railing while wearing winter gear .
3. two people are walking by the ocean .
4. two people in coats walking next to a fence .
5. two people walk together on a cold day .
Predicted Caption: startseq line of old fence at a fence in a city park with black handrail on the ground behind them looks up the put to the left behind her purse at the water behind her first purse just her

Image ID: 451081733
Actual Captions:
1. a man on the beach in jeans looking at his camera .
2. a shirtless guy turned around videotaping something at the beach .
3. barechested man filming at the beach .
4. the man is wearing rolled up blue jeans and holding a video camera on a stone beach .
5. the shirtless man used his camera while sitting on the rocky beach .
Predicted Caption: startseq wrestler in black shorts with black and black top with a backdrop of black horse on pavement in front of ring behind ring of ring behind two other crowds men in black outfits with black vests standing on

Image ID: 451326127
Actual Captions:
1. a dog jumping over a fallen tree in the forest
2. a dog leaps over a tree fallen in the forest .
3. a large dog jumping over a fallen tree in the forest .
4. large brown dog jumps over a low tree trunk in a wooded area .
5. the german shepherd is jumping over a fallen tree .
Predicted Caption: startseq bird walks in a stream surrounded by fallen rocks and trees and a house are covered in background in the distance nearby trees and trees behind them in the distance behind them holding a fallen tree in the

Image ID: 451597318
Actual Captions:
1. a brown dog leaps up to catch an orange toy .
2. a dog catches a disk in the air .
3. a dog is jumping in the air to catch an orange frisbee .
4. a dog leaping to catch a frisbee in the yard .
5. brown dog leaping up with orange disc in mouth with blue and yellow toy boat in background .
Predicted Caption: startseq balls in the yard with a man in a blue shirt and blue shorts on a blue leash to create a trick to him several others in front of him covered ground in front of him covered ground

Image ID: 452345346
Actual Captions:
1. a brown and white dog chews on a tire .
2. a brown and white dog with pointy ears stands outside in sand holding a small tire in its mouth .
3. a brown , black and white dog holding a tire in its mouth while standing on sand
4. a bull terrier terrorizes an old tire in the sand .
5. a dog standing in sand , holding a tire in his mouth .
Predicted Caption: startseq of their puppies are playing on a plastic string outside of a house and a dog in the background watches them next to him and a house in the background like them with red mouths sits nearby a

Image ID: 452363869
Actual Captions:
1. a black dog chases a ball in the grass .
2. a black dog is chasing a ball on a green grass .
3. a dog and a ball on green grass and in front of trees .
4. a dog chases a ball in the grass .
5. green grass field , a black dog running after a ball .
Predicted Caption: startseq orange dog chasing after a red ball in a field of green grass in the field by a blue field of orange flowers in the background on the left with orange balls in background in the background in

Image ID: 452416075
Actual Captions:
1. a baby dressed in blue jumps outside .
2. a child is bouncing on a trampoline that is next to the house .
3. a small child jumps up on a trampoline .
4. a young boy jumping on a trampoline outside of a house .
5. the little boy with red hair jumps on the trampoline .
Predicted Caption: startseq in the air about to walk a skateboarding high down a bright orange light blue building with his feet in the air skating around a boy wearing a blue shirt and blue shorts and blue hat wearing a

Image ID: 452419961
Actual Captions:
1. the three children are in a cage .
2. three children are locked in a cage .
3. three children in a black dog kennel .
4. three small children are in a cage .
5. three well dressed blond children in a cage .
Predicted Caption: startseq her elderly woman is petting her little baby in a blue blanket with a piece of book in a blue blanket of a yellow and white blanket in the city with him in his mouth and both blanket

Image ID: 453473508
Actual Captions:
1. a brown dog is running though a river .
2. a brown dog jumping in a stoney brook .
3. a brown dog runs through shallow water .
4. a dog wading through shallow water .
5. a golden retriever splashes in the water .
Predicted Caption: startseq swim dog with brown collar bounding through water while carrying waves behind it in the background behind it holds shoulder branch in background of water in the background the lake behind it holds a large boat in the

Image ID: 453756106
Actual Captions:
1. a large , brown , fluffy dog with a small white and brown dog on a dirt surface .
2. a large dog is playing with a small dog in the dirt .
3. a small dog and a large dog play together .
4. bigg playing with little dog in dirt .
5. two dogs play with each other in the dirt .
Predicted Caption: startseq standing on leash playing with something in its mouth while walking on the sand next to a house with its leash attached to its hind legs on the ground next to a dog with a paper in its

Image ID: 454686980
Actual Captions:
1. a girl who looks upset with her arms crossed .
2. an indian woman in a black shirt stands with her arms crossed looking at two other people talking to each other .
3. a person in a red and black shirt has their arms crossed and looks at the camera .
4. a teenage girl is standing with her arms crossed in a busy street .
5. woman in dark shirt standing alone in front of a yellow car .
Predicted Caption: startseq running with other boys running in street race like green audience in green and green man in green shirt running with drink in city street in street like store game in green like orange cone from other person

Image ID: 454691853
Actual Captions:
1. a dog carries a leash in its mouth .
2. a fluffy dog carries a black leash in its mouth .
3. a large furry brown dog is walking with a leash in his mouth .
4. a yellow dog carries a black leash .
5. dog walking with his lease in his mouth .
Predicted Caption: startseq fabric look on wood wall looking at a dog with a bottle in its mouth and another dog in the background watching it walks through the woods with water in the background nearby nearby trees and bushes in

Image ID: 454709143
Actual Captions:
1. a man dressed in blue holds a sign while standing behind a couple of trees and in front of a large concrete wall with red writing on it .
2. a man holds up a cardboard sign near a wall with red graffiti .
3. a man in a black jacket is standing between two trees holding up a sign .
4. a man stands on the side of the road , holding a cardboard sign .
5. a man stands with a cardboard sign on a road
Predicted Caption: startseq barefoot man in red jacket and red jacket standing on a tree stump in the rain with water in the mouth of the water beside it and white birds overhear on the surface of frozen lake followed by

Image ID: 455611732
Actual Captions:
1. a hiker walks on rocky ground at the base of a foggy mountain .
2. a lone hiker walking on dirt with a snowy mountain background .
3. a person is hiking along rough terrain with fog and mountains in the background .
4. distant person with blue backpack hiking in rocky area , mountains in background .
5. the person is hiking .
Predicted Caption: startseq people are standing on a rock overlooking a strange building storm over a rock covered cliff with graffiti behind him and bright color mountains behind them holding them by them while waves in the background behind them nearby

Image ID: 455856615
Actual Captions:
1. a skier flies through the air .
2. ski boot gets pulled out of the ski .
3. the feet of a skier with one boot coming out of the ski and casting a shadow .
4. two boots are on two skis moving very fast .
5. two feet wearing yellow ski boots on ski
Predicted Caption: startseq make over snow covered in area of snow covered man wearing a yellow jacket rides his snowboarding over a snowy hill with a roof against a man in a blue jacket makes a jump on his board in

Image ID: 456299217
Actual Captions:
1. a girl sits outside at a large fountain .
2. a woman and two others are sitting nearby a decorative water fountain .
3. a woman sits on a wall next to a large conical fountain .
4. a young woman sits near a fountain .
5. woman in black poses near a pyramid fountain .
Predicted Caption: startseq skater leaps off a ramp on a half pipe at night with graffiti covered ground behind him buildings in the background a skateboarding building one is in the background one is skateboarding against the wall and one is

Image ID: 456512643
Actual Captions:
1. a brown dog is running through a grassy field .
2. a brown dog running through grass .
3. a dog runs in a grassy field .
4. a golden-brown dog running through a green field .
5. a tan dog is running fast through tall green grass .
Predicted Caption: startseq runs through field of dead leaves runs through field of flowers in tall grass flowers like its paws like one runs through field in field of dry flowers in field of flowers in field of flowers of flowers

Image ID: 457631171
Actual Captions:
1. a man extends his arms in front of a large rock formation .
2. a man in the desert .
3. a man poses in front of a large rock formation .
4. a man standing next to a huge rock formation .
5. a man stands next to a strange rock formation with his arms in the air .
Predicted Caption: startseq climbers on a rock climbing rocks side of a pile of rocks climb to climb a rock wall overlooking the ocean below of water nearby rocks and water beyond the rocks below the mountain below the building the

Image ID: 457875937
Actual Captions:
1. two black , brown and white dogs running in green grass with ears up on heads .
2. two dogs run through a field of grass
3. two fluffy dogs run through the grass .
4. two look-alike dogs running in the green grass .
5. two small dogs run through the grass .
Predicted Caption: startseq running through the field a dog with a stick in its mouth runs through the grass with a stick in its mouth open and a black dog in the background is running in the grass with a stick

Image ID: 457945610
Actual Captions:
1. a girl in striped swimsuit is jumping into the ocean .
2. a little girl in a striped bathing suit jumps in a large body of water .
3. a little girl in a striped bathing suit jumps in the ocean .
4. a young girl in a striped bathing suit jumping in the ocean .
5. girl jumping over wave
Predicted Caption: startseq floating floating diving into water while a man holds a stick in his mouth and waves him up the board behind him behind him in the water behind him and blue waves behind him and floating in the

Image ID: 458004873
Actual Captions:
1. a man is sitting on a bench facing another man who is standing .
2. a man sits on a bench while another man walks toward him .
3. a person sitting on tan bench and man in green shirt standing on black and grey floor .
4. this over the top photo shows two men taking a break .
5. top-down view of a man sitting on a bench inside with a standing man facing him .
Predicted Caption: startseq against art around a man in a black shirt is sitting on a bench in a park near a building with art around in the background behind it behind it behind it i the background watch the fence

Image ID: 458183774
Actual Captions:
1. a dog rolls on his back in the grass .
2. a large tan dog is rolling around on its back in a yard of grass .
3. a large , tan dog is rolling in green grass .
4. big yellow dog rolling around on the green lawn .
5. large dog rolling on its back in green grass .
Predicted Caption: startseq chickens is spinning back on a yellow ring in a field of grass and plants all around him behind him of a yellow toy in the background behind him behind it of a large wall with many balconies

Image ID: 458213442
Actual Captions:
1. a black and white dog is jumping over a hurdle .
2. a black and white dog jumps over a bar in an agility test .
3. a dog jumps over a hurdle on a grass field .
4. a dog leaps over a bar on an obstacle course
5. the black and white dog jumps over an obstacle .
Predicted Caption: startseq dog running on green grass with black toy in background in mouth and black and black dog beside it tries to look over metal fence in background decorated with black and white dog tries to look over railing

Image ID: 458735196
Actual Captions:
1. a brown dog indoors , with a large pink toy .
2. a dog with a wrinkled face bites on a pink toy .
3. a wrinkled dog playing with a pink chew toy
4. the dog is carrying a pink ball in its mouth .
5. this is a strange sight , a dog delivering a cookie .
Predicted Caption: startseq dog with a dog sitting on a red bench with a stuffed dog underneath it and a dog who is laying on the ground with a furry dog in the bath and flowers stands in the background with

Image ID: 459284240
Actual Captions:
1. a toddler starting at a clown walking down a snowy sidewalk .
2. several people including a child and a clown are walking towards a snowy sidewalk
3. three adults and a toddler stand on a snowy path .
4. three adults and one child are walking along a paved path that is snow covered .
5. two adults , a child , and a clown walking down a sidewalk .
Predicted Caption: startseq woman in green jacket standing in the snow holding a checkered bag points to a mother in a blue vest with a blue vest on a beige vest and a blue vest and points out in the air

Image ID: 459778335
Actual Captions:
1. a father with his two kids at the ocean with the young boy flying up in the air .
2. a little boy jumps from his fathers arms on the beach .
3. a man tosses a boy into the air at the beach .
4. an adult man is throwing a child into the air at a beach while another child watches .
5. a young boy is thrown by a man as a girl watches at the beach .
Predicted Caption: startseq in the air at a beach volleyball game at the beach the man is falling into the water as it is falling into the water behind him and the girl in the black shirt is throwing the ball

Image ID: 459814265
Actual Captions:
1. a big , shaggy dog runs in a field of dandylions .
2. a dog running in a field of daisies
3. a dog sitting in the grass , with his tongue out
4. a long haired dog frolics in a meadow of yellow flowers .
5. a shaggy dog plays in a field of grass and yellow flowers .
Predicted Caption: startseq dog running through water with a furry stick in its mouth and sunlight toy nearby it while it tries to catch it off it and a dog in the background in the background is nearby a dog that

Image ID: 460195978
Actual Captions:
1. a black dog is in the grass with a woman in jeans .
2. a grey in a grey sweashirt running alongside of a small dog
3. a person playing with their black dog in the grass .
4. a woman and a dog are running in a field .
5. a woman flies a kite in a field while her dog watches .
Predicted Caption: startseq dog running through a field with a man in a blue shirt and blue sweater on the ground behind them in a black and black shirt with a dog in the background in the background two children in

Image ID: 460350019
Actual Captions:
1. a black dog and a woman in a red shirt playing tug of war .
2. a dog is pulling on one end of a rope and a girl is pulling on the other .
3. a woman plays tug-of-war with her black dog in a brown landscape surrounded by trees .
4. a woman plays with her rottweiler dog outside .
5. a woman and a dog playing outside
Predicted Caption: startseq dog running through grass with something in mouth of it and a black dog in tall background in the background and black holds camera in background watch the background trees behind it is walking behind it over autumn

Image ID: 460478198
Actual Captions:
1. a dog chasing another dog by a lake .
2. a husky chasing a brown spoted dog at the shore .
3. two dogs , a spaniel and a husky , chase each other across the sand by a body of water .
4. two dogs chase each other near the water .
5. two dogs playing by the shore .
Predicted Caption: startseq carrying a dog carrying a stick in its mouth walking through shallow water of a white dog with a stick in its mouth walking through the water with a stick in its mouth in the mouth with a

Image ID: 460781612
Actual Captions:
1. a black and white dog catches a frisbee in midair .
2. a black and white dog is midjump and has a frisbee in his mouth .
3. a black and white dog jumps up in the air to catch a frisbee .
4. a dog jumps in the air , catching a frisbee in its mouth .
5. a white dog in a jump , holding a plate in his mouth .
Predicted Caption: startseq of dogs running in the field with yellow flowers in the background and a man in a black and black vest with red and black vest with red and black jerseys in grass with orange and black dogs

Image ID: 460935487
Actual Captions:
1. a black and white dog is running up a path towards some potted plants .
2. a dog follows another dog around the corner but looks back .
3. a dog is turns back toward the camera near some potted plants .
4. a dog turning to look at the camera .
5. a white and black dog in a hallway filled with potted plants .
Predicted Caption: startseq dog sticking head to owner on a paper in front of a cement door with home colors in the cockpit and black headband behind paws on the floor in the background behind it is dog behind them of

Image ID: 460973814
Actual Captions:
1. a group of people sitting around a table drinking tea or coffee
2. three individuals sit at a table , smiling .
3. three people gather around a table for beverages .
4. three people gather around the table and have their picture taken .
5. two women and a man sit at a table having coffee in a home .
Predicted Caption: startseq seated seated seated seated seated woman and woman sitting in a cheery mexican restaurant table and christmas colors are seated and seated seated table of table and seated seated seated and seated seated seated seated seated seated seated

Image ID: 461019788
Actual Captions:
1. a couple stands on a dock by the water hugging .
2. a stone dock and a couple hugging at the end , water behind .
3. two people are hugging at the end of a stone jetty that looks out over the ocean .
4. two people embrace on the end of a dock .
5. two people stand on the pier looking at the ocean and embrace .
Predicted Caption: startseq cars in chairs over over water beyond view of sunset beyond view of sunset below cars in background beyond end end view from behind of over behind of cars and cars in the water fishing over the ocean

Image ID: 461505235
Actual Captions:
1. a man repels down a cliff over water .
2. a mountain climber hangs from a cliff above the ocean .
3. a person descends a rope from a cliff into the ocean .
4. a person is climbing a cliff wall , over a rocky shore , using a rope .
5. the man is climbing up the rock .
Predicted Caption: startseq climbing rocks over a rocky cliff below over rocks over a bridge with a large rock and blue rocks over the water below below a mountain wall over a rock wall over a red wall over the water

Image ID: 462080147
Actual Captions:
1. a man holding a bottle of wine with a box on his head
2. a man holding a wine bottle and wearing a box on his head is standing next to a man wearing a black hoodie .
3. one man wearing a black hoodie sweatshirt and another wearing a box over his head
4. one person is wearing a box on their head and holding a bottle while another man is standing next to him .
5. two men , one with a box on his head holding a bottle
Predicted Caption: startseq woman in black jacket and black hat standing in front of a woman in black and black with red shirt toward help at a man in black pants and a flowery shirt with black boots while standing in

Image ID: 462198798
Actual Captions:
1. a big , black dog is walking along the water 's edge .
2. a black dog and its reflection are seen near a pond ringed by dry foliage .
3. a black dog is walking beside water in the woods .
4. a black dog walks along a marsh 's edge .
5. a dog is walking near a body of water .
Predicted Caption: startseq running in a lake with trees in the background are all the sun runs through the water and others watch in the back of a boat on a lake with people in the background watch it hold something

Image ID: 462288558
Actual Captions:
1. a pitbull dog is biting another dog on the face .
2. a tan dog opens his mouth to bite another tan dog .
3. one dog is trying to bite another .
4. one tag dog biting another tan dog while laying on a bed .
5. two brown dogs playing with each other , one has his mouth open biting the other dog .
Predicted Caption: startseq pile blocks on a two newborn newborn puppies lying on a toy floor with other animals 's heads behind him on the floor with a person behind him and fingers on the end of a pile of milk

Image ID: 463786229
Actual Captions:
1. a bee clings to a yellow flower .
2. a bee on top of a flower
3. a bee sits on a flower .
4. a small bee landed on a bunch of yellow flowers
5. beautiful blue sky and yellow flowers .
Predicted Caption: startseq plants in the background watch it jumps over a tree while someone takes pictures of it covers upon it and it is shown from the ground behind him upon american flags spread i it holds up it out

Image ID: 463875230
Actual Captions:
1. a girl wearing pink swings on a swing .
2. a little girl is swinging high above a wooden fence on the swing .
3. a young girl in a pick shirt swinging up in the air on a swing set
4. the girl is on a swing .
5. the little girl played on the swing .
Predicted Caption: startseq in the air in a high piece of wood and palm frame several people in the garb watch a fellow in the face and a fellow in the background watch it jumps through the air between two people

Image ID: 463978865
Actual Captions:
1. a man sitting on the left near a man walking along the side of a street with colorful buildings .
2. a man walking by a sitting man on the street .
3. a man with dreadlocks and a backpack walks down the sidewalk with colorful buildings in the background .
4. a white man with dreadlocks walks down the sidewalk .
5. two boys are on the sidewalk as cars pass by on the road .
Predicted Caption: startseq cars on a brightly colored ride with cars and cars cross them the cars are on the side of a road and one person in a red shirt and another woman in the lead watch it crossing the

Image ID: 464116251
Actual Captions:
1. a black , brown , and white dog jumping over a pile of logs with trees in the background .
2. a dog is jumping over some logs .
3. a dog jumps over a pile of logs .
4. a dog jumps over a pile of wood .
5. a large dog is leaping over some logs in a woodland clearing .
Predicted Caption: startseq child in red shirt jumping off of a log while another man stands behind him in the background a man in shorts and blue shirt climbs off of tree lined tree and fallen animal in the background beyond

Image ID: 464251704
Actual Captions:
1. a girl in a pink top is swinging with her hair flying everywhere .
2. a girl is swinging .
3. a girl is swinging and looking down with her hair flying .
4. a girl 's hair streams behind her as she swings
5. a girl with long hair flying in the breeze while she swings .
Predicted Caption: startseq strapped up high tree high high in the air with hair attached to him banner banner banner banner banner splashes bands rides in air in midair setting in midair setting in midair setting up the tree high flying

Image ID: 464506846
Actual Captions:
1. a black dog is running across a grassy field in front of some bushes .
2. a dog in a grassy park jumping and playing .
3. a dog with a muzzle on .
4. a muzzled greyhound leaps over grassy ground .
5. the black dog leaps into the air in the grass .
Predicted Caption: startseq long black dog jumping into the woods for a stick in the field with a stick in the background and trees behind him and white dog in the background holding stick in his mouth and long collar stands

Image ID: 464527562
Actual Captions:
1. a brown dog has a purple disc .
2. a brown dog has its eyes closed and a purple frisbee in its mouth .
3. the brown and black dog is holding a pink disc on a green yard .
4. the dog returns the play toy to its master .
5. this is a dog holding a frisbee .
Predicted Caption: startseq grass with something nose to their nose with a yellow bottle in water with a yellow cloth in it and yellow blanket behind it nose to nose legs for water bottle in water with green water in it

Image ID: 465859490
Actual Captions:
1. a group of people are listening to a man with a moustache speak into a microphone .
2. a lady with brown hair sitting at a table while someone speaks on a microphone in the background .
3. a man holds a microphone and speaks as a group of seated people watch and one woman looks down .
4. a woman at a table looking down .
5. people sit a tables while a man speaks with a microphone .
Predicted Caption: startseq bar in a bar with a crowd in the background a man in a pink shirt smiles at a crowd of people at a bar with a tv tv standing nearby away from the other table the tv

Image ID: 465994762
Actual Captions:
1. a brown dog jumps over a chain .
2. a dog jumps over a chain .
3. a dog leaping over a chain .
4. a greyhound jumps over a chain .
5. brown dog leaps over a chain suspended over a gravel road .
Predicted Caption: startseq plastic dog with plastic nose and back over fallen legs and bat looking over fallen animal in the background holding fallen poles in the background behind him and gold trees in the background behind him behind metal object

Image ID: 466176275
Actual Captions:
1. a grey " labradoodle " jumps over another large dog .
2. one grey puddle jumping in the air in front of another tan dog
3. two dogs are chasing each other in a yard .
4. two dogs playing in grass .
5. two dogs , the gray poodle high in the air , play on the grass .
Predicted Caption: startseq colored dog catching a ball in his mouth while carrying a toy in his mouth in the grass with something in its mouth closing in mouth while a black dog runs by him in the background nearby the

```

## Code Updated

ရလဒ်တွေကို ကြည့်တော့ BLEU, chrF++ evaluation နှစ်မျိုးနဲ့ပဲ မလုံလောက်သလို ခံစားရတယ်။  
အဲဒါကြောင့် လူက evaluation လုပ်သလိုပဲ tf-idf နဲ့ semantic measure လုပ်တဲ့ function အသစ်တစ်ခု ဖြည့်ခဲ့တယ်။ 
ပြီးတော့ pycocoevalcap library ကို သုံးပြီးတော့ SPICE and CIDEr နှစ်မျိုးကို ထပ်ဖြည့်ခဲ့တယ်။  

ပြီးတော့ GRU cell type ကိုလည်း ထပ်ဖြည့်ပြီးတော့ default cell type ကို GRU ပဲ ထားလိုက်တယ်။
LSTM နဲ့ GRU ကို ရွေးလို့ ရအောင်လို့ command line argument အသစ်တစ်ခုပါ ဖြည့်ခဲ့တယ်။  
 
## Install Additional Libraries  

scikit-learn ကို install လုပ်ခဲ့တယ်။  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ python3.8 -m pip install scikit-learn
Collecting scikit-learn
  Using cached scikit_learn-1.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (11 kB)
Requirement already satisfied: numpy<2.0,>=1.17.3 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from scikit-learn) (1.24.4)
Collecting scipy>=1.5.0 (from scikit-learn)
  Using cached scipy-1.10.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (58 kB)
Requirement already satisfied: joblib>=1.1.1 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from scikit-learn) (1.4.2)
Collecting threadpoolctl>=2.0.0 (from scikit-learn)
  Using cached threadpoolctl-3.5.0-py3-none-any.whl.metadata (13 kB)
Using cached scikit_learn-1.3.2-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (11.1 MB)
Using cached scipy-1.10.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (34.5 MB)
Using cached threadpoolctl-3.5.0-py3-none-any.whl (18 kB)
Installing collected packages: threadpoolctl, scipy, scikit-learn
Successfully installed scikit-learn-1.3.2 scipy-1.10.1 threadpoolctl-3.5.0
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$
```

pycocoevalcap library ကိုလည်း install လုပ်ခဲ့တယ်။  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ python3.8 -m pip install pycocoevalcap
Collecting pycocoevalcap
  Downloading pycocoevalcap-1.2-py3-none-any.whl.metadata (3.2 kB)
Collecting pycocotools>=2.0.2 (from pycocoevalcap)
  Downloading pycocotools-2.0.7-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (1.1 kB)
Requirement already satisfied: matplotlib>=2.1.0 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from pycocotools>=2.0.2->pycocoevalcap) (3.7.5)
Requirement already satisfied: numpy in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from pycocotools>=2.0.2->pycocoevalcap) (1.24.4)
Requirement already satisfied: contourpy>=1.0.1 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (1.1.1)
Requirement already satisfied: cycler>=0.10 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (0.12.1)
Requirement already satisfied: fonttools>=4.22.0 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (4.57.0)
Requirement already satisfied: kiwisolver>=1.0.1 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (1.4.7)
Requirement already satisfied: packaging>=20.0 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (25.0)
Requirement already satisfied: pillow>=6.2.0 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (10.4.0)
Requirement already satisfied: pyparsing>=2.3.1 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (3.1.4)
Requirement already satisfied: python-dateutil>=2.7 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (2.9.0.post0)
Requirement already satisfied: importlib-resources>=3.2.0 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (6.4.5)
Requirement already satisfied: zipp>=3.1.0 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from importlib-resources>=3.2.0->matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (3.20.2)
Requirement already satisfied: six>=1.5 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from python-dateutil>=2.7->matplotlib>=2.1.0->pycocotools>=2.0.2->pycocoevalcap) (1.17.0)
Downloading pycocoevalcap-1.2-py3-none-any.whl (104.3 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 104.3/104.3 MB 14.7 MB/s eta 0:00:00
Downloading pycocotools-2.0.7-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (439 kB)
Installing collected packages: pycocotools, pycocoevalcap
Successfully installed pycocoevalcap-1.2 pycocotools-2.0.7
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$
```

## Call --help and Check Arguments  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ python3.8 ./image_captioning.py --help
2025-06-21 17:31:29.502746: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:31:29.502768: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
usage: image_captioning.py [-h] [--data_dir DATA_DIR] [--model_dir MODEL_DIR] [--epochs EPOCHS] [--batch_size BATCH_SIZE] [--train]
                           [--evaluate] [--predict PREDICT] [--language {english,myanmar}] [--model_name MODEL_NAME]
                           [--skip_download] [--skip_feature_extraction] [--lstm_units LSTM_UNITS] [--dropout_rate DROPOUT_RATE]
                           [--learning_rate LEARNING_RATE] [--early_stopping EARLY_STOPPING] [--feature_size FEATURE_SIZE]
                           [--cell_type {lstm,gru}]

Image Captioning with Flickr30k Dataset

optional arguments:
  -h, --help            show this help message and exit
  --data_dir DATA_DIR   Directory to store dataset (default: ./data)
  --model_dir MODEL_DIR
                        Directory to save/load models (default: ./models)
  --epochs EPOCHS       Number of training epochs (default: 15)
  --batch_size BATCH_SIZE
                        Training batch size (default: 64)
  --train               Train the model
  --evaluate            Evaluate on test set
  --predict PREDICT     Path to single image for prediction
  --language {english,myanmar}
                        Caption language (default: english)
  --model_name MODEL_NAME
                        Model filename (default: best_model.h5)
  --skip_download       Skip dataset download (for prediction mode)
  --skip_feature_extraction
                        Skip feature extraction if features file exists
  --lstm_units LSTM_UNITS
                        Number of units in LSTM layer (default: 256)
  --dropout_rate DROPOUT_RATE
                        Dropout rate (default: 0.4)
  --learning_rate LEARNING_RATE
                        Learning rate (default: 0.001)
  --early_stopping EARLY_STOPPING
                        Patience for early stopping (default: None)
  --feature_size FEATURE_SIZE
                        Size of image features (default: 4096)
  --cell_type {lstm,gru}
                        RNN cell type (default: gru)
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$
```

## Training GRU with 50 Epochs

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ cp ./model_lstm_50ep/features.pkl ./model_gru_50ep/
```

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ ./train_test_gru_50ep.sh
2025-06-21 17:39:35.901033: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:39:35.901050: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 17:39:37.499205: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 17:39:37.499366: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:39:37.499404: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:39:37.499428: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:39:37.499452: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:39:37.518286: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:39:37.518380: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 17:39:37.518392: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 17:39:37.518807: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Using GRU architecture
Training model for 50 epochs with:
- LSTM units: 256
- Dropout rate: 0.3
- Learning rate: 0.001
- Batch size: 32
227/227 [==============================] - 133s 580ms/step - loss: 4.9947
227/227 [==============================] - 129s 569ms/step - loss: 3.7312
227/227 [==============================] - 129s 569ms/step - loss: 3.3031
227/227 [==============================] - 128s 564ms/step - loss: 3.0322
227/227 [==============================] - 127s 559ms/step - loss: 2.8387
227/227 [==============================] - 128s 563ms/step - loss: 2.6952
227/227 [==============================] - 128s 561ms/step - loss: 2.5867
227/227 [==============================] - 127s 557ms/step - loss: 2.4932
227/227 [==============================] - 127s 559ms/step - loss: 2.4131
227/227 [==============================] - 127s 559ms/step - loss: 2.3371
227/227 [==============================] - 126s 556ms/step - loss: 2.2732
227/227 [==============================] - 127s 560ms/step - loss: 2.2201
227/227 [==============================] - 103s 453ms/step - loss: 2.1679
227/227 [==============================] - 103s 454ms/step - loss: 2.1227
227/227 [==============================] - 107s 471ms/step - loss: 2.0800
227/227 [==============================] - 125s 551ms/step - loss: 2.0397
227/227 [==============================] - 127s 558ms/step - loss: 2.0014
227/227 [==============================] - 127s 558ms/step - loss: 1.9711
227/227 [==============================] - 126s 554ms/step - loss: 1.9415
227/227 [==============================] - 126s 555ms/step - loss: 1.9098
227/227 [==============================] - 126s 554ms/step - loss: 1.8822
227/227 [==============================] - 126s 553ms/step - loss: 1.8574
227/227 [==============================] - 125s 551ms/step - loss: 1.8300
227/227 [==============================] - 127s 557ms/step - loss: 1.8071
227/227 [==============================] - 126s 553ms/step - loss: 1.7868
227/227 [==============================] - 126s 554ms/step - loss: 1.7668
227/227 [==============================] - 126s 553ms/step - loss: 1.7517
227/227 [==============================] - 126s 554ms/step - loss: 1.7327
227/227 [==============================] - 127s 557ms/step - loss: 1.7122
227/227 [==============================] - 126s 554ms/step - loss: 1.6948
227/227 [==============================] - 124s 545ms/step - loss: 1.6765
227/227 [==============================] - 125s 550ms/step - loss: 1.6592
227/227 [==============================] - 126s 554ms/step - loss: 1.6420
227/227 [==============================] - 125s 552ms/step - loss: 1.6298
227/227 [==============================] - 126s 554ms/step - loss: 1.6183
227/227 [==============================] - 126s 554ms/step - loss: 1.5990
227/227 [==============================] - 125s 551ms/step - loss: 1.5828
227/227 [==============================] - 126s 553ms/step - loss: 1.5677
227/227 [==============================] - 118s 521ms/step - loss: 1.5559
227/227 [==============================] - 99s 437ms/step - loss: 1.5413
227/227 [==============================] - 104s 460ms/step - loss: 1.5316
227/227 [==============================] - 112s 494ms/step - loss: 1.5208
227/227 [==============================] - 120s 528ms/step - loss: 1.5070
227/227 [==============================] - 126s 555ms/step - loss: 1.4961
227/227 [==============================] - 127s 559ms/step - loss: 1.4832
227/227 [==============================] - 126s 555ms/step - loss: 1.4742
227/227 [==============================] - 126s 552ms/step - loss: 1.4614
227/227 [==============================] - 126s 556ms/step - loss: 1.4492
227/227 [==============================] - 125s 551ms/step - loss: 1.4405
227/227 [==============================] - 126s 554ms/step - loss: 1.4335
Model saved to ./model_gru_50ep/best_model.h5
Tokenizer saved to ./model_gru_50ep/tokenizer.pkl

real    103m7.566s
user    1270m3.771s
sys     73m50.899s
2025-06-21 19:22:43.610247: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 19:22:43.610269: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 19:22:45.746319: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 19:22:45.746476: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 19:22:45.746513: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 19:22:45.746541: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 19:22:45.746569: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 19:22:45.769173: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 19:22:45.769240: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 19:22:45.769249: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 19:22:45.769470: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Model loaded from ./model_gru_50ep/best_model.h5
Evaluating: 100%|████████████████████████████████████████████████████████████████████████████████████| 810/810 [18:25<00:00,  1.36s/it]
Traceback (most recent call last):
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 1354, in do_open
Downloading stanford-corenlp-3.6.0 for SPICE ...
    h.request(req.get_method(), req.selector, req.data, headers,
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/http/client.py", line 1256, in request
    self._send_request(method, url, body, headers, encode_chunked)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/http/client.py", line 1302, in _send_request
    self.endheaders(body, encode_chunked=encode_chunked)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/http/client.py", line 1251, in endheaders
    self._send_output(message_body, encode_chunked=encode_chunked)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/http/client.py", line 1011, in _send_output
    self.send(msg)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/http/client.py", line 951, in send
    self.connect()
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/http/client.py", line 1425, in connect
    self.sock = self._context.wrap_socket(self.sock,
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/ssl.py", line 500, in wrap_socket
    return self.sslsocket_class._create(
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/ssl.py", line 1073, in _create
    self.do_handshake()
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/ssl.py", line 1342, in do_handshake
    self._sslobj.do_handshake()
ssl.SSLCertVerificationError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1149)

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "./image_captioning.py", line 755, in <module>
    main()
  File "./image_captioning.py", line 684, in main
    results, metrics = evaluate_model(
  File "./image_captioning.py", line 380, in evaluate_model
    spice_scorer = Spice()
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/pycocoevalcap/spice/spice.py", line 24, in __init__
    get_stanford_models()
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/pycocoevalcap/spice/get_stanford_models.py", line 27, in get_stanford_models
    zip_file, headers = urlretrieve(url, reporthook=print_progress)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 247, in urlretrieve
    with contextlib.closing(urlopen(url, data)) as fp:
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 222, in urlopen
    return opener.open(url, data, timeout)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 531, in open
    response = meth(req, response)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 640, in http_response
    response = self.parent.error(
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 563, in error
    result = self._call_chain(*args)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 502, in _call_chain
    result = func(*args)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 755, in http_error_302
    return self.parent.open(new, timeout=req.timeout)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 531, in open
    response = meth(req, response)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 640, in http_response
    response = self.parent.error(
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 563, in error
    result = self._call_chain(*args)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 502, in _call_chain
    result = func(*args)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 755, in http_error_302
    return self.parent.open(new, timeout=req.timeout)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 525, in open
    response = self._open(req, data)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 542, in _open
    result = self._call_chain(self.handle_open, protocol, protocol +
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 502, in _call_chain
    result = func(*args)
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 1397, in https_open
    return self.do_open(http.client.HTTPSConnection, req,
  File "/home/ye/miniforge3/envs/img2txt/lib/python3.8/urllib/request.py", line 1357, in do_open
    raise URLError(err)
urllib.error.URLError: <urlopen error [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: certificate has expired (_ssl.c:1149)>

real    18m33.647s
user    20m13.195s
sys     1m17.492s

```

SPICE evaluation က Error ဖြစ်တယ်။  
download လုပ်ဖို့ လိုအပ်တာနဲ့ ဆာဗာက ခွင့်မပြုတာစတာတွေကြောင့် ပြီးတော့ English အတွက် အဓိက ဖြစ်နေလို့ SPICE ကို ဖြုတ်ဖို့ လုပ်ခဲ့။  

## Updating the Code  

ROUGE score လည်း ထပ်ဖြည့်ခဲ့။  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ python3.8 -m pip install rouge-score
Collecting rouge-score
  Using cached rouge_score-0.1.2.tar.gz (17 kB)
  Preparing metadata (setup.py) ... done
Requirement already satisfied: absl-py in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from rouge-score) (2.3.0)
Requirement already satisfied: nltk in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from rouge-score) (3.9.1)
Requirement already satisfied: numpy in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from rouge-score) (1.24.4)
Requirement already satisfied: six>=1.14.0 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from rouge-score) (1.17.0)
Requirement already satisfied: click in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from nltk->rouge-score) (8.1.8)
Requirement already satisfied: joblib in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from nltk->rouge-score) (1.4.2)
Requirement already satisfied: regex>=2021.8.3 in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from nltk->rouge-score) (2024.11.6)
Requirement already satisfied: tqdm in /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages (from nltk->rouge-score) (4.67.1)
Building wheels for collected packages: rouge-score
  Building wheel for rouge-score (setup.py) ... done
  Created wheel for rouge-score: filename=rouge_score-0.1.2-py3-none-any.whl size=24936 sha256=e3153622a48fb8a03071778c9b695da449edf320d0bcb4e3be333cff4577eedc
  Stored in directory: /home/ye/.cache/pip/wheels/24/55/6f/ebfc4cb176d1c9665da4e306e1705496206d08215c1acd9dde
Successfully built rouge-score
Installing collected packages: rouge-score
Successfully installed rouge-score-0.1.2
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$
```

Evaluation results on GRU 50 epochs:  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 ./image_captioning.py --evaluate --model_dir ./model_gru_50ep | tee evaluate_gru_50ep.result.log
2025-06-21 20:21:17.685786: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 20:21:17.685814: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 20:21:19.623248: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 20:21:19.623394: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 20:21:19.623432: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 20:21:19.623460: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 20:21:19.623489: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 20:21:19.642765: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 20:21:19.642830: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 20:21:19.642840: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 20:21:19.643053: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Model loaded from ./model_gru_50ep/best_model.h5
Evaluating: 100%|████████████████████████████████████████████████████████████████████████████████████| 810/810 [18:26<00:00,  1.37s/it]

Warning: CIDEr calculation failed - 'dict' object has no attribute 'split'

Evaluation Metrics:
bleu1: 0.2325
bleu2: 0.1315
bleu4: 0.0343
chrf: 0.2105
semantic_similarity: 0.1379
keyword_overlap: 0.3010
composite_score: 0.1868
cider: 0.0000
rouge1: 0.1840
rouge2: 0.0415
rougeL: 0.1506
Results saved to ./model_gru_50ep/evaluation_results.txt

real    18m32.884s
user    20m14.346s
sys     1m18.058s
```

## Evaluation Result with GRU 50 Epochs  

```
Evaluation Metrics:
BLEU-1: 0.2325
BLEU-2: 0.1315
BLEU-4: 0.0343
chrF: 0.2105
CIDEr: 0.0000
ROUGE-1: 0.1840
ROUGE-2: 0.0415
ROUGE-L: 0.1506
Semantic Similarity: 0.1379
Keyword Overlap: 0.3010
Composite Score: 0.1868

Sample Results:

Image ID: 436015762
Actual Captions:
1. a man prepares to enter the red building .
2. a man walking around the corner of a red building .
3. a man walks past a red building with a fake rocket attached to it .
4. a man walks under a building with a large rocket shaped sculpture .
5. a person walking by a red building with a jet on top of it .
Predicted Caption: startseq against a large building with a neon view of a man on the left picture of him and blue pants on a wall behind him and a man in a neon blue jacket is standing on top of
Semantic Analysis:
- similarity: 0.2110
- keyword_overlap: 0.3600
- composite_score: 0.2557

Image ID: 436393371
Actual Captions:
1. a brown doberman is outside with a stick in its mouth .
2. a brown dog shows his teeth .
3. a dog bites a stick .
4. a dog is biting a twig .
5. a dog with sharp teeth is chewing on a stick outside .
Predicted Caption: startseq two dogs wrestle in the grass by a red carpet and a stone wall showing its fangs its mouth wide wide 's face in the background and a person watches in the distance the brown dog has fallen
Semantic Analysis:
- similarity: 0.1298
- keyword_overlap: 0.2069
- composite_score: 0.1529

Image ID: 436608339
Actual Captions:
1. a couple posing in front of a picture wall
2. an adult couple pose by a cardboard cut out for a movie .
3. an asian couple are standing by a fantasy poster .
4. an asian couple stands near a wax figure .
5. one person in a brown suit with his arm around another in a hat by a wall .
Predicted Caption: startseq two women in front of a building points at a woman in a knit cap and another woman in front waves behind them with short hair in the background holding a book bag behind them another speaking in
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2222
- composite_score: 0.0667

Image ID: 437054333
Actual Captions:
1. a bus filled with passengers in chicago at night .
2. a bus full of people waiting at a stop .
3. people are sitting on a bus .
4. people in a bus which is heading to 84 peterson .
5. there are people sitting on a bus that is labeled 84 peterson .
Predicted Caption: startseq looking in a hat looking at a screen in a city street with a silver house in the background and a building in the background looking at the counter in front of the door door door door door
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2500
- composite_score: 0.0750

Image ID: 437404867
Actual Captions:
1. a woman is sitting on a sidewalk with a cellphone at her ear .
2. a woman rests on the curb of a city street while talking on her cellphone .
3. a woman sits on the curb while talking on her cellphone .
4. a woman sits on the edge of a sidewalk with a garbage bin beside her
5. woman sits on the curb talking on a cellphone .
Predicted Caption: startseq a man is skateboarding in a small metal outdoor restaurant with a blue door and a woman behind him sits on a bench in front of a blue door with art behind them and a man behind him
Semantic Analysis:
- similarity: 0.1111
- keyword_overlap: 0.2917
- composite_score: 0.1653

Image ID: 437527058
Actual Captions:
1. a caravan of snowmobile travel through the snow .
2. a pair of people in heavy winter jackets rides through the snow on a snowmobile .
3. people riding something in the snow .
4. person on a polaris ski mobile in the snow .
5. the man wearing a blue helmet is riding a polaris .
Predicted Caption: startseq ice with red and red parka on a red sled in the snow and ice in the background and a red and red striped helmet begins to get the ice around him her ice in the background and
Semantic Analysis:
- similarity: 0.0578
- keyword_overlap: 0.2857
- composite_score: 0.1262

Image ID: 437917001
Actual Captions:
1. a dark colored man is laying on newspapers by a metal railing with his shoes off .
2. a homeless man is lying on the ground with his stuff strewn around .
3. a homeless man is sleeping outside at the top of a staircase .
4. an man is sleeping on top of his clothes on concrete stairs .
5. man sleeping on the street .
Predicted Caption: startseq truck is laying down on the ground 's legs and looks at the ground behind him laying on back of it and a blue hood on the ground and looks at the camera with its mouth open and
Semantic Analysis:
- similarity: 0.0799
- keyword_overlap: 0.3462
- composite_score: 0.1598

Image ID: 438639005
Actual Captions:
1. a boy in red and a girl pink are walking through a low cut field .
2. the little boy and little girl are walking side by side .
3. two small children walk away in a field .
4. two small children walking in a field .
5. two young children are walking across an open field .
Predicted Caption: startseq a boy runs through a field with two children on the grass team takes a kick out of the water and the player in the blue top is chasing the ball on the field of a field with
Semantic Analysis:
- similarity: 0.2970
- keyword_overlap: 0.3462
- composite_score: 0.3117

Image ID: 439037721
Actual Captions:
1. two men sitting on the bank of a lake with an ice chest .
2. two people having a picnic by a lake .
3. two people having a picnic by the shore .
4. two people sitting on grass in front of a lake looking at the sky .
5. two people with hats looking at a lake while sitting on a yellow-grassed hill .
Predicted Caption: startseq on a rainbow lines a man is riding a blue horse over a body of water beside a body of water below to fly behind him fly behind him behind him fly behind him behind him in a
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.1905
- composite_score: 0.0571

Image ID: 439049388
Actual Captions:
1. people , possibly fishermen , with their boats in shadow on shore at an orangesunset
2. a man in an orange vest is standing next to a yellow canoe .
3. people tend canoes at the edge of a body of water during a dimly lit time of day .
4. the men are getting their kayaks secured on the beach for the night .
5. two men standing on the shore beside their kayaks at dusk .
Predicted Caption: startseq sun on back of beach with two shirtless rocks and a city back behind it in the ocean and the sun is watching the sun of the water park it jumping over the water at sunset in the
Semantic Analysis:
- similarity: 0.0511
- keyword_overlap: 0.4231
- composite_score: 0.1627

Image ID: 439492931
Actual Captions:
1. a cluster of four brown dogs play in a field of brown grass .
2. four dogs are together in the field of dry grass .
3. four dogs in a grassy area .
4. four medium-sized dogs wrestle with each other on a grass field .
5. four small dogs play outside .
Predicted Caption: startseq followed a woman in a brown coat and coat on a horse and licking followed by a woman in a mask on the camera and a dog beckons it for a camera in its mouth while a small
Semantic Analysis:
- similarity: 0.0409
- keyword_overlap: 0.2609
- composite_score: 0.1069

Image ID: 439569646
Actual Captions:
1. a girl is hiding behind a painted wooden structure inside a building .
2. a little girl with a red dress facing a panel with her back to the camera .
3. a young blonde girl wearing a red dress kneeling on a red carpet .
4. a young girl faces a white and black wall in a red-carpeted room .
5. girl kneeling on a red carpet .
Predicted Caption: startseq purple dog is jumping on a couch in a house on the edge of a couch with a map of the other in the background of a adult 's lap in the background and a dog looks on
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.3182
- composite_score: 0.0955

Image ID: 439916996
Actual Captions:
1. brown dogs and a woman in a yard
2. a brown dog persues a frisbee across the grass as the thrower watches .
3. a woman in a blue jacket watches as her two brown dogs play with a red ball in a grassy yard .
4. a woman throws a frisbee for her two brown dogs to chase .
5. a woman watches a brown dog run away from a house across the grass .
Predicted Caption: startseq dog standing beside a white dog in a grassy park with a dog toy in its mouth and stuffed dog standing next to it and a dog toy to get it held by it of the dogs 's
Semantic Analysis:
- similarity: 0.1496
- keyword_overlap: 0.3600
- composite_score: 0.2127

Image ID: 440184957
Actual Captions:
1. a clown shares cut-out pictures of children .
2. a dirty looking clown holding up two paper cut outs of children with blond hair
3. a man wearing a balloon hat and a grassy shirt holds up two large paper dolls .
4. a man wearing a balloon hat holds up colored cut-out drawings of two men .
5. the man wears balloons on his head and holds paper people .
Predicted Caption: startseq of little girls are sitting on a red bench outside of a building with one of them in front of a wooden building and a person in a red cloth in her mouth and a person in overalls
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2083
- composite_score: 0.0625

Image ID: 440190907
Actual Captions:
1. a group of people walk through a shopping mall .
2. many people walk through the store .
3. people browse in a store .
4. people strolling through an indoor market .
5. the shoppers are walking in a store .
Predicted Caption: startseq vendor in a crowded square at night decorated with a stuffed toy in the background of a stuffed display in the background decorated at a carnival market at the concert and a stuffed toy in the background at
Semantic Analysis:
- similarity: 0.0141
- keyword_overlap: 0.2500
- composite_score: 0.0849

Image ID: 440737340
Actual Captions:
1. a black man with a red mask is carrying a box .
2. a man in a domino mask carries an amplifier up a hill .
3. a man with a mask carrying a black speaker
4. a masked man in bright clothing carrying a large box .
5. black man lifting black box is watched by black dog .
Predicted Caption: startseq brown dog dancing in the woods with a blue blanket in his mouth leaping to get it in the air while a man in the background tries to eat their back to the right of the picture of
Semantic Analysis:
- similarity: 0.0892
- keyword_overlap: 0.1786
- composite_score: 0.1160

Image ID: 441212506
Actual Captions:
1. the black dog runs with a ball with two smaller dogs behind it .
2. three dogs playing in a field , one with a ball in its mouth .
3. three dogs race towards the viewer over a lawn .
4. three dogs running in grass , one carrying a tennis ball in mouth .
5. two small dogs follow a larger dog with a tennis ball
Predicted Caption: startseq dog playing in a field with a black dog nearby a field of grass and a brown dog on the grass 's legs in front of the sky and a dog 's hand is nearby on the grass
Semantic Analysis:
- similarity: 0.1924
- keyword_overlap: 0.4286
- composite_score: 0.2633

Image ID: 44129946
Actual Captions:
1. a couple watches a boat against a skyline .
2. a man and woman sit on a bench , watching a boat go by .
3. the sun is setting while a man and woman watch a boat go by .
4. two people sit on a bench and watch a boat on the water .
5. two people watching a boat sail past .
Predicted Caption: startseq the lady is sitting on a dock looking out into the water with his feet up behind him and several people behind him behind her water on the end of it beyond the water and lake with their
Semantic Analysis:
- similarity: 0.0915
- keyword_overlap: 0.2500
- composite_score: 0.1391

Image ID: 441398149
Actual Captions:
1. a female jogger wearing red .
2. a girl with headphones is running next to some street signs .
3. a woman in a red outfit is jogging next to several street signs .
4. a woman jogging across an intersection .
5. the lady in red shorts jogs near a stop sign while listening to music .
Predicted Caption: startseq picture of a young girl in a red and black coat in front of a red building with a painted girl in front of him in front of a building with a funny decoration in her mouth while
Semantic Analysis:
- similarity: 0.1633
- keyword_overlap: 0.2857
- composite_score: 0.2000

Image ID: 441817653
Actual Captions:
1. a bearded man wearing a denim jacket and a hat sits on a park bench
2. a bearded man wearing a denim jacket sits on a bench .
3. a man with a bushy beard and a baseball cap sits on a park bench .
4. an old man with a long beard and jean jacket sits on a park bench .
5. an old man with a long white beard , glasses , and a hat is sitting on a park bench .
Predicted Caption: startseq a woman wearing a red coat and sunglasses talks to a man in a red jacket and sunglasses on a busy sidewalk with a bottle of water on her neck on the street with his hand on the
Semantic Analysis:
- similarity: 0.1055
- keyword_overlap: 0.2692
- composite_score: 0.1546

Image ID: 441921713
Actual Captions:
1. a bird lands on a mans glove .
2. a man holds a bird .
3. a man holds a falcon on his arm .
4. gloved man holding a bird of prey .
5. the man is wearing gloves and holding a hawk in his hands .
Predicted Caption: startseq view of a bench at a fair game with a dog and a person in a blue shirt with a shopping cart behind him in a blue sweater one person is drinking from a fishing object and a
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.1923
- composite_score: 0.0577

Image ID: 442220883
Actual Captions:
1. a brown dog has a white toy in its mouth .
2. a dog holding a white stuffed animal .
3. a tan dog hangong on to a white plushie toy .
4. a yellow dog is chewing on a white stuffed toy .
5. the dog is holding a stuffed toy in his mouth .
Predicted Caption: startseq dog with orange collar laying in the sand with a red toy in its mouth standing in shallow water with a red toy between them two ear of water in its mouths while eating in the mouths has
Semantic Analysis:
- similarity: 0.2020
- keyword_overlap: 0.3077
- composite_score: 0.2337

Image ID: 442594271
Actual Captions:
1. a bunch of people at the beach .
2. people are enjoying a sunny day on a sandy beach by the ocean .
3. people are on the beach and there is a kite in the air .
4. people on the beach and a kite in the sky .
5. sandy beach , people walking , laying , sitting , a kite is flying .
Predicted Caption: startseq along the beach of a group of people on a beach at beach of a beach of people on the beach at the beach at the beach and casting a rope at the beach of the water viewpoint
Semantic Analysis:
- similarity: 0.5669
- keyword_overlap: 0.5333
- composite_score: 0.5569

Image ID: 442918418
Actual Captions:
1. a brown dog is jumping over a fallen tree in the woods .
2. a small tan dog jumps over a small log .
3. tan colored dog jumping over a branch in the forest .
4. the dog leaps over the log in the forest .
5. the white dog is jumping over a fallen tree .
Predicted Caption: startseq dog running through fallen leaves on a log covered yard fallen in snow covered tree away from nearby foliage in the woods covered tree fallen leaves in the woods between foliage fallen fallen fallen fallen fallen fallen fallen
Semantic Analysis:
- similarity: 0.2770
- keyword_overlap: 0.3810
- composite_score: 0.3082

Image ID: 443430496
Actual Captions:
1. a brown dog swimming in murky water .
2. a brown dog swims in the murky water .
3. a dog with yellow fur swims , neck deep , in water .
4. a golden retreiver swimming in the water .
5. a yellow dog is swimming in the water .
Predicted Caption: startseq wet dog with golden hair walking in shallow water with a stick in its mouth while walking towards the water 's edge while a brown dog walks towards it towards the shore of the water 's back in
Semantic Analysis:
- similarity: 0.4174
- keyword_overlap: 0.3200
- composite_score: 0.3882

Image ID: 443885436
Actual Captions:
1. a tan curly haired dog jumps in the snow with a stick in its mouth .
2. a white dog catches a stick in the snow .
3. a white dog holds a stick in its mouth while it runs through snow .
4. a white dog jumps in the snow .
5. a white dog with light brown markings has a stick in his mouth and his paws in the snow .
Predicted Caption: startseq dog running through snow covered ground rocks in snow covered field with something in its mouth in the snow covered trees in snow looks behind it in snow covered landscape behind it in snow covered rocks in the
Semantic Analysis:
- similarity: 0.2972
- keyword_overlap: 0.4500
- composite_score: 0.3430

Image ID: 444047125
Actual Captions:
1. a person hiking at the foot of snowcapped mountains .
2. a person walks in the valley between tall mountains .
3. a person with a backpack and walking stick , walking towards the mountains in the valley below .
4. people with backpacks hiking in the mountains .
5. three people walk through a valley towards snowy mountains .
Predicted Caption: startseq mountain climbing road hiking covered mountains in background with a mountain in the background and a father stands in the background looking at the mountain in the background of mountains behind him seen from behind him seen from
Semantic Analysis:
- similarity: 0.1388
- keyword_overlap: 0.4091
- composite_score: 0.2199

Image ID: 444057017
Actual Captions:
1. a little girl gets her picture taken while on the merry-go-round .
2. a little girl in pink clothes holding yellow rods .
3. a little girl on a piece of playground equipment
4. a little girl sitting on a playground ride .
5. a young girl looks up as she rides on a merry-go-round .
Predicted Caption: startseq harness hanging hanging upside down with rope hanging out of frame dangling and rope rope rope nearby rope equipment behind him in green background and blue rubber rope dangling from support terrain by the background enjoys his legs
Semantic Analysis:
- similarity: 0.0076
- keyword_overlap: 0.1379
- composite_score: 0.0467

Image ID: 444481722
Actual Captions:
1. a dark skinned man walks by a woman talking on a cellphone .
2. a male walking and a female talking on the phone beside the concrete building .
3. people stand outside near a concrete wall and a window .
4. two people standing on the sidewalk .
5. two women , one carrying a purse and papers , are standing on a sidewalk .
Predicted Caption: startseq back of a man walking the top of a large brick wall while another man watches from the ground while another man watches him the back of the man is wearing a black and black jacket while walking
Semantic Analysis:
- similarity: 0.1150
- keyword_overlap: 0.2727
- composite_score: 0.1624

Image ID: 444803340
Actual Captions:
1. a guy and a girl , both wearing white shirts and jeans , stand under a flowering tree .
2. a man and a woman are talking in a park
3. a man and woman standing underneath the tree are talking .
4. a man in a white shirt is standing in the grass showing something to a woman in a white shirt .
5. a young couple both wearing white shirts and blue jeans standing in a light misty rain
Predicted Caption: startseq the little girl in the striped shirt is holding a drink in his mouth while standing in the background of flowers flowers with the other people in the background of the other people are looking at the fence
Semantic Analysis:
- similarity: 0.0761
- keyword_overlap: 0.3200
- composite_score: 0.1493

Image ID: 444845904
Actual Captions:
1. a man in a yellow helmet climbs a cliff face , snow behind him .
2. a man is climbing up a wall with a rope
3. a man leans back while climbing a mountain tethered to a rope .
4. he is rock climbing .
5. man with helmet rock climbing in a snowy area .
Predicted Caption: startseq sheer his tent in the snow with his backpack and a yellow backpack walks down the snow covered hill with his backpack resting his route down the surface of deep river and landscape behind him and another man
Semantic Analysis:
- similarity: 0.1064
- keyword_overlap: 0.2963
- composite_score: 0.1634

Image ID: 444872454
Actual Captions:
1. a group of students dressed in sweatshirts and jackets head towards the right .
2. a group of students walking on campus , some carrying books .
3. a group of students walk together .
4. a group of young people are walking through a park under blossoming trees .
5. several young women walk near blossoming cherry trees .
Predicted Caption: startseq a group of people gather for a picture with a lot of trees in the background and one of the girls is posing for a picture with a young girl in the back of a tree while others
Semantic Analysis:
- similarity: 0.1801
- keyword_overlap: 0.3600
- composite_score: 0.2340

Image ID: 444881000
Actual Captions:
1. a group of college students walk in nice weather .
2. a group of people walk in the park , while some talk on phones .
3. a group of students are walking through the campus .
4. a group of young people walking with two talking on cellphones .
5. several young people walking casually around
Predicted Caption: startseq two women and two dogs are outside with a white house in a wooded area while a woman looks on beside a woman in a black jacket and a lot of flowers in the background of the woman
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.3462
- composite_score: 0.1038

Image ID: 445148321
Actual Captions:
1. a person in the distance hikes among hoodoos with stars visible in the sky .
2. a person standing on a ridge in the desert .
3. interesting rock formations in the desert landscape , with stars above .
4. the night sky in the desert .
5. there is a person standing a mountain that has some interesting shapes .
Predicted Caption: startseq climbing snow hill of the water below this is walking on the snow covered ground with a cloudy background behind him behind him in the background of a cave with long clouds in the background and clouds in
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2400
- composite_score: 0.0720

Image ID: 445655284
Actual Captions:
1. a black and brown dog walks through the snow near a building .
2. a black dog , running in the snow .
3. a black dog running in the snow by some trees .
4. a large black and tan dog is running across the snow in a wooded area .
5. the black and brown dog is running through the snow .
Predicted Caption: startseq dog playing in snow with a blue toy in his mouth standing in snow covered dogs in the snow and snow covered object in its mouth 's snow in snow and snow background are other other dogs are
Semantic Analysis:
- similarity: 0.3438
- keyword_overlap: 0.2727
- composite_score: 0.3224

Image ID: 445861800
Actual Captions:
1. three men walking on a sidewalk in a city .
2. three people are walking down the street with cars and buildings in the background .
3. three people stand along a main road .
4. three people walking on a sidewalk with 3 light colored cars in the background .
5. three people wearing winter clothes standing on the sidewalk near a street
Predicted Caption: startseq a man in a grey jacket and blue scarf stands in front of a traffic covered street with a traffic engine in the background and traffic covered in traffic surrounded by traffic on the left side of it
Semantic Analysis:
- similarity: 0.0431
- keyword_overlap: 0.3200
- composite_score: 0.1262

Image ID: 446138054
Actual Captions:
1. a man in an orange hat jumping .
2. a man jumps in the middle of a rocky desert .
3. a man wearing a white shirt and an orange shirt jumped into the air .
4. man in khaki pants does elaborate kick in desert
5. man jumping with a rock formation in background .
Predicted Caption: startseq mid jump in the middle of a mountain field with a green clouds in the background and trees behind him looks like her opponent watches from behind her clouds in the mountains with trees in the background watch
Semantic Analysis:
- similarity: 0.0428
- keyword_overlap: 0.3077
- composite_score: 0.1222

Image ID: 446286714
Actual Captions:
1. an elderly man is sitting on a bench .
2. an older man wearing a brown coat siting on a bench .
3. an old man in a coat and hat sitting on a park bench .
4. old man in tan jacket and black cap sitting on bench
5. the older man with the shopping bag and cane is sitting on a bench .
Predicted Caption: startseq little girl in red dress and flip in front of a booth with rope in it both side of them in background are laying on back to back to the camera sitting behind them in a green pot
Semantic Analysis:
- similarity: 0.0604
- keyword_overlap: 0.2333
- composite_score: 0.1123

Image ID: 446291803
Actual Captions:
1. these woman are watching people play tennis from a bench .
2. two individuals watch a tennis match .
3. two people sit on a park bench while watching a neighborhood tennis match .
4. two people with red scarves on their heads are watching tennis .
5. two women sitting on a bench in front of a tennis court near a building complex .
Predicted Caption: startseq of people sitting on a wall step in the city whilst a few people sitting on a city center of the water with onlookers nearby them with a couple in the background next to a crowd of people
Semantic Analysis:
- similarity: 0.1464
- keyword_overlap: 0.2917
- composite_score: 0.1900

Image ID: 446514680
Actual Captions:
1. two brown dogs are fighting and they are both wearing red .
2. two brown dogs rough house outside .
3. two brown dogs wearing red collars look at each other while running along a dirt field .
4. two dogs play together .
5. two large brown short haired dogs with collars play chase in a field .
Predicted Caption: startseq brown dog running on sand with a ball in its mouth running beside frame on back of camera in background walking behind it in dry grass background on the ground behind it looks on them back to the
Semantic Analysis:
- similarity: 0.0885
- keyword_overlap: 0.1786
- composite_score: 0.1155

Image ID: 447111935
Actual Captions:
1. the two greyhound dogs wearing sweaters are playing in the grass .
2. two dogs play in the grass .
3. two dogs wearing shirts play in the green grass .
4. two dogs wearing sweaters play in a field .
5. two dogs wearing sweaters play in the grass .
Predicted Caption: startseq dog with mouth open and jumping in the grass direction another dog is laying in the grass with his mouth open and a dog in the grass tries to get it in the grass setting the other hand
Semantic Analysis:
- similarity: 0.1607
- keyword_overlap: 0.1739
- composite_score: 0.1647

Image ID: 447722389
Actual Captions:
1. a brown and white dog is jumping high and catching a blue ball .
2. a dog is jumping and catching a small , blue ball in a park surrounded by two other dogs .
3. a dog jumps and catches a blue ball in his mouth .
4. a dog jumps in the air to catch a blue ball .
5. three dogs run on grass , one leaps to catch blue ball .
Predicted Caption: startseq dog jumping to catch a ball in his mouth while one dog jumps back to catch him in his mouth while another dog watches from behind by a dog who is jumping in the mouth and tries to
Semantic Analysis:
- similarity: 0.4477
- keyword_overlap: 0.6000
- composite_score: 0.4934

Image ID: 447733067
Actual Captions:
1. a girl in a skimpy bikini outfit walks and carries a helmet .
2. a scantily clad girl , in a helmet , walks away from the camera , down a busy sidewalk .
3. a woman wearing a helmet , tall boots , and short shorts walks down the street .
4. girl in bikini bottoms , boots and a helmet walking away at a street fair .
5. the woman in the purple bikini and pink top is wearing a safety helmet .
Predicted Caption: startseq school girls wearing hats are walking on the street in front of a crowd of people in costumes at a street parade of school climbing building while people walk by her back on the sidewalk behind her clothing
Semantic Analysis:
- similarity: 0.0952
- keyword_overlap: 0.2759
- composite_score: 0.1494

Image ID: 447800028
Actual Captions:
1. a black dog playing with a purple toy in the snow .
2. a black dog runs through the snow carrying a blue toy .
3. a dog plays in the snow .
4. dog running with a purple toy in the snowy field .
5. the black and brown dog carries a purple toy in the snow .
Predicted Caption: startseq dog jumping to catch a toy in the snow as it jumps over a snowy field covered in snow and snow as a toy dog 's mouth open mouth open for it leaps in the snow as it
Semantic Analysis:
- similarity: 0.4678
- keyword_overlap: 0.3913
- composite_score: 0.4449

Image ID: 448252603
Actual Captions:
1. a boy pointing in a direction on a dirt road .
2. a boy with a backpack sits on a trail and points .
3. a man points his finger to the path ahead as he sits on the dirt path .
4. a man with a backpack is sitting in a dirt road and pointing toward the horizon .
5. a young man sitting in the middle of a dirt road pointing up the road .
Predicted Caption: startseq hiking little kids traveling tug of war with a large rock on the ground in front of the trees and a river in the background and a person walks down the path in front of the river and
Semantic Analysis:
- similarity: 0.0265
- keyword_overlap: 0.3200
- composite_score: 0.1145

Image ID: 448257345
Actual Captions:
1. a dog is staring at the food in the plate of a person eating .
2. a person holding a dog while they eat .
3. a person is eating a plate of pasta with a black and brown dog on his or her lap .
4. a person is eating pasta , while a dog is watching .
5. someone in a blue and white striped sweater is eating and the dog next to them is interested in their food .
Predicted Caption: startseq of brown and white puppies are standing on a wooden wall with flowers in its mouth open flowers with a blue collar behind it in its mouth one another is nearby a wooden fence with flowers on the
Semantic Analysis:
- similarity: 0.0331
- keyword_overlap: 0.3929
- composite_score: 0.1410

Image ID: 44856031
Actual Captions:
1. a brown dog is sprayed with water .
2. a dog is being squirted with water in the face outdoors .
3. a dog stands on his hind feet and catches a stream of water .
4. a jug is jumping up it is being squirted with a jet of water .
5. a tan , male dog is jumping up to get a drink of water from a spraying bottle .
Predicted Caption: startseq dog on leash in air over grass bench in area of building with white dog in the grass and looks on to get a ball held by the dogs that the dog has a stuffed colored dog on
Semantic Analysis:
- similarity: 0.2140
- keyword_overlap: 0.3571
- composite_score: 0.2569

Image ID: 448590900
Actual Captions:
1. a brown dog is sniffing around green grass on a hill .
2. a dog is digging a field .
3. a dog stands in a large , grassy field .
4. a dog walks alone in a field .
5. a dog with a red harness tracks a scent in a field .
Predicted Caption: startseq autumn brown dog with red collar resting his head through grassy field by grassy field field of grass with trees in the background and a person laying on the grass in front of it runs in the grass
Semantic Analysis:
- similarity: 0.4458
- keyword_overlap: 0.3571
- composite_score: 0.4192

Image ID: 448658518
Actual Captions:
1. a large man dressed in black on a street corner by a red brick building .
2. a man dressed in black is waiting at a crosswalk .
3. a man dressed in black stands at a street corner near a crossing light .
4. a man stands at a traffic light , waiting to cross the street .
5. man in black waits at crossing signal near large brick building .
Predicted Caption: startseq against a traffic wall and doing a trick against a brick wall and a person in a black shirt and hat jumping on the ground and corporate him in the distance tries to get it above him and
Semantic Analysis:
- similarity: 0.0916
- keyword_overlap: 0.3077
- composite_score: 0.1564

Image ID: 448916362
Actual Captions:
1. a dog is running through a field with its tongue hanging out .
2. a dog runs with his tongue hanging out .
3. a dog with its mouth open is running .
4. brown and cream dog with tongue out
5. the white and black dog runs on the field with his tongue hanging out .
Predicted Caption: startseq dog with mouth open and jumping in a field of purple and white flowers and a yellow item in the mouth whilst three other dogs are in the background watch a black and white dog is jumping through
Semantic Analysis:
- similarity: 0.2793
- keyword_overlap: 0.4444
- composite_score: 0.3288
```

## Note on Test Data

```
# Split data (around line 700 in your code)
image_ids = list(mapping.keys())
split = int(len(image_ids) * 0.9)  # 90% train, 10% test
train_keys = image_ids[:split]
test_keys = image_ids[split:]  # This is your test set
```

## CIDEr Format Updated  

```python
#!/usr/bin/env python
# coding: utf-8

"""
Improved Flickr30k Image Captioning System

Features:
- Command-line interface with argparse
- Support for both dataset evaluation and single image prediction
- Configurable paths for data and model saving
- Modular design for easier maintenance
- Prepared for multilingual support (including Myanmar)
- Evaluation metrics: BLEU, chrF++, CIDEr, ROUGE, semantic similarity
- Robust evaluation handling
- Enhanced hyperparameter configuration
- Support for both LSTM and GRU architectures
"""

import os
import pickle
import argparse
import numpy as np
import pandas as pd
from tqdm import tqdm
import matplotlib.pyplot as plt
from PIL import Image
import cv2

# TensorFlow/Keras imports
from tensorflow.keras.applications.vgg16 import VGG16, preprocess_input
from tensorflow.keras.preprocessing.image import load_img, img_to_array
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Model, load_model
from tensorflow.keras.utils import to_categorical, plot_model
from tensorflow.keras.layers import Input, Dense, LSTM, Embedding, Dropout, add
from tensorflow.keras.optimizers import Adam

# Evaluation metrics
from nltk.translate.bleu_score import corpus_bleu
from nltk.translate.chrf_score import corpus_chrf
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

try:
    from pycocoevalcap.cider.cider import Cider
except ImportError:
    print("Warning: pycocoevalcap not found. CIDEr metric will be unavailable.")
    Cider = None

try:
    from rouge_score import rouge_scorer
except ImportError:
    print("Warning: rouge-score not found. ROUGE metrics will be unavailable.")
    rouge_scorer = None

def download_dataset(data_dir):
    """Download and extract Flickr30k dataset with captions"""
    if not os.path.exists(data_dir):
        os.makedirs(data_dir)
    
    # 1. Download images
    image_dir = os.path.join(data_dir, 'flickr30k_images')
    if not os.path.exists(image_dir):
        print("Downloading Flickr30k images...")
        try:
            # Download parts
            for part in ['00', '01', '02']:
                url = f"https://github.com/awsaf49/flickr-dataset/releases/download/v1.0/flickr30k_part{part}"
                if os.system(f'wget "{url}" -q --show-progress') != 0:
                    raise Exception(f"Failed to download part {part}")
            
            # Combine and extract
            if os.system('cat flickr30k_part00 flickr30k_part01 flickr30k_part02 > flickr30k.zip') != 0:
                raise Exception("Failed to combine parts")
                
            # Create target directory
            os.makedirs(image_dir, exist_ok=True)
            
            # Extract to the correct location
            if os.system(f'unzip -q flickr30k.zip -d {image_dir}') != 0:
                raise Exception("Failed to extract zip")
            
            # Cleanup
            os.system('rm flickr30k_part00 flickr30k_part01 flickr30k_part02 flickr30k.zip')
            
            # Verify extraction
            if not os.listdir(image_dir):
                raise Exception("Extracted directory is empty")
            
        except Exception as e:
            print(f"Download failed: {str(e)}")
            if os.path.exists(image_dir):
                os.rmdir(image_dir)  # Clean up empty directory
            return False
    
    # 2. Download captions (if needed)
    captions_path = os.path.join(data_dir, "captions.txt")
    if not os.path.exists(captions_path):
        print("Downloading captions...")
        try:
            if os.system(f'wget https://github.com/jbrownlee/Datasets/releases/download/Flickr8k/Flickr8k_text.zip -O {data_dir}/captions.zip -q --show-progress') != 0:
                raise Exception("Failed to download captions")
            if os.system(f'unzip -j {data_dir}/captions.zip "Flickr8k.token.txt" -d {data_dir}') != 0:
                raise Exception("Failed to extract captions")
            os.system(f'mv {data_dir}/Flickr8k.token.txt {captions_path}')
            os.system(f'rm {data_dir}/captions.zip')
            
            # Verify captions file
            if not os.path.exists(captions_path):
                raise Exception("Captions file not created")
                
        except Exception as e:
            print(f"Caption download failed: {str(e)}")
            return False
    
    print("Dataset download complete.")
    return True

def load_and_preprocess_captions(caption_path, clean_func=None):
    """Load and preprocess captions from file"""
    mapping = {}
    
    with open(caption_path, 'r', encoding='utf-8') as f:
        # Handle both CSV and Flickr8k formats
        first_line = f.readline()
        f.seek(0)  # Rewind to start
        
        if first_line.startswith('image,caption'):  # Flickr30k format
            next(f)  # Skip header
            for line in f:
                tokens = line.strip().split(',')
                if len(line) < 2:
                    continue
                # MODIFIED: Remove everything after last underscore
                image_id = tokens[0].split('.')[0].rsplit('_', 1)[0]
                image_desc = tokens[1].strip()
                
                if clean_func:
                    image_desc = clean_func(image_desc)
                
                if image_id not in mapping:
                    mapping[image_id] = []
                mapping[image_id].append(image_desc)
        else:  # Flickr8k format
            for line in f:
                if not line.strip():
                    continue
                parts = line.strip().split('\t')
                if len(parts) < 2:
                    continue
                # MODIFIED: Remove everything after last underscore
                image_id = parts[0].split('.')[0].split('#')[0].rsplit('_', 1)[0]
                image_desc = parts[1].strip()
                
                if clean_func:
                    image_desc = clean_func(image_desc)
                
                if image_id not in mapping:
                    mapping[image_id] = []
                mapping[image_id].append(image_desc)
    
    return mapping

def clean_english_text(text):
    """Basic English text cleaning"""
    text = text.lower()
    # Add more cleaning as needed
    return text

def clean_myanmar_text(text):
    """Basic Myanmar text cleaning"""
    # Add Myanmar-specific cleaning here
    return text

def extract_image_features(image_paths, model, feature_size=4096):
    """Extract features from images using pre-trained model"""
    features = {}
    
    for img_path in tqdm(image_paths, desc="Extracting features"):
        try:
            img = load_img(img_path, target_size=(224, 224))
            img = img_to_array(img)
            img = img.reshape((1, img.shape[0], img.shape[1], img.shape[2]))
            img = preprocess_input(img)
            
            feature = model.predict(img, verbose=0).reshape(feature_size,)
            image_id = os.path.splitext(os.path.basename(img_path))[0]
            features[image_id] = feature
        except Exception as e:
            print(f"Error processing {img_path}: {str(e)}")
    
    return features

def create_tokenizer(captions):
    """Create tokenizer from captions"""
    all_captions = []
    for key in captions:
        for caption in captions[key]:
            all_captions.append(caption)
    
    tokenizer = Tokenizer()
    tokenizer.fit_on_texts(all_captions)
    
    vocab_size = len(tokenizer.word_index) + 1
    max_length = max(len(caption.split()) for caption in all_captions)
    
    return tokenizer, vocab_size, max_length

def data_generator(data_keys, features, mapping, tokenizer, max_length, vocab_size, batch_size):
    """Generator for training data"""
    X1, X2, y = [], [], []
    n = 0
    
    # Filter keys to only those with both features and captions
    valid_keys = [k for k in data_keys if k in features and k in mapping]
    
    while True:
        for key in valid_keys:
            n += 1
            captions = mapping[key]
            
            for caption in captions:
                seq = tokenizer.texts_to_sequences([caption])[0]
                
                for i in range(1, len(seq)):
                    in_seq, out_seq = seq[:i], seq[i]
                    in_seq = pad_sequences([in_seq], maxlen=max_length)[0]
                    out_seq = to_categorical([out_seq], num_classes=vocab_size)[0]
                    
                    X1.append(features[key])
                    X2.append(in_seq)
                    y.append(out_seq)
            
            if n == batch_size:
                X1 = np.array(X1)
                X2 = np.array(X2)
                y = np.array(y)
                yield [X1, X2], y
                X1, X2, y = [], [], []
                n = 0

def build_model(vocab_size, max_length, feature_size=4096, 
               lstm_units=256, dropout_rate=0.4, learning_rate=0.001,
               cell_type='gru'):
    """Build image captioning model with configurable architecture"""
    # Image feature layers
    inputs1 = Input(shape=(feature_size,))
    fe1 = Dropout(dropout_rate)(inputs1)
    fe2 = Dense(lstm_units, activation='relu')(fe1)
    
    # Sequence feature layers
    inputs2 = Input(shape=(max_length,))
    se1 = Embedding(vocab_size, lstm_units, mask_zero=True)(inputs2)
    se2 = Dropout(dropout_rate)(se1)
    
    # Select RNN cell type
    if cell_type.lower() == 'gru':
        from tensorflow.keras.layers import GRU
        se3 = GRU(lstm_units)(se2)
    else:  # Default to LSTM
        from tensorflow.keras.layers import LSTM
        se3 = LSTM(lstm_units)(se2)
    
    # Decoder model
    decoder1 = add([fe2, se3])
    decoder2 = Dense(lstm_units, activation='relu')(decoder1)
    outputs = Dense(vocab_size, activation='softmax')(decoder2)
    
    model = Model(inputs=[inputs1, inputs2], outputs=outputs)
    optimizer = Adam(learning_rate=learning_rate)
    model.compile(loss='categorical_crossentropy', optimizer=optimizer)
    
    return model

def idx_to_word(integer, tokenizer):
    """Convert index to word using tokenizer"""
    for word, index in tokenizer.word_index.items():
        if index == integer:
            return word
    return None

def predict_caption(model, image, tokenizer, max_length):
    """Generate caption for an image"""
    in_text = 'startseq'
    
    for _ in range(max_length):
        seq = tokenizer.texts_to_sequences([in_text])[0]
        seq = pad_sequences([seq], maxlen=max_length)
        yhat = model.predict([image, seq], verbose=0)
        yhat = np.argmax(yhat)
        
        word = idx_to_word(yhat, tokenizer)
        if word is None:
            break
            
        in_text += ' ' + word
        if word == 'endseq':
            break
    
    return in_text

## Own implementation for semantic similarity measurement
def semantic_similarity(predicted, references):
    """Calculate semantic similarity between predicted and reference captions"""
    # Combine all references
    all_texts = [' '.join(references), predicted]
    
    # Calculate TF-IDF vectors
    vectorizer = TfidfVectorizer(stop_words='english')
    try:
        tfidf = vectorizer.fit_transform(all_texts)
    except ValueError:
        return {'similarity': 0.0, 'keyword_overlap': 0.0}
    
    # Calculate cosine similarity
    sim = cosine_similarity(tfidf[0:1], tfidf[1:2])[0][0]
    
    # Keyword matching
    pred_words = set(predicted.lower().split())
    ref_words = set(' '.join(references).lower().split())
    keyword_overlap = len(pred_words & ref_words) / max(1, len(pred_words))
    
    return {
        'similarity': sim,
        'keyword_overlap': keyword_overlap,
        'composite_score': 0.7*sim + 0.3*keyword_overlap
    }

def evaluate_model(model, test_keys, features, mapping, tokenizer, max_length):
    """Evaluate model with multiple metrics"""
    actual, predicted = [], []
    actual_str, predicted_str = [], []
    results = []
    
    for key in tqdm(test_keys, desc="Evaluating"):
        captions = mapping[key]
        y_pred = predict_caption(model, features[key].reshape(1, -1), tokenizer, max_length)
        
        # Store results
        results.append({
            'image_id': key,
            'actual_captions': captions,
            'predicted_caption': y_pred
        })
        
        # Prepare for different metrics
        actual_captions = [caption.split() for caption in captions]
        y_pred_split = y_pred.split()
        
        actual.append(actual_captions)
        predicted.append(y_pred_split)
        actual_str.append(captions)
        predicted_str.append(y_pred)
    
    # Calculate metrics
    metrics = {}
    
    # BLEU scores
    metrics['bleu1'] = corpus_bleu(actual, predicted, weights=(1.0, 0, 0, 0))
    metrics['bleu2'] = corpus_bleu(actual, predicted, weights=(0.5, 0.5, 0, 0))
    metrics['bleu4'] = corpus_bleu(actual, predicted, weights=(0.25, 0.25, 0.25, 0.25))
    
    # chrF++
    metrics['chrf'] = corpus_chrf([' '.join(ref[0]) for ref in actual], predicted_str, beta=2.0)
    
    # Semantic similarity
    sem_scores = [semantic_similarity(pred, refs) 
                 for pred, refs in zip(predicted_str, actual_str)]
    metrics['semantic_similarity'] = np.mean([s['similarity'] for s in sem_scores])
    metrics['keyword_overlap'] = np.mean([s['keyword_overlap'] for s in sem_scores])
    metrics['composite_score'] = np.mean([s['composite_score'] for s in sem_scores])
    
    # CIDEr if available
    if Cider is not None:
        try:
            # Convert to COCO format - need to use the original references (not tokenized)
            gts = {}
            res = {}
            for i, (key, pred) in enumerate(zip(test_keys, predicted_str)):
                # Get original references (not tokenized)
                refs = mapping[key]
                gts[str(i)] = [{'caption': cap} for cap in refs]
                res[str(i)] = [{'caption': pred}]
        
            # Calculate CIDEr
            cider_scorer = Cider()
            cider_score, _ = cider_scorer.compute_score(gts, res)
            metrics['cider'] = cider_score
        except Exception as e:
            print(f"\nWarning: CIDEr calculation failed - {str(e)}")
            metrics['cider'] = 0.0

    # ROUGE scores if available
    if rouge_scorer is not None:
        try:
            scorer = rouge_scorer.RougeScorer(['rouge1', 'rouge2', 'rougeL'], use_stemmer=True)
            rouge_scores = []
            for refs, pred in zip(actual_str, predicted_str):
                # Use the first reference for ROUGE calculation
                score = scorer.score(refs[0], pred)
                rouge_scores.append(score)
            
            # Average ROUGE scores
            metrics['rouge1'] = np.mean([s['rouge1'].fmeasure for s in rouge_scores])
            metrics['rouge2'] = np.mean([s['rouge2'].fmeasure for s in rouge_scores])
            metrics['rougeL'] = np.mean([s['rougeL'].fmeasure for s in rouge_scores])
        except Exception as e:
            print(f"\nWarning: ROUGE calculation failed - {str(e)}")
            metrics['rouge1'] = metrics['rouge2'] = metrics['rougeL'] = 0.0
    
    return results, metrics

def save_results(results, metrics, output_dir):
    """Save evaluation results with all metrics"""
    # Save pickle file
    pickle_path = os.path.join(output_dir, 'evaluation_results.pkl')
    with open(pickle_path, 'wb') as f:
        pickle.dump({
            'results': results,
            'metrics': metrics
        }, f)
    
    # Save text file
    txt_path = os.path.join(output_dir, 'evaluation_results.txt')
    with open(txt_path, 'w', encoding='utf-8') as f:
        f.write("Evaluation Metrics:\n")
        f.write(f"BLEU-1: {metrics.get('bleu1', 0):.4f}\n")
        f.write(f"BLEU-2: {metrics.get('bleu2', 0):.4f}\n")
        f.write(f"BLEU-4: {metrics.get('bleu4', 0):.4f}\n")
        f.write(f"chrF: {metrics.get('chrf', 0):.4f}\n")
        
        if 'cider' in metrics:
            f.write(f"CIDEr: {metrics['cider']:.4f}\n")
        
        if 'rouge1' in metrics:
            f.write(f"ROUGE-1: {metrics['rouge1']:.4f}\n")
            f.write(f"ROUGE-2: {metrics['rouge2']:.4f}\n")
            f.write(f"ROUGE-L: {metrics['rougeL']:.4f}\n")
        
        f.write(f"Semantic Similarity: {metrics.get('semantic_similarity', 0):.4f}\n")
        f.write(f"Keyword Overlap: {metrics.get('keyword_overlap', 0):.4f}\n")
        f.write(f"Composite Score: {metrics.get('composite_score', 0):.4f}\n")
        
        f.write("\nSample Results:\n")
        for i, result in enumerate(results[:50]):
            f.write(f"\nImage ID: {result['image_id']}\n")
            f.write("Actual Captions:\n")
            for j, caption in enumerate(result['actual_captions'], 1):
                f.write(f"{j}. {caption}\n")
            f.write(f"Predicted Caption: {result['predicted_caption']}\n")
            f.write("Semantic Analysis:\n")
            sem = semantic_similarity(result['predicted_caption'], result['actual_captions'])
            for k, v in sem.items():
                f.write(f"- {k}: {v:.4f}\n")
    
    print(f"Results saved to {txt_path}")

def visualize_results(image_path, actual_captions, predicted_caption):
    """Visualize image with actual and predicted captions"""
    image = Image.open(image_path)
    plt.imshow(image)
    plt.axis('off')
    
    print("\nActual Captions:")
    for i, caption in enumerate(actual_captions, 1):
        print(f"{i}. {caption}")
    
    print(f"\nPredicted Caption: {predicted_caption}")
    plt.show()

def find_caption_file(data_dir):
    """Find the caption file in directory"""
    possible_names = [
        'captions.txt',
        'results.csv', 
        'Flickr8k.token.txt',
        'annotations/captions.txt'
    ]
    
    for name in possible_names:
        path = os.path.join(data_dir, name)
        if os.path.exists(path):
            return path
    return None

def main():
    parser = argparse.ArgumentParser(description='Image Captioning with Flickr30k Dataset')
    parser.add_argument('--data_dir', type=str, default='./data', 
                       help='Directory to store dataset (default: ./data)')
    parser.add_argument('--model_dir', type=str, default='./models', 
                       help='Directory to save/load models (default: ./models)')
    parser.add_argument('--epochs', type=int, default=15, 
                       help='Number of training epochs (default: 15)')
    parser.add_argument('--batch_size', type=int, default=64, 
                       help='Training batch size (default: 64)')
    parser.add_argument('--train', action='store_true', 
                       help='Train the model')
    parser.add_argument('--evaluate', action='store_true', 
                       help='Evaluate on test set')
    parser.add_argument('--predict', type=str, 
                       help='Path to single image for prediction')
    parser.add_argument('--language', type=str, default='english', 
                       choices=['english', 'myanmar'], help='Caption language (default: english)')
    parser.add_argument('--model_name', type=str, default='best_model.h5', 
                       help='Model filename (default: best_model.h5)')
    parser.add_argument('--skip_download', action='store_true',
                      help='Skip dataset download (for prediction mode)')
    parser.add_argument('--skip_feature_extraction', action='store_true',
                      help='Skip feature extraction if features file exists')
    
    parser.add_argument('--lstm_units', type=int, default=256,
                       help='Number of units in LSTM layer (default: 256)')
    parser.add_argument('--dropout_rate', type=float, default=0.4,
                       help='Dropout rate (default: 0.4)')
    parser.add_argument('--learning_rate', type=float, default=0.001,
                       help='Learning rate (default: 0.001)')
    parser.add_argument('--early_stopping', type=int, default=None,
                       help='Patience for early stopping (default: None)')
    parser.add_argument('--feature_size', type=int, default=4096,
                       help='Size of image features (default: 4096)')
    parser.add_argument('--cell_type', type=str, default='gru',
                       choices=['lstm', 'gru'], 
                       help='RNN cell type (default: gru)')

    args = parser.parse_args()
    
    # Create necessary directories
    os.makedirs(args.model_dir, exist_ok=True)
    model_path = os.path.join(args.model_dir, args.model_name)
    
    # Download dataset if needed (skip if in predict mode or --skip_download specified)
    if not (args.skip_download or args.predict):
        if not download_dataset(args.data_dir):
            return
    elif args.predict:
        print("Skipping dataset download for prediction mode")
    
    # Set paths
    image_dir = os.path.join(args.data_dir, 'flickr30k_images', 'Images')
    
    # Verify image directory exists
    if not os.path.exists(image_dir):
        print(f"Error: Image directory not found at {image_dir}")
        print("Please ensure the dataset downloaded correctly")
        return
    
    # Find caption file
    caption_path = find_caption_file(args.data_dir)
    if caption_path is None:
        print("Error: Could not find captions file in data directory")
        return

    # Load and preprocess captions
    clean_func = clean_english_text if args.language == 'english' else clean_myanmar_text
    mapping = load_and_preprocess_captions(caption_path, clean_func)
    
    # Get image paths
    image_paths = [os.path.join(image_dir, f) for f in os.listdir(image_dir) 
                  if f.lower().endswith(('.jpg', '.jpeg', '.png'))]

    # Load or extract image features
    features_path = os.path.join(args.model_dir, 'features.pkl')
    
    # Skip feature extraction if --skip_feature_extraction is set and features exist
    if args.skip_feature_extraction and os.path.exists(features_path):
        print("--skip_feature_extraction flag set and features file exists, skipping feature extraction")
        with open(features_path, 'rb') as f:
            features = pickle.load(f)
        print(f"Loaded features for {len(features)} images")
    else:
        if os.path.exists(features_path):
            try:
                print("Loading precomputed features...")
                with open(features_path, 'rb') as f:
                    features = pickle.load(f)
                print(f"Loaded features for {len(features)} images")
            except Exception as e:
                print(f"Error loading features: {str(e)}")
                print("Will re-extract features...")
                features = {}
        else:
            features = {}

        if not features:
            print("Extracting features with VGG16...")
            vgg_model = VGG16(weights='imagenet')
            vgg_model = Model(inputs=vgg_model.inputs, outputs=vgg_model.layers[-2].output)
            
            # Only extract features for images we don't already have
            existing_ids = set(features.keys())
            new_image_paths = [p for p in image_paths 
                             if os.path.splitext(os.path.basename(p))[0] not in existing_ids]
            
            if new_image_paths:
                new_features = extract_image_features(new_image_paths, vgg_model)
                features.update(new_features)
                print(f"Added features for {len(new_features)} new images")
            
            # Save features if we have any
            if features:
                with open(features_path, 'wb') as f:
                    pickle.dump(features, f)
                print(f"Saved features for {len(features)} images total")
            else:
                print("Error: No features extracted")
                return

    print(f"Found {len(image_paths)} images in {image_dir}")
    print("Sample image paths:", image_paths[:3])

    # Find common keys
    common_keys = set(features.keys()) & set(mapping.keys())
    print(f"Common images with both features and captions: {len(common_keys)}")

    if not common_keys:
        print("Error: No matching images between features and captions!")
        print("Sample feature keys:", list(features.keys())[:5])
        print("Sample mapping keys:", list(mapping.keys())[:5])
        return

    # Filter mappings to only include images we have features for
    mapping = {k: v for k, v in mapping.items() if k in features}

    # Create tokenizer
    tokenizer, vocab_size, max_length = create_tokenizer(mapping)
    
    # Split data
    image_ids = list(mapping.keys())
    split = int(len(image_ids) * 0.9)  # 90% train, 10% test
    train_keys = image_ids[:split]
    test_keys = image_ids[split:]
        
    if args.train:
        
        # Build model with selected cell type
        model = build_model(
            vocab_size, 
            max_length,
            feature_size=args.feature_size,
            lstm_units=args.lstm_units,
            dropout_rate=args.dropout_rate,
            learning_rate=args.learning_rate,
            cell_type=args.cell_type
        )
        
        steps = len(train_keys) // args.batch_size

        print(f"Using {args.cell_type.upper()} architecture")
        print(f"Training model for {args.epochs} epochs with:")
        print(f"- LSTM units: {args.lstm_units}")
        print(f"- Dropout rate: {args.dropout_rate}")
        print(f"- Learning rate: {args.learning_rate}")
        print(f"- Batch size: {args.batch_size}")

        for epoch in range(args.epochs):
            generator = data_generator(
                train_keys, features, mapping, tokenizer, 
                max_length, vocab_size, args.batch_size
            )
            model.fit(
                generator, 
                steps_per_epoch=steps, 
                epochs=1, 
                verbose=1
            )
        
        # Save model
        model.save(model_path)
        print(f"Model saved to {model_path}")
    
        # Save tokenizer and max_length for prediction
        tokenizer_path = os.path.join(args.model_dir, 'tokenizer.pkl')
        with open(tokenizer_path, 'wb') as f:
            pickle.dump((tokenizer, max_length), f)
        print(f"Tokenizer saved to {tokenizer_path}")

    # Load model for evaluation/prediction
    if args.evaluate or args.predict:
        if os.path.exists(model_path):
            model = load_model(model_path)
            print(f"Model loaded from {model_path}")
        else:
            print("Error: Model not found. Please train first or check path.")
            return
    
#    if args.evaluate:
        # Evaluate on test set with new metrics
#        results, bleu1, bleu2, bleu3, bleu4, chrfpp = evaluate_model(
#            model, test_keys, features, mapping, tokenizer, max_length
#        )
        
#        print("\nEvaluation Metrics:")
#        print(f"BLEU-1: {bleu1:.4f}")
#        print(f"BLEU-2: {bleu2:.4f}")
#        print(f"BLEU-3: {bleu3:.4f}")
#        print(f"BLEU-4: {bleu4:.4f}")
#        print(f"chrF++: {chrfpp:.4f}")
        
        # Save results with new format
#        metrics = {
#            'bleu1': bleu1,
#            'bleu2': bleu2,
#            'bleu3': bleu3,
#            'bleu4': bleu4,
#            'chrfpp': chrfpp
#        }
#        save_results(results, metrics, args.model_dir)
    
    if args.evaluate:
        results, metrics = evaluate_model(
            model, test_keys, features, mapping, tokenizer, max_length
        )
        
        print("\nEvaluation Metrics:")
        for name, score in metrics.items():
            print(f"{name}: {score:.4f}")
        
        save_results(results, metrics, args.model_dir)

    if args.predict:
        # Predict for single image
        if not os.path.exists(args.predict):
            print(f"Error: Image file not found at {args.predict}")
            return
    
        # Verify image directory exists
        if not os.path.exists(image_dir):
            print(f"Error: Image directory not found at {image_dir}")
            print("Please ensure the dataset downloaded correctly")
            return
    
        # Load tokenizer and max_length
        tokenizer_path = os.path.join(args.model_dir, 'tokenizer.pkl')
        if os.path.exists(tokenizer_path):
            with open(tokenizer_path, 'rb') as f:
                tokenizer, max_length = pickle.load(f)
        else:
            print("Error: Tokenizer not found. Please train first.")
            return
        
        # Extract features for the image
        vgg_model = VGG16(weights='imagenet')
        vgg_model = Model(inputs=vgg_model.inputs, outputs=vgg_model.layers[-2].output)
    
        # Skip image directory check for prediction
        try:
            img_features = extract_image_features([args.predict], vgg_model)
        except Exception as e:
            print(f"Error processing image: {str(e)}")
            return
    
        if not img_features:
            print("Error: Could not extract features from image.")
            return
    
        # Get image ID (use filename without extension)
        image_id = os.path.splitext(os.path.basename(args.predict))[0]
    
        # Predict caption
        feature = img_features[image_id].reshape(1, -1)
        caption = predict_caption(model, feature, tokenizer, max_length)
    
        # Display results
        #image = Image.open(args.predict)
        #plt.imshow(image)
        #plt.axis('off')
        #plt.title("Predicted Caption: " + caption)
        #plt.show()
        #plt.savefig("hyp.png")
    
        print(f"\nPredicted Caption: {caption}")

        # Also show semantic analysis
        sem = semantic_similarity(caption, mapping.get(image_id, ["No reference captions"]))
        print("\nSemantic Analysis:")
        for k, v in sem.items():
            print(f"{k}: {v:.4f}")
        return

if __name__ == '__main__':
    main()


```

## Evaluation Again with Updated Code  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ time python3.8 ./image_captioning.py --evaluate --model_dir ./model_gru_50ep | tee evaluate_gru_50ep.result.log2
2025-06-21 21:41:54.831656: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 21:41:54.831673: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 21:41:56.893134: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 21:41:56.893376: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 21:41:56.893451: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 21:41:56.893513: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 21:41:56.893576: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 21:41:56.915977: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 21:41:56.916059: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 21:41:56.916068: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 21:41:56.916301: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Model loaded from ./model_gru_50ep/best_model.h5
Evaluating: 100%|████████████████████████████████████████████████████████████████████████████████████| 810/810 [18:10<00:00,  1.35s/it]

Evaluation Metrics:
bleu1: 0.2325
bleu2: 0.1315
bleu4: 0.0343
chrf: 0.2105
semantic_similarity: 0.1379
keyword_overlap: 0.3010
composite_score: 0.1868
cider: 0.0004
rouge1: 0.1840
rouge2: 0.0415
rougeL: 0.1506
Results saved to ./model_gru_50ep/evaluation_results.txt

real    18m18.316s
user    19m58.582s
sys     1m17.282s
```

## Running GRU with 200 epochs  

```
(img2txt) ye@lst-hpc3090:~/intern3/img2txt$ ./train_test_gru_200ep.sh
2025-06-21 23:15:11.851322: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 23:15:11.851343: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-21 23:15:13.141161: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-21 23:15:13.141320: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 23:15:13.141361: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 23:15:13.141392: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 23:15:13.141431: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 23:15:13.163723: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 23:15:13.163786: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-21 23:15:13.163796: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-21 23:15:13.164011: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Extracting features with VGG16...
Extracting features: 100%|█████████████████████████████████████████████████████████████████████| 31783/31783 [1:08:32<00:00,  7.73it/s]
Added features for 31783 new images
Saved features for 31783 images total
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Using GRU architecture
Training model for 200 epochs with:
- LSTM units: 256
- Dropout rate: 0.5
- Learning rate: 0.002
- Batch size: 24
303/303 [==============================] - 141s 460ms/step - loss: 4.6857
303/303 [==============================] - 138s 456ms/step - loss: 3.5668
303/303 [==============================] - 134s 444ms/step - loss: 3.2232
303/303 [==============================] - 135s 444ms/step - loss: 3.0084
303/303 [==============================] - 133s 438ms/step - loss: 2.8558
303/303 [==============================] - 134s 442ms/step - loss: 2.7414
303/303 [==============================] - 133s 440ms/step - loss: 2.6509
303/303 [==============================] - 133s 440ms/step - loss: 2.5765
303/303 [==============================] - 133s 439ms/step - loss: 2.5159
303/303 [==============================] - 133s 440ms/step - loss: 2.4636
303/303 [==============================] - 133s 439ms/step - loss: 2.4210
303/303 [==============================] - 132s 436ms/step - loss: 2.3814
303/303 [==============================] - 132s 437ms/step - loss: 2.3420
303/303 [==============================] - 134s 443ms/step - loss: 2.3077
303/303 [==============================] - 132s 437ms/step - loss: 2.2742
303/303 [==============================] - 132s 434ms/step - loss: 2.2422
303/303 [==============================] - 132s 434ms/step - loss: 2.2180
303/303 [==============================] - 132s 435ms/step - loss: 2.1959
303/303 [==============================] - 126s 416ms/step - loss: 2.1734
303/303 [==============================] - 104s 344ms/step - loss: 2.1526
303/303 [==============================] - 111s 365ms/step - loss: 2.1370
303/303 [==============================] - 124s 410ms/step - loss: 2.1198
303/303 [==============================] - 131s 433ms/step - loss: 2.1013
303/303 [==============================] - 131s 432ms/step - loss: 2.0875
303/303 [==============================] - 130s 430ms/step - loss: 2.0735
303/303 [==============================] - 122s 404ms/step - loss: 2.0620
303/303 [==============================] - 130s 430ms/step - loss: 2.0498
303/303 [==============================] - 130s 429ms/step - loss: 2.0378
303/303 [==============================] - 130s 429ms/step - loss: 2.0303
303/303 [==============================] - 130s 429ms/step - loss: 2.0193
303/303 [==============================] - 130s 428ms/step - loss: 2.0102
303/303 [==============================] - 129s 427ms/step - loss: 2.0030
303/303 [==============================] - 131s 431ms/step - loss: 1.9932
303/303 [==============================] - 129s 427ms/step - loss: 1.9884
303/303 [==============================] - 105s 345ms/step - loss: 1.9824
303/303 [==============================] - 130s 429ms/step - loss: 1.9762
303/303 [==============================] - 130s 428ms/step - loss: 1.9731
303/303 [==============================] - 130s 428ms/step - loss: 1.9662
303/303 [==============================] - 131s 431ms/step - loss: 1.9583
303/303 [==============================] - 130s 430ms/step - loss: 1.9551
303/303 [==============================] - 130s 429ms/step - loss: 1.9451
303/303 [==============================] - 131s 431ms/step - loss: 1.9416
303/303 [==============================] - 130s 429ms/step - loss: 1.9401
303/303 [==============================] - 115s 381ms/step - loss: 1.9356
303/303 [==============================] - 112s 369ms/step - loss: 1.9272
303/303 [==============================] - 107s 353ms/step - loss: 1.9245
303/303 [==============================] - 112s 369ms/step - loss: 1.9204
303/303 [==============================] - 131s 432ms/step - loss: 1.9191
303/303 [==============================] - 130s 429ms/step - loss: 1.9091
303/303 [==============================] - 130s 428ms/step - loss: 1.9093
303/303 [==============================] - 131s 434ms/step - loss: 1.9048
303/303 [==============================] - 130s 430ms/step - loss: 1.9030
303/303 [==============================] - 129s 427ms/step - loss: 1.8987
303/303 [==============================] - 129s 426ms/step - loss: 1.8979
303/303 [==============================] - 130s 430ms/step - loss: 1.8908
303/303 [==============================] - 130s 428ms/step - loss: 1.8896
303/303 [==============================] - 131s 431ms/step - loss: 1.8863
303/303 [==============================] - 130s 429ms/step - loss: 1.8850
303/303 [==============================] - 130s 431ms/step - loss: 1.8828
303/303 [==============================] - 130s 429ms/step - loss: 1.8775
303/303 [==============================] - 131s 432ms/step - loss: 1.8780
303/303 [==============================] - 130s 430ms/step - loss: 1.8758
303/303 [==============================] - 130s 430ms/step - loss: 1.8774
303/303 [==============================] - 126s 416ms/step - loss: 1.8710
303/303 [==============================] - 129s 427ms/step - loss: 1.8695
303/303 [==============================] - 130s 429ms/step - loss: 1.8663
303/303 [==============================] - 130s 429ms/step - loss: 1.8650
303/303 [==============================] - 130s 427ms/step - loss: 1.8664
303/303 [==============================] - 130s 429ms/step - loss: 1.8596
303/303 [==============================] - 105s 345ms/step - loss: 1.8622
303/303 [==============================] - 108s 358ms/step - loss: 1.8581
303/303 [==============================] - 117s 387ms/step - loss: 1.8546
303/303 [==============================] - 131s 430ms/step - loss: 1.8541
303/303 [==============================] - 130s 430ms/step - loss: 1.8521
303/303 [==============================] - 131s 431ms/step - loss: 1.8527
303/303 [==============================] - 130s 429ms/step - loss: 1.8527
303/303 [==============================] - 130s 430ms/step - loss: 1.8511
303/303 [==============================] - 130s 429ms/step - loss: 1.8473
303/303 [==============================] - 130s 430ms/step - loss: 1.8460
303/303 [==============================] - 131s 431ms/step - loss: 1.8493
303/303 [==============================] - 129s 427ms/step - loss: 1.8468
303/303 [==============================] - 129s 426ms/step - loss: 1.8479
303/303 [==============================] - 130s 429ms/step - loss: 1.8408
303/303 [==============================] - 130s 430ms/step - loss: 1.8454
303/303 [==============================] - 130s 429ms/step - loss: 1.8409
303/303 [==============================] - 130s 430ms/step - loss: 1.8447
303/303 [==============================] - 131s 431ms/step - loss: 1.8375
303/303 [==============================] - 131s 431ms/step - loss: 1.8356
303/303 [==============================] - 131s 432ms/step - loss: 1.8386
303/303 [==============================] - 130s 427ms/step - loss: 1.8375
303/303 [==============================] - 130s 430ms/step - loss: 1.8386
303/303 [==============================] - 119s 393ms/step - loss: 1.8376
303/303 [==============================] - 130s 429ms/step - loss: 1.8347
303/303 [==============================] - 128s 421ms/step - loss: 1.8334
303/303 [==============================] - 103s 340ms/step - loss: 1.8321
303/303 [==============================] - 110s 362ms/step - loss: 1.8365
303/303 [==============================] - 123s 405ms/step - loss: 1.8368
303/303 [==============================] - 131s 433ms/step - loss: 1.8340
303/303 [==============================] - 131s 432ms/step - loss: 1.8297
303/303 [==============================] - 130s 429ms/step - loss: 1.8281
303/303 [==============================] - 131s 431ms/step - loss: 1.8282
303/303 [==============================] - 131s 431ms/step - loss: 1.8299
303/303 [==============================] - 130s 430ms/step - loss: 1.8308
303/303 [==============================] - 131s 431ms/step - loss: 1.8328
303/303 [==============================] - 130s 428ms/step - loss: 1.8334
303/303 [==============================] - 130s 429ms/step - loss: 1.8292
303/303 [==============================] - 131s 431ms/step - loss: 1.8308
303/303 [==============================] - 130s 430ms/step - loss: 1.8297
303/303 [==============================] - 130s 428ms/step - loss: 1.8318
303/303 [==============================] - 130s 430ms/step - loss: 1.8350
303/303 [==============================] - 130s 429ms/step - loss: 1.8282
303/303 [==============================] - 130s 428ms/step - loss: 1.8325
303/303 [==============================] - 130s 429ms/step - loss: 1.8268
303/303 [==============================] - 131s 430ms/step - loss: 1.8295
303/303 [==============================] - 131s 431ms/step - loss: 1.8267
303/303 [==============================] - 131s 431ms/step - loss: 1.8303
303/303 [==============================] - 130s 429ms/step - loss: 1.8304
303/303 [==============================] - 131s 432ms/step - loss: 1.8333
303/303 [==============================] - 113s 373ms/step - loss: 1.8332
303/303 [==============================] - 106s 351ms/step - loss: 1.8327
303/303 [==============================] - 112s 368ms/step - loss: 1.8324
303/303 [==============================] - 130s 430ms/step - loss: 1.8303
303/303 [==============================] - 130s 429ms/step - loss: 1.8301
303/303 [==============================] - 128s 423ms/step - loss: 1.8316
303/303 [==============================] - 130s 429ms/step - loss: 1.8310
303/303 [==============================] - 130s 430ms/step - loss: 1.8323
303/303 [==============================] - 130s 430ms/step - loss: 1.8365
303/303 [==============================] - 131s 432ms/step - loss: 1.8344
303/303 [==============================] - 130s 429ms/step - loss: 1.8291
303/303 [==============================] - 130s 430ms/step - loss: 1.8330
303/303 [==============================] - 131s 431ms/step - loss: 1.8327
303/303 [==============================] - 126s 417ms/step - loss: 1.8342
303/303 [==============================] - 130s 429ms/step - loss: 1.8352
303/303 [==============================] - 130s 428ms/step - loss: 1.8354
303/303 [==============================] - 130s 427ms/step - loss: 1.8363
303/303 [==============================] - 130s 430ms/step - loss: 1.8367
303/303 [==============================] - 130s 428ms/step - loss: 1.8382
303/303 [==============================] - 130s 430ms/step - loss: 1.8413
303/303 [==============================] - 130s 430ms/step - loss: 1.8384
303/303 [==============================] - 131s 431ms/step - loss: 1.8403
303/303 [==============================] - 129s 425ms/step - loss: 1.8419
303/303 [==============================] - 130s 427ms/step - loss: 1.8415
303/303 [==============================] - 129s 425ms/step - loss: 1.8393
303/303 [==============================] - 107s 352ms/step - loss: 1.8378
303/303 [==============================] - 108s 356ms/step - loss: 1.8418
303/303 [==============================] - 116s 383ms/step - loss: 1.8401
303/303 [==============================] - 131s 431ms/step - loss: 1.8439
303/303 [==============================] - 130s 429ms/step - loss: 1.8397
303/303 [==============================] - 130s 430ms/step - loss: 1.8483
303/303 [==============================] - 130s 430ms/step - loss: 1.8442
303/303 [==============================] - 130s 429ms/step - loss: 1.8419
303/303 [==============================] - 129s 425ms/step - loss: 1.8443
303/303 [==============================] - 130s 429ms/step - loss: 1.8456
303/303 [==============================] - 130s 429ms/step - loss: 1.8426
303/303 [==============================] - 130s 430ms/step - loss: 1.8414
303/303 [==============================] - 131s 432ms/step - loss: 1.8430
303/303 [==============================] - 130s 429ms/step - loss: 1.8463
303/303 [==============================] - 130s 430ms/step - loss: 1.8464
303/303 [==============================] - 132s 436ms/step - loss: 1.8429
303/303 [==============================] - 135s 444ms/step - loss: 1.8517
303/303 [==============================] - 127s 417ms/step - loss: 1.8561
303/303 [==============================] - 136s 448ms/step - loss: 1.8541
303/303 [==============================] - 137s 451ms/step - loss: 1.8565
303/303 [==============================] - 136s 447ms/step - loss: 1.8535
303/303 [==============================] - 136s 448ms/step - loss: 1.8538
303/303 [==============================] - 137s 452ms/step - loss: 1.8552
303/303 [==============================] - 137s 451ms/step - loss: 1.8529
303/303 [==============================] - 131s 431ms/step - loss: 1.8472
303/303 [==============================] - 108s 355ms/step - loss: 1.8511
303/303 [==============================] - 114s 377ms/step - loss: 1.8542
303/303 [==============================] - 130s 427ms/step - loss: 1.8613
303/303 [==============================] - 136s 448ms/step - loss: 1.8615
303/303 [==============================] - 136s 449ms/step - loss: 1.8576
303/303 [==============================] - 136s 450ms/step - loss: 1.8571
303/303 [==============================] - 137s 450ms/step - loss: 1.8624
303/303 [==============================] - 136s 448ms/step - loss: 1.8618
303/303 [==============================] - 136s 448ms/step - loss: 1.8630
303/303 [==============================] - 136s 450ms/step - loss: 1.8634
303/303 [==============================] - 136s 449ms/step - loss: 1.8669
303/303 [==============================] - 414s 1s/step - loss: 1.8681
303/303 [==============================] - 131s 431ms/step - loss: 1.8684
303/303 [==============================] - 132s 436ms/step - loss: 1.8729
303/303 [==============================] - 131s 432ms/step - loss: 1.8676
303/303 [==============================] - 132s 437ms/step - loss: 1.8731
303/303 [==============================] - 136s 448ms/step - loss: 1.8727
303/303 [==============================] - 135s 447ms/step - loss: 1.8732
303/303 [==============================] - 135s 446ms/step - loss: 1.8793
303/303 [==============================] - 136s 450ms/step - loss: 1.8736
303/303 [==============================] - 123s 406ms/step - loss: 1.8701
303/303 [==============================] - 109s 360ms/step - loss: 1.8735
303/303 [==============================] - 115s 378ms/step - loss: 1.8778
303/303 [==============================] - 133s 440ms/step - loss: 1.8778
303/303 [==============================] - 135s 445ms/step - loss: 1.8840
303/303 [==============================] - 135s 446ms/step - loss: 1.8865
303/303 [==============================] - 135s 446ms/step - loss: 1.8809
303/303 [==============================] - 136s 447ms/step - loss: 1.8833
303/303 [==============================] - 132s 436ms/step - loss: 1.8838
303/303 [==============================] - 135s 446ms/step - loss: 1.8865
303/303 [==============================] - 135s 445ms/step - loss: 1.8916
303/303 [==============================] - 135s 445ms/step - loss: 1.8906
Model saved to ./model_gru_200ep/best_model.h5
Tokenizer saved to ./model_gru_200ep/tokenizer.pkl

real    503m0.727s
user    5531m42.946s
sys     318m6.858s
2025-06-22 07:38:12.796805: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-22 07:38:12.796824: I tensorflow/stream_executor/cuda/cudart_stub.cc:29] Ignore above cudart dlerror if you do not have a GPU set up on your machine.
2025-06-22 07:38:15.647034: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:936] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2025-06-22 07:38:15.647184: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudart.so.11.0'; dlerror: libcudart.so.11.0: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-22 07:38:15.647217: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublas.so.11'; dlerror: libcublas.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-22 07:38:15.647242: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcublasLt.so.11'; dlerror: libcublasLt.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-22 07:38:15.647268: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcufft.so.10'; dlerror: libcufft.so.10: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-22 07:38:15.680848: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcusparse.so.11'; dlerror: libcusparse.so.11: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-22 07:38:15.680910: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory; LD_LIBRARY_PATH: /home/ye/miniforge3/envs/img2txt/lib/python3.8/site-packages/cv2/../../lib64:/usr/local/lib:/usr/local/lib:
2025-06-22 07:38:15.680920: W tensorflow/core/common_runtime/gpu/gpu_device.cc:1850] Cannot dlopen some GPU libraries. Please make sure the missing libraries mentioned above are installed properly if you would like to use GPU. Follow the guide at https://www.tensorflow.org/install/gpu for how to download and setup the required libraries for your platform.
Skipping registering GPU devices...
2025-06-22 07:38:15.681131: I tensorflow/core/platform/cpu_feature_guard.cc:151] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Dataset download complete.
Loading precomputed features...
Loaded features for 31783 images
Found 31783 images in ./data/flickr30k_images/Images
Sample image paths: ['./data/flickr30k_images/Images/435802277.jpg', './data/flickr30k_images/Images/216594524.jpg', './data/flickr30k_images/Images/5543458745.jpg']
Common images with both features and captions: 8092
Model loaded from ./model_gru_200ep/best_model.h5
Evaluating: 100%|████████████████████████████████████████████████████████████████████████████████████| 810/810 [18:03<00:00,  1.34s/it]

Evaluation Metrics:
bleu1: 0.2292
bleu2: 0.1274
bleu4: 0.0327
chrf: 0.2064
semantic_similarity: 0.1122
keyword_overlap: 0.2773
composite_score: 0.1617
cider: 0.0003
rouge1: 0.1840
rouge2: 0.0395
rougeL: 0.1530
Results saved to ./model_gru_200ep/evaluation_results.txt

real    18m12.082s
user    19m52.065s
sys     1m17.014s
```

## For Detail Analysis  

GRU, 200 epoch နဲ့ ဆောက်ထားတဲ့ မော်ဒယ်ကို သုံးပြီး test လုပ်ထားတဲ့ ရလဒ်...  

```
Evaluation Metrics:
BLEU-1: 0.2292
BLEU-2: 0.1274
BLEU-4: 0.0327
chrF: 0.2064
CIDEr: 0.0003
ROUGE-1: 0.1840
ROUGE-2: 0.0395
ROUGE-L: 0.1530
Semantic Similarity: 0.1122
Keyword Overlap: 0.2773
Composite Score: 0.1617

Sample Results:

Image ID: 436015762
Actual Captions:
1. a man prepares to enter the red building .
2. a man walking around the corner of a red building .
3. a man walks past a red building with a fake rocket attached to it .
4. a man walks under a building with a large rocket shaped sculpture .
5. a person walking by a red building with a jet on top of it .
Predicted Caption: startseq suits and a dog are running around a track with people in the background and building in the background with a person in the foreground watch him climb in the air at night and handrail on a pumpkin
Semantic Analysis:
- similarity: 0.0873
- keyword_overlap: 0.2692
- composite_score: 0.1419

Image ID: 436393371
Actual Captions:
1. a brown doberman is outside with a stick in its mouth .
2. a brown dog shows his teeth .
3. a dog bites a stick .
4. a dog is biting a twig .
5. a dog with sharp teeth is chewing on a stick outside .
Predicted Caption: startseq dog sniffing recently bubble a piece of blue and white flowers in the grass and a larger dog looks on the fence at the camera while another dog looks on the ground in the grass behind him in
Semantic Analysis:
- similarity: 0.2013
- keyword_overlap: 0.1538
- composite_score: 0.1870

Image ID: 436608339
Actual Captions:
1. a couple posing in front of a picture wall
2. an adult couple pose by a cardboard cut out for a movie .
3. an asian couple are standing by a fantasy poster .
4. an asian couple stands near a wax figure .
5. one person in a brown suit with his arm around another in a hat by a wall .
Predicted Caption: startseq people are gathered outside a building with columns at them call in the background with skyscrapers in the background of a restaurant and a greenhouse of them embrace on the wall with a tv in the foreground with
Semantic Analysis:
- similarity: 0.0389
- keyword_overlap: 0.2400
- composite_score: 0.0992

Image ID: 437054333
Actual Captions:
1. a bus filled with passengers in chicago at night .
2. a bus full of people waiting at a stop .
3. people are sitting on a bus .
4. people in a bus which is heading to 84 peterson .
5. there are people sitting on a bus that is labeled 84 peterson .
Predicted Caption: startseq spills of a bus stop to music in a line of art restaurant station past a mcdonalds restaurant window can see the photographs of the dining building machines smile at the camera while a woman stands behind her
Semantic Analysis:
- similarity: 0.0933
- keyword_overlap: 0.2258
- composite_score: 0.1330

Image ID: 437404867
Actual Captions:
1. a woman is sitting on a sidewalk with a cellphone at her ear .
2. a woman rests on the curb of a city street while talking on her cellphone .
3. a woman sits on the curb while talking on her cellphone .
4. a woman sits on the edge of a sidewalk with a garbage bin beside her
5. woman sits on the curb talking on a cellphone .
Predicted Caption: startseq meat table of electrical equpiment on a railing while seen from a turn in a skate park while people watch from behind them for a picture nearby a restaurant with a tv in the background with handlers dressed
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2000
- composite_score: 0.0600

Image ID: 437527058
Actual Captions:
1. a caravan of snowmobile travel through the snow .
2. a pair of people in heavy winter jackets rides through the snow on a snowmobile .
3. people riding something in the snow .
4. person on a polaris ski mobile in the snow .
5. the man wearing a blue helmet is riding a polaris .
Predicted Caption: startseq helmet and a dog are walking through snow in the snow behind them with snow nearby camera in the background and another dog smiles directly behind them in the snow from the snow covers them in the snow
Semantic Analysis:
- similarity: 0.3723
- keyword_overlap: 0.2727
- composite_score: 0.3424

Image ID: 437917001
Actual Captions:
1. a dark colored man is laying on newspapers by a metal railing with his shoes off .
2. a homeless man is lying on the ground with his stuff strewn around .
3. a homeless man is sleeping outside at the top of a staircase .
4. an man is sleeping on top of his clothes on concrete stairs .
5. man sleeping on the street .
Predicted Caption: startseq hands of a man in a batman jacket sitting on the sidewalk next to a large painting of flowers and flowers on its back is sitting on the sidewalk next to a red and red banner with a
Semantic Analysis:
- similarity: 0.0799
- keyword_overlap: 0.2917
- composite_score: 0.1435

Image ID: 438639005
Actual Captions:
1. a boy in red and a girl pink are walking through a low cut field .
2. the little boy and little girl are walking side by side .
3. two small children walk away in a field .
4. two small children walking in a field .
5. two young children are walking across an open field .
Predicted Caption: startseq man teeing off nearby a large white dog with a frisbee in his mouth in the field of a white house in a grassy field with a hurdle in the background two people watch him fall on the
Semantic Analysis:
- similarity: 0.1169
- keyword_overlap: 0.1852
- composite_score: 0.1374

Image ID: 439037721
Actual Captions:
1. two men sitting on the bank of a lake with an ice chest .
2. two people having a picnic by a lake .
3. two people having a picnic by the shore .
4. two people sitting on grass in front of a lake looking at the sky .
5. two people with hats looking at a lake while sitting on a yellow-grassed hill .
Predicted Caption: startseq biking through heavy sand while a racetrack behind them turns around in the sand beside him turns around in the air while the sun sets on the ground behind him and a cart in the background watch him
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2000
- composite_score: 0.0600

Image ID: 439049388
Actual Captions:
1. people , possibly fishermen , with their boats in shadow on shore at an orangesunset
2. a man in an orange vest is standing next to a yellow canoe .
3. people tend canoes at the edge of a body of water during a dimly lit time of day .
4. the men are getting their kayaks secured on the beach for the night .
5. two men standing on the shore beside their kayaks at dusk .
Predicted Caption: startseq in midair center of the painting of a fan in the air at sunset in the background with people guarding him stand in the background with graffiti covered in graffiti covered landscape behind them in background dressed in
Semantic Analysis:
- similarity: 0.0293
- keyword_overlap: 0.2917
- composite_score: 0.1080

Image ID: 439492931
Actual Captions:
1. a cluster of four brown dogs play in a field of brown grass .
2. four dogs are together in the field of dry grass .
3. four dogs in a grassy area .
4. four medium-sized dogs wrestle with each other on a grass field .
5. four small dogs play outside .
Predicted Caption: startseq dog herding sheep through field of animals in rural area with woods in the background two two dogs are chasing a red and white dog in the grass with a small dog in the background and table nearby
Semantic Analysis:
- similarity: 0.2079
- keyword_overlap: 0.4074
- composite_score: 0.2677

Image ID: 439569646
Actual Captions:
1. a girl is hiding behind a painted wooden structure inside a building .
2. a little girl with a red dress facing a panel with her back to the camera .
3. a young blonde girl wearing a red dress kneeling on a red carpet .
4. a young girl faces a white and black wall in a red-carpeted room .
5. girl kneeling on a red carpet .
Predicted Caption: startseq two girls are sitting on a bed laughing and laughing on a wood floor and a small girl is lying on her arm outstretched arms in a room with her mouth outstretched and laughs while a man in
Semantic Analysis:
- similarity: 0.0767
- keyword_overlap: 0.3333
- composite_score: 0.1537

Image ID: 439916996
Actual Captions:
1. brown dogs and a woman in a yard
2. a brown dog persues a frisbee across the grass as the thrower watches .
3. a woman in a blue jacket watches as her two brown dogs play with a red ball in a grassy yard .
4. a woman throws a frisbee for her two brown dogs to chase .
5. a woman watches a brown dog run away from a house across the grass .
Predicted Caption: startseq shot of a fence in a grassy area with a fence behind him in the background two people watch him fall from behind him in the background two vegetation building watch him from behind him in the background
Semantic Analysis:
- similarity: 0.0109
- keyword_overlap: 0.3500
- composite_score: 0.1127

Image ID: 440184957
Actual Captions:
1. a clown shares cut-out pictures of children .
2. a dirty looking clown holding up two paper cut outs of children with blond hair
3. a man wearing a balloon hat and a grassy shirt holds up two large paper dolls .
4. a man wearing a balloon hat holds up colored cut-out drawings of two men .
5. the man wears balloons on his head and holds paper people .
Predicted Caption: startseq a man in a black shirt and cap is jumping over a gate fence in a busy city park with other people in the background and him passes by graffiti covered walls in the background watch him and
Semantic Analysis:
- similarity: 0.0687
- keyword_overlap: 0.2500
- composite_score: 0.1231

Image ID: 440190907
Actual Captions:
1. a group of people walk through a shopping mall .
2. many people walk through the store .
3. people browse in a store .
4. people strolling through an indoor market .
5. the shoppers are walking in a store .
Predicted Caption: startseq people stand inside a restaurant there has a candles dressed in jackets in a parade lit behind it to a sign that says fayre sign behind him from behind him in background chairs lit of statue of a
Semantic Analysis:
- similarity: 0.0796
- keyword_overlap: 0.1481
- composite_score: 0.1002

Image ID: 440737340
Actual Captions:
1. a black man with a red mask is carrying a box .
2. a man in a domino mask carries an amplifier up a hill .
3. a man with a mask carrying a black speaker
4. a masked man in bright clothing carrying a large box .
5. black man lifting black box is watched by black dog .
Predicted Caption: startseq tattoos sitting on a bench next to a wood wall with a toddler in the background two people look on the side of a wooden ice statue of a city that they look on the edge of them
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.1071
- composite_score: 0.0321

Image ID: 441212506
Actual Captions:
1. the black dog runs with a ball with two smaller dogs behind it .
2. three dogs playing in a field , one with a ball in its mouth .
3. three dogs race towards the viewer over a lawn .
4. three dogs running in grass , one carrying a tennis ball in mouth .
5. two small dogs follow a larger dog with a tennis ball
Predicted Caption: startseq dog with a frisbee rolling in the air with a ball in its mouth in the background two black and white dog are running on the grass near the ocean with a large dog in the background rain
Semantic Analysis:
- similarity: 0.2313
- keyword_overlap: 0.4800
- composite_score: 0.3059

Image ID: 44129946
Actual Captions:
1. a couple watches a boat against a skyline .
2. a man and woman sit on a bench , watching a boat go by .
3. the sun is setting while a man and woman watch a boat go by .
4. two people sit on a bench and watch a boat on the water .
5. two people watching a boat sail past .
Predicted Caption: startseq enjoy a coaster enjoying a docked on a lake with a dog on the driver 's back to the ocean below him take off camera from the water from the water from the water while the sun sets
Semantic Analysis:
- similarity: 0.0652
- keyword_overlap: 0.2308
- composite_score: 0.1149

Image ID: 441398149
Actual Captions:
1. a female jogger wearing red .
2. a girl with headphones is running next to some street signs .
3. a woman in a red outfit is jogging next to several street signs .
4. a woman jogging across an intersection .
5. the lady in red shorts jogs near a stop sign while listening to music .
Predicted Caption: startseq prevent the camera is being cheered on by a passerby and a boy in a tracksuit on a skateboard in front of a brick wall with graffiti on the ground behind him buildings in the background whilst other
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.1724
- composite_score: 0.0517

Image ID: 441817653
Actual Captions:
1. a bearded man wearing a denim jacket and a hat sits on a park bench
2. a bearded man wearing a denim jacket sits on a bench .
3. a man with a bushy beard and a baseball cap sits on a park bench .
4. an old man with a long beard and jean jacket sits on a park bench .
5. an old man with a long white beard , glasses , and a hat is sitting on a park bench .
Predicted Caption: startseq a woman wearing a white hat and sunglasses is holding a camera with a video camera in her mouth while a man in a blue shirt sits on a chair return to kiss the camera in her hand
Semantic Analysis:
- similarity: 0.1417
- keyword_overlap: 0.3571
- composite_score: 0.2063

Image ID: 441921713
Actual Captions:
1. a bird lands on a mans glove .
2. a man holds a bird .
3. a man holds a falcon on his arm .
4. gloved man holding a bird of prey .
5. the man is wearing gloves and holding a hawk in his hands .
Predicted Caption: startseq a man in a black and black jacket is standing in a stadium with his dog on the left has a red and red bicycle on the street with a dog in the background with other people behind
Semantic Analysis:
- similarity: 0.0727
- keyword_overlap: 0.3333
- composite_score: 0.1509

Image ID: 442220883
Actual Captions:
1. a brown dog has a white toy in its mouth .
2. a dog holding a white stuffed animal .
3. a tan dog hangong on to a white plushie toy .
4. a yellow dog is chewing on a white stuffed toy .
5. the dog is holding a stuffed toy in his mouth .
Predicted Caption: startseq open dog is licking its nose while standing on a grassy area with cloth jar on it is looking at the camera while the dogs watch him shop is in the background with a blue blanket on its
Semantic Analysis:
- similarity: 0.0730
- keyword_overlap: 0.2414
- composite_score: 0.1235

Image ID: 442594271
Actual Captions:
1. a bunch of people at the beach .
2. people are enjoying a sunny day on a sandy beach by the ocean .
3. people are on the beach and there is a kite in the air .
4. people on the beach and a kite in the sky .
5. sandy beach , people walking , laying , sitting , a kite is flying .
Predicted Caption: startseq on the beach jockeys a family stands on the beach with a identical clouds and water crashing in the distance and a sandy track behind them to kicked the water all on twilight in the water and the
Semantic Analysis:
- similarity: 0.1657
- keyword_overlap: 0.2917
- composite_score: 0.2035

Image ID: 442918418
Actual Captions:
1. a brown dog is jumping over a fallen tree in the woods .
2. a small tan dog jumps over a small log .
3. tan colored dog jumping over a branch in the forest .
4. the dog leaps over the log in the forest .
5. the white dog is jumping over a fallen tree .
Predicted Caption: startseq dog chasing a tennis ball in a fenced in area with a small dog jumping in the background of a white dog with a log in the background play frame on the grass near a tree table in
Semantic Analysis:
- similarity: 0.4166
- keyword_overlap: 0.3750
- composite_score: 0.4041

Image ID: 443430496
Actual Captions:
1. a brown dog swimming in murky water .
2. a brown dog swims in the murky water .
3. a dog with yellow fur swims , neck deep , in water .
4. a golden retreiver swimming in the water .
5. a yellow dog is swimming in the water .
Predicted Caption: startseq dog running through water in water with a stick in its mouth in the water one dog is jumping in the water and a blue ball is falling into the water and it is swimming in the ocean
Semantic Analysis:
- similarity: 0.5445
- keyword_overlap: 0.3478
- composite_score: 0.4855

Image ID: 443885436
Actual Captions:
1. a tan curly haired dog jumps in the snow with a stick in its mouth .
2. a white dog catches a stick in the snow .
3. a white dog holds a stick in its mouth while it runs through snow .
4. a white dog jumps in the snow .
5. a white dog with light brown markings has a stick in his mouth and his paws in the snow .
Predicted Caption: startseq dog running through snow covered ground in snow covered area with trees in the background behind him in the snow covered trees behind him watch him look on the mountain beside them covered in snow look on the
Semantic Analysis:
- similarity: 0.2244
- keyword_overlap: 0.2857
- composite_score: 0.2428

Image ID: 444047125
Actual Captions:
1. a person hiking at the foot of snowcapped mountains .
2. a person walks in the valley between tall mountains .
3. a person with a backpack and walking stick , walking towards the mountains in the valley below .
4. people with backpacks hiking in the mountains .
5. three people walk through a valley towards snowy mountains .
Predicted Caption: startseq siluettes of people clouds over a hill of pointy rocks and clouds and the surrounding of the cyclist goes toward him off a hill of water and mountains behind him to take a camera threw over the mountains
Semantic Analysis:
- similarity: 0.1902
- keyword_overlap: 0.2400
- composite_score: 0.2051

Image ID: 444057017
Actual Captions:
1. a little girl gets her picture taken while on the merry-go-round .
2. a little girl in pink clothes holding yellow rods .
3. a little girl on a piece of playground equipment
4. a little girl sitting on a playground ride .
5. a young girl looks up as she rides on a merry-go-round .
Predicted Caption: startseq playground scooter on a swing set with a colorful creature of a fence in the background and a silver ring shaped jack park watch him shop on the ground giving him make a basket in the air and
Semantic Analysis:
- similarity: 0.0275
- keyword_overlap: 0.2069
- composite_score: 0.0813

Image ID: 444481722
Actual Captions:
1. a dark skinned man walks by a woman talking on a cellphone .
2. a male walking and a female talking on the phone beside the concrete building .
3. people stand outside near a concrete wall and a window .
4. two people standing on the sidewalk .
5. two women , one carrying a purse and papers , are standing on a sidewalk .
Predicted Caption: startseq a skater is performing a jump on a skateboard in front of a building taking a shot of quickly on a city wall while others passing by a bar in a city park area while a group of
Semantic Analysis:
- similarity: 0.0382
- keyword_overlap: 0.2000
- composite_score: 0.0867

Image ID: 444803340
Actual Captions:
1. a guy and a girl , both wearing white shirts and jeans , stand under a flowering tree .
2. a man and a woman are talking in a park
3. a man and woman standing underneath the tree are talking .
4. a man in a white shirt is standing in the grass showing something to a woman in a white shirt .
5. a young couple both wearing white shirts and blue jeans standing in a light misty rain
Predicted Caption: startseq dresses is standing outside a building with a lot of people in the background with buckets of a porch on a sunny day in a wooded area with a woman in a black jacket and a white shirt
Semantic Analysis:
- similarity: 0.1866
- keyword_overlap: 0.3333
- composite_score: 0.2306

Image ID: 444845904
Actual Captions:
1. a man in a yellow helmet climbs a cliff face , snow behind him .
2. a man is climbing up a wall with a rope
3. a man leans back while climbing a mountain tethered to a rope .
4. he is rock climbing .
5. man with helmet rock climbing in a snowy area .
Predicted Caption: startseq snow motorcycle riding through the snow ejected off a snowy slope whilst being watched by a cyclist about to be seen from behind him in the background with many visible in the background of mountains in the background
Semantic Analysis:
- similarity: 0.0435
- keyword_overlap: 0.2667
- composite_score: 0.1105

Image ID: 444872454
Actual Captions:
1. a group of students dressed in sweatshirts and jackets head towards the right .
2. a group of students walking on campus , some carrying books .
3. a group of students walk together .
4. a group of young people are walking through a park under blossoming trees .
5. several young women walk near blossoming cherry trees .
Predicted Caption: startseq people gather in a run road at a party party shot with skyscrapers in the background like a group of people watching something in the background with a crowd of mountains in the background watch from behind a
Semantic Analysis:
- similarity: 0.0837
- keyword_overlap: 0.2500
- composite_score: 0.1336

Image ID: 444881000
Actual Captions:
1. a group of college students walk in nice weather .
2. a group of people walk in the park , while some talk on phones .
3. a group of students are walking through the campus .
4. a group of young people walking with two talking on cellphones .
5. several young people walking casually around
Predicted Caption: startseq uniformed women walk through a grassy area with a dog and a silver car parked nearby a bench in a parking lot covered in grass with trees and mountains in background watch him behind them in the background
Semantic Analysis:
- similarity: 0.0290
- keyword_overlap: 0.2069
- composite_score: 0.0824

Image ID: 445148321
Actual Captions:
1. a person in the distance hikes among hoodoos with stars visible in the sky .
2. a person standing on a ridge in the desert .
3. interesting rock formations in the desert landscape , with stars above .
4. the night sky in the desert .
5. there is a person standing a mountain that has some interesting shapes .
Predicted Caption: startseq chairlift occupied by two people are walking through a wooded area framed formations behind them ends of ends of a hillside with snow flying in the background behind them ends in the air of a mountain range in
Semantic Analysis:
- similarity: 0.0311
- keyword_overlap: 0.2143
- composite_score: 0.0861

Image ID: 445655284
Actual Captions:
1. a black and brown dog walks through the snow near a building .
2. a black dog , running in the snow .
3. a black dog running in the snow by some trees .
4. a large black and tan dog is running across the snow in a wooded area .
5. the black and brown dog is running through the snow .
Predicted Caption: startseq dog in snow and a 5 dog rolls in the snow and snow runs in snow covered ground in the background with trees in the background with trees in the background behind him in the snow and winter
Semantic Analysis:
- similarity: 0.3771
- keyword_overlap: 0.3889
- composite_score: 0.3806

Image ID: 445861800
Actual Captions:
1. three men walking on a sidewalk in a city .
2. three people are walking down the street with cars and buildings in the background .
3. three people stand along a main road .
4. three people walking on a sidewalk with 3 light colored cars in the background .
5. three people wearing winter clothes standing on the sidewalk near a street
Predicted Caption: startseq busy busy street with signs for traffic behind him on the crosswalk with a silver car parked past them painted on the street he can see in the background with a silver purse on it in the background
Semantic Analysis:
- similarity: 0.1190
- keyword_overlap: 0.2692
- composite_score: 0.1640

Image ID: 446138054
Actual Captions:
1. a man in an orange hat jumping .
2. a man jumps in the middle of a rocky desert .
3. a man wearing a white shirt and an orange shirt jumped into the air .
4. man in khaki pants does elaborate kick in desert
5. man jumping with a rock formation in background .
Predicted Caption: startseq water park climb over a rock wall where water in the mud are watching the camera in the ocean below him kelp in the background with a smoke behind them in frame on the beach in front of
Semantic Analysis:
- similarity: 0.0328
- keyword_overlap: 0.2414
- composite_score: 0.0954

Image ID: 446286714
Actual Captions:
1. an elderly man is sitting on a bench .
2. an older man wearing a brown coat siting on a bench .
3. an old man in a coat and hat sitting on a park bench .
4. old man in tan jacket and black cap sitting on bench
5. the older man with the shopping bag and cane is sitting on a bench .
Predicted Caption: startseq dresses says police officer and a man in a black shirt are standing in front of a building with a body of water in the background and trees to the right of them grabs a crowd behind them
Semantic Analysis:
- similarity: 0.0859
- keyword_overlap: 0.2500
- composite_score: 0.1351

Image ID: 446291803
Actual Captions:
1. these woman are watching people play tennis from a bench .
2. two individuals watch a tennis match .
3. two people sit on a park bench while watching a neighborhood tennis match .
4. two people with red scarves on their heads are watching tennis .
5. two women sitting on a bench in front of a tennis court near a building complex .
Predicted Caption: startseq construction worker with a martial arts bag and black pants run down a street covered with graffiti on it and walls in front of a flag door and graffiti to banner behind him and a banner in a
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2143
- composite_score: 0.0643

Image ID: 446514680
Actual Captions:
1. two brown dogs are fighting and they are both wearing red .
2. two brown dogs rough house outside .
3. two brown dogs wearing red collars look at each other while running along a dirt field .
4. two dogs play together .
5. two large brown short haired dogs with collars play chase in a field .
Predicted Caption: startseq dog shaking off smaller little boy in the background two two black one dog waits to chase another dog on the beach near the ocean with a cover of them in the background and sea stand nearby building
Semantic Analysis:
- similarity: 0.0112
- keyword_overlap: 0.1935
- composite_score: 0.0659

Image ID: 447111935
Actual Captions:
1. the two greyhound dogs wearing sweaters are playing in the grass .
2. two dogs play in the grass .
3. two dogs wearing shirts play in the green grass .
4. two dogs wearing sweaters play in a field .
5. two dogs wearing sweaters play in the grass .
Predicted Caption: startseq dog with a red toy in its mouth and a black and black dog running through the grass with a ball in its mouth mouth open over the woods in front of a fence of gravel path in
Semantic Analysis:
- similarity: 0.0434
- keyword_overlap: 0.1667
- composite_score: 0.0804

Image ID: 447722389
Actual Captions:
1. a brown and white dog is jumping high and catching a blue ball .
2. a dog is jumping and catching a small , blue ball in a park surrounded by two other dogs .
3. a dog jumps and catches a blue ball in his mouth .
4. a dog jumps in the air to catch a blue ball .
5. three dogs run on grass , one leaps to catch blue ball .
Predicted Caption: startseq dog running through the woods with a ball in its mouth jumping in the grass with a white toy in his mouth and a white dog follows shortly after a ball in his mouth in the grass with
Semantic Analysis:
- similarity: 0.3622
- keyword_overlap: 0.5238
- composite_score: 0.4107

Image ID: 447733067
Actual Captions:
1. a girl in a skimpy bikini outfit walks and carries a helmet .
2. a scantily clad girl , in a helmet , walks away from the camera , down a busy sidewalk .
3. a woman wearing a helmet , tall boots , and short shorts walks down the street .
4. girl in bikini bottoms , boots and a helmet walking away at a street fair .
5. the woman in the purple bikini and pink top is wearing a safety helmet .
Predicted Caption: startseq 2 girls in summer clothes are dancing in a circle with silly arms stretched out on the street aside a view of water balloons toss a bottled pole in the streets with a crowd of people in ornamental
Semantic Analysis:
- similarity: 0.0240
- keyword_overlap: 0.1333
- composite_score: 0.0568

Image ID: 447800028
Actual Captions:
1. a black dog playing with a purple toy in the snow .
2. a black dog runs through the snow carrying a blue toy .
3. a dog plays in the snow .
4. dog running with a purple toy in the snowy field .
5. the black and brown dog carries a purple toy in the snow .
Predicted Caption: startseq black dog running through snow covered ground all in snow covered ground all around him runs in the snow covered ground behind him in the snow covered ground behind him in the snow covered ground behind him in
Semantic Analysis:
- similarity: 0.2433
- keyword_overlap: 0.5333
- composite_score: 0.3303

Image ID: 448252603
Actual Captions:
1. a boy pointing in a direction on a dirt road .
2. a boy with a backpack sits on a trail and points .
3. a man points his finger to the path ahead as he sits on the dirt path .
4. a man with a backpack is sitting in a dirt road and pointing toward the horizon .
5. a young man sitting in the middle of a dirt road pointing up the road .
Predicted Caption: startseq dog and owner are sitting on a mound stump in the woods and a playhouse is behind them for the presidential candidate and the sun shines behind him make a walk along a dirt path in the snow
Semantic Analysis:
- similarity: 0.1236
- keyword_overlap: 0.3103
- composite_score: 0.1796

Image ID: 448257345
Actual Captions:
1. a dog is staring at the food in the plate of a person eating .
2. a person holding a dog while they eat .
3. a person is eating a plate of pasta with a black and brown dog on his or her lap .
4. a person is eating pasta , while a dog is watching .
5. someone in a blue and white striped sweater is eating and the dog next to them is interested in their food .
Predicted Caption: startseq bed with two brown dogs are hugging each other in a bed with a blue blanket on a bed of ice cream leaves in the background and watch him watch it listening to music in their mouth in
Semantic Analysis:
- similarity: 0.0226
- keyword_overlap: 0.3667
- composite_score: 0.1258

Image ID: 44856031
Actual Captions:
1. a brown dog is sprayed with water .
2. a dog is being squirted with water in the face outdoors .
3. a dog stands on his hind feet and catches a stream of water .
4. a jug is jumping up it is being squirted with a jet of water .
5. a tan , male dog is jumping up to get a drink of water from a spraying bottle .
Predicted Caption: startseq dog trotting through grass in fenced yard in cut mouth in background two other dogs are running in the grass with a fence behind it in the background a building watches from behind him in the background watch
Semantic Analysis:
- similarity: 0.0531
- keyword_overlap: 0.2593
- composite_score: 0.1149

Image ID: 448590900
Actual Captions:
1. a brown dog is sniffing around green grass on a hill .
2. a dog is digging a field .
3. a dog stands in a large , grassy field .
4. a dog walks alone in a field .
5. a dog with a red harness tracks a scent in a field .
Predicted Caption: startseq horse and dog running through a field of grass and trees look on the edge of a field of grass spotted trees in a field of grass and trees shirts in the distance with a fence behind him
Semantic Analysis:
- similarity: 0.3291
- keyword_overlap: 0.3043
- composite_score: 0.3217

Image ID: 448658518
Actual Captions:
1. a large man dressed in black on a street corner by a red brick building .
2. a man dressed in black is waiting at a crosswalk .
3. a man dressed in black stands at a street corner near a crossing light .
4. a man stands at a traffic light , waiting to cross the street .
5. man in black waits at crossing signal near large brick building .
Predicted Caption: startseq a boy is doing a trick on a skateboard at a skate park night in a public area while a crowd watches from a scene in the background gloves watch him washes lines eat her arms in the
Semantic Analysis:
- similarity: 0.0000
- keyword_overlap: 0.2000
- composite_score: 0.0600

Image ID: 448916362
Actual Captions:
1. a dog is running through a field with its tongue hanging out .
2. a dog runs with his tongue hanging out .
3. a dog with its mouth open is running .
4. brown and cream dog with tongue out
5. the white and black dog runs on the field with his tongue hanging out .
Predicted Caption: startseq dog with a red frisbee in its mouth running through the grass with a ball in its mouth jumping over a field of flowers in the background two white dogs follow him in the air while chasing a
Semantic Analysis:
- similarity: 0.2129
- keyword_overlap: 0.3571
- composite_score: 0.2562

```

