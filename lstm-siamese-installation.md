# LSTM-Siamese-Text-Similarities-Installation

Some notes of installation/training of LSTM based Siamese Network for my PhD student Myint Myint Htay (UTYCC).  
အရင်ဆုံး ```git clone https://github.com/amansrivastava17/lstm-siamese-text-similarity``` လုပ်ခဲ့တယ်။   

## Creating a New Conda Environment

Tensorflow framework နဲ့ Keras ကိုလည်း သုံးထားတာမို့၊ ကောင်းတာက အရင်ဆုံး conda environment အသစ်လုပ်ပြီး ဖြစ်နိုင်သ၍ သုံးမယ့် lstm-siamese code က သုံးထားတဲ့ library လိုအပ်ချက်တွေကို ပြင်ဆင်တာက ကောင်းတာမို့ ...   
အရင်ဆုံး conda command ကို သုံးပြီး tensor1.15.4_keras2.2.4 ဆိုတဲ့ environment ကို create လုပ်ခဲ့တယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ conda create --name tensor1.15.4_keras2.2.4 python=3.6
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4

  added / updated specs:
    - python=3.6


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  ca-certificates    pkgs/main/linux-64::ca-certificates-2020.10.14-0
  certifi            pkgs/main/noarch::certifi-2020.6.20-pyhd3eb1b0_3
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
  libedit            pkgs/main/linux-64::libedit-3.1.20191231-h14c3975_1
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1h-h7b6447c_0
  pip                pkgs/main/linux-64::pip-20.2.4-py36h06a4308_0
  python             pkgs/main/linux-64::python-3.6.12-hcff3b4d_2
  readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
  setuptools         pkgs/main/linux-64::setuptools-50.3.1-py36h06a4308_1
  sqlite             pkgs/main/linux-64::sqlite-3.33.0-h62c20be_0
  tk                 pkgs/main/linux-64::tk-8.6.10-hbc83047_0
  wheel              pkgs/main/noarch::wheel-0.35.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate tensor1.15.4_keras2.2.4
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

conda activate လုပ်ပြီး အသစ်ဆောက်ထားတဲ့ python environment ထဲ ဝင်ပါ။  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ conda activate tensor1.15.4_keras2.2.4
```

လိုအပ်တဲ့ library တွေကို pip command နဲ့ requirements.txt ဖိုင်ကို သုံးပြီး ကိုယ့်စက်ထဲမှာ installation လုပ်ပါ။  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ ls
config.py      images       inputHandler.py  model.py   requirements.txt
controller.py  __init__.py  LICENSE          README.md  sample_data.csv
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ pip install -r requirements.txt 
Collecting tensorflow==1.15.4
  Using cached tensorflow-1.15.4-cp36-cp36m-manylinux2010_x86_64.whl (110.5 MB)
Collecting tensorboard==1.12.0
  Downloading tensorboard-1.12.0-py3-none-any.whl (3.0 MB)
     |████████████████████████████████| 3.0 MB 441 kB/s 
Collecting pandas==0.23.4
  Downloading pandas-0.23.4-cp36-cp36m-manylinux1_x86_64.whl (8.9 MB)
     |████████████████████████████████| 8.9 MB 562 kB/s 
Collecting Keras==2.2.4
  Downloading Keras-2.2.4-py2.py3-none-any.whl (312 kB)
     |████████████████████████████████| 312 kB 733 kB/s 
Collecting gensim==3.6.0
  Downloading gensim-3.6.0-cp36-cp36m-manylinux1_x86_64.whl (23.6 MB)
     |████████████████████████████████| 23.6 MB 87 kB/s 
Collecting astor>=0.6.0
  Using cached astor-0.8.1-py2.py3-none-any.whl (27 kB)
Collecting absl-py>=0.7.0
  Using cached absl_py-0.11.0-py3-none-any.whl (127 kB)
Requirement already satisfied: numpy<1.19.0,>=1.16.0 in /home/ye/.local/lib/python3.6/site-packages (from tensorflow==1.15.4->-r requirements.txt (line 1)) (1.18.1)
Requirement already satisfied: six>=1.10.0 in /home/ye/.local/lib/python3.6/site-packages (from tensorflow==1.15.4->-r requirements.txt (line 1)) (1.15.0)
Collecting opt-einsum>=2.3.2
  Using cached opt_einsum-3.3.0-py3-none-any.whl (65 kB)
Collecting keras-applications>=1.0.8
  Using cached Keras_Applications-1.0.8-py3-none-any.whl (50 kB)
Requirement already satisfied: wheel>=0.26; python_version >= "3" in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from tensorflow==1.15.4->-r requirements.txt (line 1)) (0.35.1)
Processing /home/ye/.cache/pip/wheels/93/2a/eb/e58dbcbc963549ee4f065ff80a59f274cc7210b6eab962acdc/termcolor-1.1.0-py3-none-any.whl
Collecting google-pasta>=0.1.6
  Using cached google_pasta-0.2.0-py3-none-any.whl (57 kB)
Collecting tensorflow-estimator==1.15.1
  Using cached tensorflow_estimator-1.15.1-py2.py3-none-any.whl (503 kB)
Collecting keras-preprocessing>=1.0.5
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Processing /home/ye/.cache/pip/wheels/32/42/7f/23cae9ff6ef66798d00dc5d659088e57dbba01566f6c60db63/wrapt-1.12.1-cp36-cp36m-linux_x86_64.whl
Collecting grpcio>=1.8.6
  Using cached grpcio-1.33.2-cp36-cp36m-manylinux2014_x86_64.whl (3.8 MB)
Processing /home/ye/.cache/pip/wheels/19/a7/b9/0740c7a3a7d1d348f04823339274b90de25fbcd217b2ee1fbe/gast-0.2.2-py3-none-any.whl
Collecting protobuf>=3.6.1
  Using cached protobuf-3.14.0-cp36-cp36m-manylinux1_x86_64.whl (1.0 MB)
Collecting markdown>=2.6.8
  Using cached Markdown-3.3.3-py3-none-any.whl (96 kB)
Collecting werkzeug>=0.11.10
  Using cached Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Requirement already satisfied: pytz>=2011k in /home/ye/.local/lib/python3.6/site-packages (from pandas==0.23.4->-r requirements.txt (line 3)) (2020.1)
Requirement already satisfied: python-dateutil>=2.5.0 in /home/ye/.local/lib/python3.6/site-packages (from pandas==0.23.4->-r requirements.txt (line 3)) (2.8.1)
Processing /home/ye/.cache/pip/wheels/e5/9d/ad/2ee53cf262cba1ffd8afe1487eef788ea3f260b7e6232a80fc/PyYAML-5.3.1-cp36-cp36m-linux_x86_64.whl
Collecting h5py
  Using cached h5py-3.1.0-cp36-cp36m-manylinux1_x86_64.whl (4.0 MB)
Collecting scipy>=0.14
  Using cached scipy-1.5.4-cp36-cp36m-manylinux1_x86_64.whl (25.9 MB)
Collecting smart-open>=1.2.1
  Using cached smart_open-3.0.0.tar.gz (113 kB)
Collecting importlib-metadata; python_version < "3.8"
  Using cached importlib_metadata-2.0.0-py2.py3-none-any.whl (31 kB)
Collecting cached-property; python_version < "3.8"
  Using cached cached_property-1.5.2-py2.py3-none-any.whl (7.6 kB)
Requirement already satisfied: requests in /home/ye/.local/lib/python3.6/site-packages (from smart-open>=1.2.1->gensim==3.6.0->-r requirements.txt (line 5)) (2.24.0)
Collecting zipp>=0.5
  Using cached zipp-3.4.0-py3-none-any.whl (5.2 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/.local/lib/python3.6/site-packages (from requests->smart-open>=1.2.1->gensim==3.6.0->-r requirements.txt (line 5)) (2020.6.20)
Requirement already satisfied: idna<3,>=2.5 in /home/ye/.local/lib/python3.6/site-packages (from requests->smart-open>=1.2.1->gensim==3.6.0->-r requirements.txt (line 5)) (2.10)
Requirement already satisfied: urllib3!=1.25.0,!=1.25.1,<1.26,>=1.21.1 in /home/ye/.local/lib/python3.6/site-packages (from requests->smart-open>=1.2.1->gensim==3.6.0->-r requirements.txt (line 5)) (1.25.10)
Requirement already satisfied: chardet<4,>=3.0.2 in /home/ye/.local/lib/python3.6/site-packages (from requests->smart-open>=1.2.1->gensim==3.6.0->-r requirements.txt (line 5)) (3.0.4)
Building wheels for collected packages: smart-open
  Building wheel for smart-open (setup.py) ... done
  Created wheel for smart-open: filename=smart_open-3.0.0-py3-none-any.whl size=107095 sha256=301372bcf3b4ffa64866b621ba95b49542963ea4d90bfb9d6d1f153a73ce5d02
  Stored in directory: /home/ye/.cache/pip/wheels/88/2a/d4/f2e9023989d4d4b3574f268657cb6cd23994665a038803f547
Successfully built smart-open
Installing collected packages: astor, protobuf, zipp, importlib-metadata, markdown, werkzeug, grpcio, tensorboard, absl-py, opt-einsum, cached-property, h5py, keras-applications, termcolor, google-pasta, tensorflow-estimator, keras-preprocessing, wrapt, gast, tensorflow, pandas, pyyaml, scipy, Keras, smart-open, gensim
  Attempting uninstall: pandas
    Found existing installation: pandas 1.1.2
    Uninstalling pandas-1.1.2:
      Successfully uninstalled pandas-1.1.2
ERROR: After October 2020 you may experience errors when installing or updating packages. This is because pip will change the way that it resolves dependency conflicts.

We recommend you use --use-feature=2020-resolver to test your packages with the new resolver before it becomes the default.

tensorflow 1.15.4 requires tensorboard<1.16.0,>=1.15.0, but you'll have tensorboard 1.12.0 which is incompatible.
Successfully installed Keras-2.2.4 absl-py-0.11.0 astor-0.8.1 cached-property-1.5.2 gast-0.2.2 gensim-3.6.0 google-pasta-0.2.0 grpcio-1.33.2 h5py-3.1.0 importlib-metadata-2.0.0 keras-applications-1.0.8 keras-preprocessing-1.1.2 markdown-3.3.3 opt-einsum-3.3.0 pandas-0.23.4 protobuf-3.14.0 pyyaml-5.3.1 scipy-1.5.4 smart-open-3.0.0 tensorboard-1.12.0 tensorflow-1.15.4 tensorflow-estimator-1.15.1 termcolor-1.1.0 werkzeug-1.0.1 wrapt-1.12.1 zipp-3.4.0
```

ဆရာ့စက်ထဲမှာတော့ အထက်မှာ ပြထားတဲ့ အတိုင်း tensorboard version က incompatible လို့ message ပေးခဲ့လို့ tensorboard ကို uninstall လုပ်ပြီး...  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ pip uninstall tensorboard
Found existing installation: tensorboard 1.12.0
Uninstalling tensorboard-1.12.0:
  Would remove:
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/bin/tensorboard
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/tensorboard-1.12.0.dist-info/*
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/tensorboard/*
Proceed (y/n)? y
  Successfully uninstalled tensorboard-1.12.0
```

tensorboard version 1.15.0 ကို installation ပြန်လုပ်ခဲ့...   
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ pip install tensorboard==1.15.0
Collecting tensorboard==1.15.0
  Using cached tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
Requirement already satisfied: protobuf>=3.6.0 in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from tensorboard==1.15.0) (3.14.0)
Requirement already satisfied: six>=1.10.0 in /home/ye/.local/lib/python3.6/site-packages (from tensorboard==1.15.0) (1.15.0)
Requirement already satisfied: wheel>=0.26; python_version >= "3" in /home/ye/tool/anaconda3/envs/tensor1.15.4_kerအထas2.2.4/lib/python3.6/site-packages (from tensorboard==1.15.0) (0.35.1)
Requirement already satisfied: numpy>=1.12.0 in /home/ye/.local/lib/python3.6/site-packages (from tensorboard==1.15.0) (1.18.1)
Requirement already satisfied: werkzeug>=0.11.15 in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from tensorboard==1.15.0) (1.0.1)
Requirement already satisfied: markdown>=2.6.8 in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from tensorboard==1.15.0) (3.3.3)
Requirement already satisfied: setuptools>=41.0.0 in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from tensorboard==1.15.0) (50.3.1.post20201107)
Requirement already satisfied: grpcio>=1.6.3 in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from tensorboard==1.15.0) (1.33.2)
Requirement already satisfied: absl-py>=0.4 in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from tensorboard==1.15.0) (0.11.0)
Requirement already satisfied: importlib-metadata; python_version < "3.8" in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from markdown>=2.6.8->tensorboard==1.15.0) (2.0.0)
Requirement already satisfied: zipp>=0.5 in /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages (from importlib-metadata; python_version < "3.8"->markdown>=2.6.8->tensorboard==1.15.0) (3.4.0)
Installing collected packages: tensorboard
Successfully installed tensorboard-1.15.0
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

## Got Error When Training with Sample Data

LSTM-Siamese model ကို training လုပ်ဖို့အတွက် ရှာကြည့်တော့ train-sample.py ဆိုတဲ့ python script ကိုရှာတွေ့လို့ အဲဒီ code နဲ့ တင်ပေးထားတဲ့ sample data ကို သုံးပြီး စမ်းကြည့်တော့ အောက်ပါအတိုင်း error တွေ့ရ...   
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ python ./train-sample.py 2>&1 | tee train-sample.log
Traceback (most recent call last):
  File "./train-sample.py", line 1, in <module>
    from model import SiameseBiLSTM
  File "/media/ye/project1/tool/lstm-siamese-text-similarity/model.py", line 2, in <module>
    from keras.layers import Dense, Input, LSTM, Dropout, Bidirectional
  File "/home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/__init__.py", line 3, in <module>
    from . import utils
  File "/home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/utils/__init__.py", line 5, in <module>
    from . import io_utils
  File "/home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/utils/io_utils.py", line 13, in <module>
    import h5py
  File "/home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/h5py/__init__.py", line 25, in <module>
    from . import _errors
  File "h5py/_errors.pyx", line 1, in init h5py._errors
AttributeError: module 'numpy' has no attribute 'dtype'
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

numpy library version ပြဿနာလို့ ထင်တယ်...   

## Remove numpy and Reinstall Lower Version

Version က မြင့်နေလို့ အဆင်မပြေတာလို့ နားလည်လိုက်လို့ လက်ရှိဗားရှင်းကို ဖြုတ်ခဲ့တယ်။  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ pip uninstall numpy
Found existing installation: numpy 1.18.1
Uninstalling numpy-1.18.1:
  Would remove:
    /home/ye/.local/lib/python3.6/site-packages/numpy-1.18.1.dist-info/*
    /home/ye/.local/lib/python3.6/site-packages/numpy/.libs/libgfortran-ed201abd.so.3.0.0
    /home/ye/.local/lib/python3.6/site-packages/numpy/.libs/libopenblasp-r0-34a18dc3.3.7.so
    /home/ye/.local/lib/python3.6/site-packages/numpy/core/tests/test_issue14735.py
    /home/ye/.local/lib/python3.6/site-packages/numpy/distutils/compat.py
    /home/ye/.local/lib/python3.6/site-packages/numpy/random/_bit_generator.cpython-36m-x86_64-linux-gnu.so
    /home/ye/.local/lib/python3.6/site-packages/numpy/random/_bit_generator.pxd
Proceed (y/n)? y
  Successfully uninstalled numpy-1.18.1
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ pip install numpy
Collecting numpy
  Downloading numpy-1.19.4-cp36-cp36m-manylinux2010_x86_64.whl (14.5 MB)
     |████████████████████████████████| 14.5 MB 381 kB/s 
Installing collected packages: numpy
ERROR: After October 2020 you may experience errors when installing or updating packages. This is because pip will change the way that it resolves dependency conflicts.

We recommend you use --use-feature=2020-resolver to test your packages with the new resolver before it becomes the default.

tensorflow 1.15.4 requires numpy<1.19.0,>=1.16.0, but you'll have numpy 1.19.4 which is incompatible.
Successfully installed numpy-1.19.4
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ pip uninstall numpy
Found existing installation: numpy 1.19.4
Uninstalling numpy-1.19.4:
  Would remove:
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/bin/f2py
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/bin/f2py3
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/bin/f2py3.6
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/numpy-1.19.4.dist-info/*
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/numpy.libs/libgfortran-2e0d59d6.so.5.0.0
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/numpy.libs/libopenblasp-r0-ae94cfde.3.9.dev.so
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/numpy.libs/libquadmath-2d0c479f.so.0.0.0
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/numpy.libs/libz-eb09ad1d.so.1.2.3
    /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/numpy/*
Proceed (y/n)? y
  Successfully uninstalled numpy-1.19.4
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

numpy version 1.16.0 ကို install လုပ်ခဲ့...  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ pip install numpy==1.16.0
Collecting numpy==1.16.0
  Downloading numpy-1.16.0-cp36-cp36m-manylinux1_x86_64.whl (17.3 MB)
     |████████████████████████████████| 17.3 MB 436 kB/s 
Installing collected packages: numpy
Successfully installed numpy-1.16.0
```

## Training

Sample data နဲ့ training ပြန်ကြိုးစားကြည့်ခဲ့...  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ python ./train-sample.py 2>&1 | tee train-sample.log
Using TensorFlow backend.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:74: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:517: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:4138: The name tf.random_uniform is deprecated. Please use tf.random.uniform instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:174: The name tf.get_default_session is deprecated. Please use tf.compat.v1.get_default_session instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:181: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:186: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2020-11-18 04:29:13.640095: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2893390000 Hz
2020-11-18 04:29:13.640582: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x563415d207a0 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-11-18 04:29:13.640621: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:190: The name tf.global_variables is deprecated. Please use tf.compat.v1.global_variables instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:199: The name tf.is_variable_initialized is deprecated. Please use tf.compat.v1.is_variable_initialized instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:206: The name tf.variables_initializer is deprecated. Please use tf.compat.v1.variables_initializer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:133: The name tf.placeholder_with_default is deprecated. Please use tf.compat.v1.placeholder_with_default instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3445: calling dropout (from tensorflow.python.ops.nn_ops) with keep_prob is deprecated and will be removed in a future version.
Instructions for updating:
Please use `rate` instead of `keep_prob`. Rate should be set to `rate = 1 - keep_prob`.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/optimizers.py:790: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3376: The name tf.log is deprecated. Please use tf.math.log instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/tensorflow_core/python/ops/nn_impl.py:183: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:986: The name tf.assign_add is deprecated. Please use tf.compat.v1.assign_add instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:973: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/callbacks.py:850: The name tf.summary.merge_all is deprecated. Please use tf.compat.v1.summary.merge_all instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/callbacks.py:853: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

Embedding matrix shape: (3052, 50)
Null word embeddings: 1
Train on 450 samples, validate on 49 samples
Epoch 1/200

 64/450 [===>..........................] - ETA: 18s - loss: 0.9940 - acc: 0.5000
192/450 [===========>..................] - ETA: 4s - loss: 0.9387 - acc: 0.5312 
320/450 [====================>.........] - ETA: 1s - loss: 0.9227 - acc: 0.5281
448/450 [============================>.] - ETA: 0s - loss: 0.9133 - acc: 0.5179
450/450 [==============================] - 4s 8ms/step - loss: 0.9141 - acc: 0.5178 - val_loss: 0.9484 - val_acc: 0.5510
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/callbacks.py:995: The name tf.Summary is deprecated. Please use tf.compat.v1.Summary instead.

Epoch 2/200

 64/450 [===>..........................] - ETA: 0s - loss: 0.7160 - acc: 0.5938
192/450 [===========>..................] - ETA: 0s - loss: 0.7640 - acc: 0.5677
320/450 [====================>.........] - ETA: 0s - loss: 0.7710 - acc: 0.5750
448/450 [============================>.] - ETA: 0s - loss: 0.7842 - acc: 0.5804
450/450 [==============================] - 0s 586us/step - loss: 0.7853 - acc: 0.5800 - val_loss: 0.8706 - val_acc: 0.5714
Epoch 3/200

 64/450 [===>..........................] - ETA: 0s - loss: 0.7885 - acc: 0.5156
192/450 [===========>..................] - ETA: 0s - loss: 0.8339 - acc: 0.5417
320/450 [====================>.........] - ETA: 0s - loss: 0.7933 - acc: 0.5625
448/450 [============================>.] - ETA: 0s - loss: 0.7864 - acc: 0.5603
450/450 [==============================] - 0s 570us/step - loss: 0.7888 - acc: 0.5600 - val_loss: 0.8246 - val_acc: 0.5510
Epoch 4/200

 64/450 [===>..........................] - ETA: 0s - loss: 0.8365 - acc: 0.5469
192/450 [===========>..................] - ETA: 0s - loss: 0.7679 - acc: 0.6146
320/450 [====================>.........] - ETA: 0s - loss: 0.7497 - acc: 0.6094
448/450 [============================>.] - ETA: 0s - loss: 0.7242 - acc: 0.6138
450/450 [==============================] - 0s 569us/step - loss: 0.7241 - acc: 0.6133 - val_loss: 0.7827 - val_acc: 0.5510
Epoch 5/200

 64/450 [===>..........................] - ETA: 0s - loss: 0.7119 - acc: 0.5781
192/450 [===========>..................] - ETA: 0s - loss: 0.7367 - acc: 0.5677
320/450 [====================>.........] - ETA: 0s - loss: 0.7592 - acc: 0.5500
448/450 [============================>.] - ETA: 0s - loss: 0.7510 - acc: 0.5536
450/450 [==============================] - 0s 578us/step - loss: 0.7506 - acc: 0.5533 - val_loss: 0.7586 - val_acc: 0.5714
Epoch 6/200

 64/450 [===>..........................] - ETA: 0s - loss: 0.6889 - acc: 0.5625
192/450 [===========>..................] - ETA: 0s - loss: 0.6550 - acc: 0.6198
320/450 [====================>.........] - ETA: 0s - loss: 0.6737 - acc: 0.5969
448/450 [============================>.] - ETA: 0s - loss: 0.6710 - acc: 0.6161
450/450 [==============================] - 0s 576us/step - loss: 0.6687 - acc: 0.6178 - val_loss: 0.8125 - val_acc: 0.5510
Epoch 7/200

 64/450 [===>..........................] - ETA: 0s - loss: 0.6886 - acc: 0.6250
192/450 [===========>..................] - ETA: 0s - loss: 0.6628 - acc: 0.6302
320/450 [====================>.........] - ETA: 0s - loss: 0.6807 - acc: 0.6094
448/450 [============================>.] - ETA: 0s - loss: 0.6894 - acc: 0.6094
450/450 [==============================] - 0s 575us/step - loss: 0.6905 - acc: 0.6089 - val_loss: 0.7689 - val_acc: 0.5714
Epoch 8/200

 64/450 [===>..........................] - ETA: 0s - loss: 0.6366 - acc: 0.5938
192/450 [===========>..................] - ETA: 0s - loss: 0.6362 - acc: 0.6406
320/450 [====================>.........] - ETA: 0s - loss: 0.6986 - acc: 0.6312
448/450 [============================>.] - ETA: 0s - loss: 0.6733 - acc: 0.6362
450/450 [==============================] - 0s 596us/step - loss: 0.6721 - acc: 0.6378 - val_loss: 0.8000 - val_acc: 0.5102
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

***Very fast!!!***  
Accuracy က သိပ်အကောင်းကြီး မဟုတ်ပေမဲ့ လက်ရှိဒေတာနဲ့ လက်ရှိ setting နဲ့ အချိန်တိုတိုအတွင်းမှာ similarity measure လုပ်နိုင်တာမို့ ရည်ရွယ်ထားတဲ့ paraphrase experiment အတွက် အဆင်ပြေနိုင်တယ် ... :)

## Testing

Testing ကိုလည်း သူ့မှာ ပါတဲ့ original script ဖြစ်တဲ့ test-sample.py နဲ့ စမ်းကြည့်ခဲ့တယ်။ Error အမျိုးမျိုးပေးတယ်။  
Finally, source code debug လုပ်တာရသွားတယ်။    
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ python test-sample.py 2>&1 | tee test-sample.log
Using TensorFlow backend.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:517: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:74: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:4138: The name tf.random_uniform is deprecated. Please use tf.random.uniform instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:133: The name tf.placeholder_with_default is deprecated. Please use tf.compat.v1.placeholder_with_default instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3445: calling dropout (from tensorflow.python.ops.nn_ops) with keep_prob is deprecated and will be removed in a future version.
Instructions for updating:
Please use `rate` instead of `keep_prob`. Rate should be set to `rate = 1 - keep_prob`.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:174: The name tf.get_default_session is deprecated. Please use tf.compat.v1.get_default_session instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:181: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:186: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2020-11-18 05:18:10.724034: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2893390000 Hz
2020-11-18 05:18:10.724585: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x5645cef8ead0 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-11-18 05:18:10.724645: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:190: The name tf.global_variables is deprecated. Please use tf.compat.v1.global_variables instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:199: The name tf.is_variable_initialized is deprecated. Please use tf.compat.v1.is_variable_initialized instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:206: The name tf.variables_initializer is deprecated. Please use tf.compat.v1.variables_initializer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/optimizers.py:790: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3376: The name tf.log is deprecated. Please use tf.math.log instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/tensorflow_core/python/ops/nn_impl.py:183: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:986: The name tf.assign_add is deprecated. Please use tf.compat.v1.assign_add instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:973: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.


2/2 [==============================] - 1s 348ms/step
[('What can make Physics easy to learn?', 'How can you make physics easy to learn?', 0.8667481), ('How many times a day do a clocks hands overlap?', 'What does it mean that every time I look at the clock the numbers are the same?', 0.8667481)]
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

ဒီ testing code မှာက similarity ကိုတိုင်းတာချင်တဲ့ စာကြောင်းတွေကို source code ထဲကနေ ပေးထားတယ်။ output မှာတော့ အထက်မှာ မြင်ရတဲ့အတိုင်း score တွေကို သေချာထုတ်ပေးလို့ အဆင်ပြေတယ်။  

## Testing with paraphrase data

မနေ့ကညကလား ပို့ထားတဲ့ manual ပြင်ဆင်နေတဲ့ paraphrase မဟုတ်တဲ့ စာကြောင်း တစ်သောင်းနဲ့ လက်ရှိ ရှိနေတဲ့ paraphrase စာကြောင်း ရှစ်သောင်းကျော်ကနေ တစ်သောင်းကို ဆွဲထုတ်ယူပြီး test experiment လုပ်ကြည့်မယ်။ အရင်ဆုံး အောက်ပါအတိုင်း ဒေတာတွေကို ပြင်ဆင်တယ်။  
data တွေကို လက်ရှိ ဖိုလ်ဒါအောက်ကို ကောပီကူးခဲ့...  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ cp /media/ye/project1/student/utycc-newR/seminar/6thSeminar/MyintMyintHtay/23Nov2020/forsec/paraphrase_sentence.final .

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ cp /media/ye/project1/student/utycc-newR/seminar/6thSeminar/MyintMyintHtay/16Dec2020/not-para-human.5k.txt .

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ wc paraphrase_sentence.final 
   84498  1166569 15423318 paraphrase_sentence.final   
```

ရှစ်သောင်း ကျော်ရှိပေမဲ့ test-experiment အတွက်က အဲဒီအထဲကနေ paraphrase မဟုတ်တဲ့ ဒေတာနဲ့လည်းမျှသွားအောင် လောလောဆယ် စာကြောင်းတစ်သောင်း ကိုပဲ ဆွဲထုတ်ယူခဲ့တယ်။  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head -n 10000 ./paraphrase_sentence.final > 10k.para
```

original paraphrase data 10k ရဲ့ format က အောက်ပါအတိုင်း  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head ./10k.para
အောင်မြင် အောင် ကြိုးစား ပါ အားပေး နေ ဆဲ	အောင်မြင် မှု တွေ ရ ပါ စေ အားပေး လျက်
မျှော် နေ တာ ကြာ ပြီ	မျှော်လင့် နေ တာ ကြာ ပြီ
ကျွန်တော် ကြားဖူး တာ က ထွန်းထွန်းပေါက်ပေါက်ဖြစ် ဖို့ မ လွယ် ဘူး တဲ့ ။	ကျွန်တော် ကြားဖူး တာ က အောင်မြင် ဖို့ မ လွယ် ဘူး တဲ့ ။
ကောင်း မြတ် တယ်	ကောင်း တယ်
ကူညီ ပေး ကြ ပါ ဦး	ကူညီ ကယ်တင် ပေး ကြ ပါ
စား ချင် စရာ ပဲ	စား ချင် စရာ ကြီး ပဲ နော်
နောင် ဘဝ အဆက်ဆက် ဒီလို အဖြစ်မျိုး နဲ့ ကင်းဝေး ပါ စေ	နောင် ဘဝ မှာ ဒီလို မ ဖြစ် ပါ စေ နဲ့
ငွေ မ ပြည့်စုံ တဲ့ အတွက် ကြောင့် ငါ နိုင်ငံ ခြား မ သွား တော့ ဘူး ။	ငွေ ပြည့်ပြည့်စုံစုံ မ ရှိ တဲ့ အတွက် ကြောင့် ငါ နိုင်ငံ ခြား မ သွား တော့ ဘူး ။
ဂုဏ်ယူ လျက် ပါ	ဂုဏ်ယူ လိုက် တာ
စား ချင် တယ် လေ	စား ချင် ပါ သည်
```

ထုံးစံအတိုင်း ဒေတာတွေကို training/validation မလုပ်ခင်မှာ သုံးမယ့်ပရိုဂရမ်၊ framework က သတ်မှတ်ထားတဲ့ format ဖြစ်အောင်ညှိပေးဖို့ လိုအပ်တယ်။ အရင်ဆုံး "sed command" ကို သုံးပြီးတော့ format ပြောင်းတယ်။  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ sed 's/\(.*\)/\1,1/;s/\t/,/' < ./10k.para > ./10k.para.format
```

paraphrase ဒေတာတွေအတွက် လိုချင်တဲ့ format တော့ ရသွားပြီ။ အောက်ပါအတိုင်း paraphrase ဖြစ်တဲ့ စာကြောင်းအတွဲတွေကိုတော့ နံပါတ် 1 ဆိုပြီး လေဘယ်တပ်ပါတယ်။  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head ./10k.para.format 
အောင်မြင် အောင် ကြိုးစား ပါ အားပေး နေ ဆဲ,အောင်မြင် မှု တွေ ရ ပါ စေ အားပေး လျက်,1
မျှော် နေ တာ ကြာ ပြီ,မျှော်လင့် နေ တာ ကြာ ပြီ,1
ကျွန်တော် ကြားဖူး တာ က ထွန်းထွန်းပေါက်ပေါက်ဖြစ် ဖို့ မ လွယ် ဘူး တဲ့ ။,ကျွန်တော် ကြားဖူး တာ က အောင်မြင် ဖို့ မ လွယ် ဘူး တဲ့ ။,1
ကောင်း မြတ် တယ်,ကောင်း တယ်,1
ကူညီ ပေး ကြ ပါ ဦး,ကူညီ ကယ်တင် ပေး ကြ ပါ,1
စား ချင် စရာ ပဲ,စား ချင် စရာ ကြီး ပဲ နော်,1
နောင် ဘဝ အဆက်ဆက် ဒီလို အဖြစ်မျိုး နဲ့ ကင်းဝေး ပါ စေ,နောင် ဘဝ မှာ ဒီလို မ ဖြစ် ပါ စေ နဲ့,1
ငွေ မ ပြည့်စုံ တဲ့ အတွက် ကြောင့် ငါ နိုင်ငံ ခြား မ သွား တော့ ဘူး ။,ငွေ ပြည့်ပြည့်စုံစုံ မ ရှိ တဲ့ အတွက် ကြောင့် ငါ နိုင်ငံ ခြား မ သွား တော့ ဘူး ။,1
ဂုဏ်ယူ လျက် ပါ,ဂုဏ်ယူ လိုက် တာ,1
စား ချင် တယ် လေ,စား ချင် ပါ သည်,1
```

non-paraphrase အတွက်လည်း \<sentence\>,\<sentence\>,0 ဆိုတဲ့ format ကိုပြင်ဆင်ရတယ်။ အောက်ပါအတိုင်း အဆင့်ဆင့်လုပ်သွားခဲ့တယ်...  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head not-para-human.5k.txt 
သူ ဟာ အားကစား အမျိုးမျိုး မှာ စိတ်ပါဝင်စား တယ် ဆို တာ ခင်ဗျား သိ သလား ။	သူ ဟာ အားကစား အမျိုးမျိုး မှာ ကျွမ်းကျင် တယ် ဆို တာ ခင်ဗျား သိ သလား ။	0
စံပယ် ဆို အရမ်း ကြိုက် တယ်	စံပယ် ပန်း နှင့် ထုတ် ထား ပါ တယ်	0
တရား ကို နတ် စောင့် ပါ တယ် မြန်မြန် လွတ် ပါစေ	တရားပွဲ ကို နတ် တွေ တရား လာ နာ ပါ တယ် မြန်မြန် လွတ်မြောက် ပါစေ	0
ဆရာတော် ကျန်းမာ ပါစေ ချမ်းသာ ပါစေ	ဆရာတော် ဘုရား လည်း ကျန်းမာ ရေး ကောင်း ပါ တယ်	0
ဆက် ပြီး ကြိုးစား ထား ကြ ဟေ့	ရှေ့ဆက် ပြီး ကြိုးစား သင်ယူ ပါ	0
မင်း အလို က ဘယ်တော့ ပြည့် မှာ လဲ ။	မင်း အလိုမကျ တာ က ဘာ ကြောင့် လဲ ။	0
ငါ့ ဘဝ က အတော် လေး ဆိုးရွား ပါ တယ် ။	ငါ့ ဘဝ က အဲ့လောက်တော့ မ ဆိုးဝါး ပါ ဘူး ။	0
ဒါ သူ ယူ ထား တဲ့ နောက်ဇနီး လေ ။	ဒါ သူ ယူ ထား တဲ့ နောက်မယား ရဲ့ သား လေ ။	0
ကောင်း သော နေ့လယ်ပိုင်း လေး ပါ နော်	ပျော် စရာ မွေးနေ့ ဖြစ် ပါစေ	0
တစ်သက် လုံး ရှောင်တိမ်း နေ လိုက် ပါ ကွာ နားအေး တယ် ။	တစ်သက် လုံး တိမ်းရှောင် နေ လိုက် ပါ ကွာ နားငြီး တယ် ။	0
```

ဆရာတို့ ပြင်ဆင်ထားတာက \<TAB\> ကီးခြားထားတာမို့...  
sed command ကို သုံပြီးတော့ \<TAB\> ကီးနေရာကို comma နဲ့ အစားထိုးခဲ့တယ်။   
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ sed 's/\t/,/g' < ./not-para-human.5k.txt > ./not-para-human.5k.txt.format
```

format ကို တချက် confirmation လုပ်ခဲ့...  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head ./not-para-human.5k.txt.format 
သူ ဟာ အားကစား အမျိုးမျိုး မှာ စိတ်ပါဝင်စား တယ် ဆို တာ ခင်ဗျား သိ သလား ။,သူ ဟာ အားကစား အမျိုးမျိုး မှာ ကျွမ်းကျင် တယ် ဆို တာ ခင်ဗျား သိ သလား ။,0
စံပယ် ဆို အရမ်း ကြိုက် တယ်,စံပယ် ပန်း နှင့် ထုတ် ထား ပါ တယ်,0
တရား ကို နတ် စောင့် ပါ တယ် မြန်မြန် လွတ် ပါစေ,တရားပွဲ ကို နတ် တွေ တရား လာ နာ ပါ တယ် မြန်မြန် လွတ်မြောက် ပါစေ,0
ဆရာတော် ကျန်းမာ ပါစေ ချမ်းသာ ပါစေ,ဆရာတော် ဘုရား လည်း ကျန်းမာ ရေး ကောင်း ပါ တယ်,0
ဆက် ပြီး ကြိုးစား ထား ကြ ဟေ့,ရှေ့ဆက် ပြီး ကြိုးစား သင်ယူ ပါ,0
မင်း အလို က ဘယ်တော့ ပြည့် မှာ လဲ ။,မင်း အလိုမကျ တာ က ဘာ ကြောင့် လဲ ။,0
ငါ့ ဘဝ က အတော် လေး ဆိုးရွား ပါ တယ် ။,ငါ့ ဘဝ က အဲ့လောက်တော့ မ ဆိုးဝါး ပါ ဘူး ။,0
ဒါ သူ ယူ ထား တဲ့ နောက်ဇနီး လေ ။,ဒါ သူ ယူ ထား တဲ့ နောက်မယား ရဲ့ သား လေ ။,0
ကောင်း သော နေ့လယ်ပိုင်း လေး ပါ နော်,ပျော် စရာ မွေးနေ့ ဖြစ် ပါစေ,0
တစ်သက် လုံး ရှောင်တိမ်း နေ လိုက် ပါ ကွာ နားအေး တယ် ။,တစ်သက် လုံး တိမ်းရှောင် နေ လိုက် ပါ ကွာ နားငြီး တယ် ။,0
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$
```

paraphrase data နဲ့ not paraphrase data နှစ်မျိုးကို ပေါင်းခဲ့တယ်။   
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ cat ./10k.para.format ./not-para-human.5k.txt.format > para-not-para
```

စာကြောင်းရေအရေအတွက်ကို စစ်ဆေးကြည့်ခဲ့...  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ wc ./para-not-para 
  20000  288758 3962466 ./para-not-para
```

shuffle လုပ်တယ်။ ဒီအဆင့်ဟာလည်း အရေးကြီးပါတယ်။ ခုနောက်ပိုင်း Neural Network framework တွေမှာတော့ epoch တစ်ခေါက် training လုပ်တိုင်းမှာ shuffle လုပ်ပေးတဲ့ facility တွေပါပေမဲ့ ကိုယ်တိုင်က အလေ့အကျင့်တစ်ခုအနေနဲ့ လုပ်သွားတာကကောင်းပါတယ်။ မဟုတ်ရင် training တွေလုပ်ပြီးမှ ဒေတာက shuffle မလုပ်ခဲ့လို့ model မှာ ဘက်လိုက်မှုရှိတာမျိုးကို ဂရုပြုမိရင် မော်ဒယ်ကို အစကနေ ပြန်ဆောက်ကြရတာမို့ပါ။    
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ shuf ./para-not-para > ./para-not-para.shuf
```

Format checking ကို အကြမ်းလုပ်ခဲ့။ It looks OK ...  
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head ./para-not-para.shuf 
ပိန် လိုက် တာ ပိန်ကပ် နေ တာ ပဲ ။,ပိန်း လိုက် တာ ကွာ ။,0
ဘယ်လို နည်း နဲ့ မှ ကြည်ညို လို့ မ ရ တော့ ဘူး,ကြည်ညို စရာ မ ကောင်း ဘူး,1
ဒီထက်မက အောင်မြင် နိုင် ပါ စေ,ဒီထက်မက အောင်မြင် မှု များ ရ နိုင် ပါ စေ နော်,1
မြေ တွေ ကို ဆွ ပြီး ပေါင်းထိုး လိုက် ပါ ။,မြေ တွေ ကို ထိုး ပြီး ပေါင်းထိုး လိုက် ပါ ။,1
ပျော်လွန်း လို့ မျက်ရည် တောင် ဝိုင်း တယ်,သမ်း လိုက် တာ မျက်ရည် တောင် ဝိုင်း တယ်,0
မောင် အဲလောက် အထိ စိမ်း ရက် တယ် နော် ။,မောင် အဲလောက် အထိ စိမ်းကား ရက် တယ် နော် ။,1
ရေလုံ တဲ့ ကုတ် အင်္ကျီ ပြ ပေး မလား ။,ကုတ် အင်္ကျီ ရေလုံ တာ ဝတ် သွား ပါ ။,0
သူမ မင်း ကို မ သိ ခဲ့ ပါ ဘူး ။,သူမ မင်း ကို သိ တယ် ။,0
ဒီထက် လှူ နိုင် ကြ ပါ စေ,ဒီထက် ပို ပြီး လှူနိုင်တန်းနိုင် ပါ စေ,1
မကျက်တကျက် လား ၊ အတော်အသင့် အကျက် လား ၊ ကျက်ကျက် ကြီး လား ။,မကျက်တကျက် တွေ အတော်အသင့် ကျက် တွေ မ စား ပါ နဲ့ ။,0
```

## prepare line number

အခုသုံးကြည့်ဖို့အတွက် ပြင်ဆင်နေတဲ့ LSTM Siamese program ရဲ့ data format မှာက ရှေ့ဆုံးမှာ လိုင်းနံပါတ်ဖြည့်ထားပါတယ်။ အဲဒီအတွက် အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ seq 0 20000 > ./line-no
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head line-no
0
1
2
3
4
5
6
7
8
9
```
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ tail line-no
19991
19992
19993
19994
19995
19996
19997
19998
19999
20000
```

စောစောက ပြင်ဆင်ခဲ့တဲ့ shuffle လုပ်ထားပြီးသား paraphrase+non-paraphrase ဒေတာတွေရဲ့ ဖိုင်နဲ့ လိုင်းနံပါတ်-ဖိုင် ကို ကော်မာနဲ့ခြားပြီး တွဲပေးခဲ့တယ်။   
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ paste line-no ./para-not-para.shuf -d"," > ./line-no.para-no-para.shuf
```

တွဲပြီး သိမ်းထားတဲ့ဖိုင်အသစ် line-no.para-no-para.shuf ရဲ့ ထိပ်ဆုံး ၁၀ကြောင်းကို head command နဲ့စကရင်မှာ ရိုက်ထုတ်ကြည့်ခဲ့...   
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head ./line-no.para-no-para.shuf 
0,ပိန် လိုက် တာ ပိန်ကပ် နေ တာ ပဲ ။,ပိန်း လိုက် တာ ကွာ ။,0
1,ဘယ်လို နည်း နဲ့ မှ ကြည်ညို လို့ မ ရ တော့ ဘူး,ကြည်ညို စရာ မ ကောင်း ဘူး,1
2,ဒီထက်မက အောင်မြင် နိုင် ပါ စေ,ဒီထက်မက အောင်မြင် မှု များ ရ နိုင် ပါ စေ နော်,1
3,မြေ တွေ ကို ဆွ ပြီး ပေါင်းထိုး လိုက် ပါ ။,မြေ တွေ ကို ထိုး ပြီး ပေါင်းထိုး လိုက် ပါ ။,1
4,ပျော်လွန်း လို့ မျက်ရည် တောင် ဝိုင်း တယ်,သမ်း လိုက် တာ မျက်ရည် တောင် ဝိုင်း တယ်,0
5,မောင် အဲလောက် အထိ စိမ်း ရက် တယ် နော် ။,မောင် အဲလောက် အထိ စိမ်းကား ရက် တယ် နော် ။,1
6,ရေလုံ တဲ့ ကုတ် အင်္ကျီ ပြ ပေး မလား ။,ကုတ် အင်္ကျီ ရေလုံ တာ ဝတ် သွား ပါ ။,0
7,သူမ မင်း ကို မ သိ ခဲ့ ပါ ဘူး ။,သူမ မင်း ကို သိ တယ် ။,0
8,ဒီထက် လှူ နိုင် ကြ ပါ စေ,ဒီထက် ပို ပြီး လှူနိုင်တန်းနိုင် ပါ စေ,1
9,မကျက်တကျက် လား ၊ အတော်အသင့် အကျက် လား ၊ ကျက်ကျက် ကြီး လား ။,မကျက်တကျက် တွေ အတော်အသင့် ကျက် တွေ မ စား ပါ နဲ့ ။,0
```

## Adding column header

CSV ဖိုင်တွေရဲ့ ထုံးစံအတိုင်း ဖိုင်ရဲ့ထိပ်ဆုံးအကြောင်းက column header တပ်ပေးရအောင်။ ဆရာက sample data ရဲ့column header ကိုပဲယူလိုက်ပါတယ်။ နာမည်က သိပ်ပြဿနာမရှိလို့ နောက်ပြီး Python code အထဲက field-name ဖတ်ထားတဲ့ စာကြောင်းတွေကိုလည်း ဝင်မပြင်ချင်လို့ ...   
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ (echo ",sentences1,sentences2,is_similar" && cat ./line-no.para-no-para.shuf) > line-no.para-no-para.shuf.final
```

တကယ်က အခုမှသာ မော်ဒယ်ဆောက်ဖို့အတွက် လိုအပ်တဲ့ format ကို ပြင်ဆင်တာပြီးစီးသွားတာပါ။   
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head ./line-no.para-no-para.shuf.final 
,sentences1,sentences2,is_similar
0,ပိန် လိုက် တာ ပိန်ကပ် နေ တာ ပဲ ။,ပိန်း လိုက် တာ ကွာ ။,0
1,ဘယ်လို နည်း နဲ့ မှ ကြည်ညို လို့ မ ရ တော့ ဘူး,ကြည်ညို စရာ မ ကောင်း ဘူး,1
2,ဒီထက်မက အောင်မြင် နိုင် ပါ စေ,ဒီထက်မက အောင်မြင် မှု များ ရ နိုင် ပါ စေ နော်,1
3,မြေ တွေ ကို ဆွ ပြီး ပေါင်းထိုး လိုက် ပါ ။,မြေ တွေ ကို ထိုး ပြီး ပေါင်းထိုး လိုက် ပါ ။,1
4,ပျော်လွန်း လို့ မျက်ရည် တောင် ဝိုင်း တယ်,သမ်း လိုက် တာ မျက်ရည် တောင် ဝိုင်း တယ်,0
5,မောင် အဲလောက် အထိ စိမ်း ရက် တယ် နော် ။,မောင် အဲလောက် အထိ စိမ်းကား ရက် တယ် နော် ။,1
6,ရေလုံ တဲ့ ကုတ် အင်္ကျီ ပြ ပေး မလား ။,ကုတ် အင်္ကျီ ရေလုံ တာ ဝတ် သွား ပါ ။,0
7,သူမ မင်း ကို မ သိ ခဲ့ ပါ ဘူး ။,သူမ မင်း ကို သိ တယ် ။,0
8,ဒီထက် လှူ နိုင် ကြ ပါ စေ,ဒီထက် ပို ပြီး လှူနိုင်တန်းနိုင် ပါ စေ,1
```

## Copy and Editing the Python Script

git clone လုပ်ခဲ့တုန်းက ပါလာတဲ့ train-sample.py ကို train-para1.py အဖြစ်ကော်ပီကူးခဲ့တယ်...   
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ cp train-sample.py train-para1.py
```

gedit နဲ့ ဖွင့်ပြီးတော့...  

```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ gedit train-para1.py
```

အောက်ပါလိုင်းတွေကို update လုပ်ခဲ့ ...  
ကိုယ့်ဒေတာရှိတဲ့ path နဲ့ အစားထိုးသွားပါ။   
```python
#df = pd.read_csv('sample_data.csv')
df = pd.read_csv('./para-tst-1/original/line-no.para-no-para.shuf.final.csv')
```

## Backup checkpoints folder

checkpoints/ ဆိုတဲ့ ဖိုလ်ဒါအောက်မှာ configuration setting မှာ သတ်မှတ်ထားတဲ့အတိုင်း best model ကိုသိမ်းပေးတာဘာညာ လုပ်ပေးသွားလိမ့်မယ်။ တစ်ခုရှိတာက training မလုပ်ခင်မှာ ရှေ့မှာ ဆောက်ခဲ့တဲ့ မော်ဒယ်တွေဘာတွေကို backup လုပ်တဲ့ အလေ့အကျင့်လုပ်ပါ။   
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ mv checkpoints/ checkpoints.bak
```

မော်ဒယ်မဆောက်ခင်မှာ Confirmation တစ်ခု လုပ်ရလိမ့်မယ်...  
training မလုပ်ခင်မှာ တကယ်လို့ ကိုယ်က (Ctrl+Shift+t နဲ့ပဲဖြစ်ဖြစ်) terminal အသစ်ဖွင့်သုံးထားတာဆိုရင်တော့ conda command သုံးပြီး   
LSTM Siamese Network experiment လုပ်ဖို့အတွက် ပြင်ဆင်ထားခဲ့တဲ့ Python environment အောက်ကို ပြန်ဝင်ရပါလိမ့်မယ်။   
```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ conda activate tensor1.15.4_keras2.2.4
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ 
```

## Training-1

ငါတို့ပြင်ဆင်ခဲ့ကြတဲ့ ဗမာစာ paraphrase ဒေတာကိုသုံးပြီး CPU Notebook ပေါ်မှာပဲ မောဒယ်စမ်းဆောက်ကြည့်ရအောင်....   
WARNING တွေက ခဏမေ့ထားပါ အိုကေပါတယ်။   
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ time python ./train-para1.py 2>&1 | tee ./para-tst-1/original/train-after-last-err-line-removed.log
Using TensorFlow backend.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:74: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:517: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:4138: The name tf.random_uniform is deprecated. Please use tf.random.uniform instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:174: The name tf.get_default_session is deprecated. Please use tf.compat.v1.get_default_session instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:181: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:186: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2020-12-16 06:30:35.983257: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2893330000 Hz
2020-12-16 06:30:35.983763: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55b02d6ca450 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-12-16 06:30:35.983809: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:190: The name tf.global_variables is deprecated. Please use tf.compat.v1.global_variables instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:199: The name tf.is_variable_initialized is deprecated. Please use tf.compat.v1.is_variable_initialized instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:206: The name tf.variables_initializer is deprecated. Please use tf.compat.v1.variables_initializer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:133: The name tf.placeholder_with_default is deprecated. Please use tf.compat.v1.placeholder_with_default instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3445: calling dropout (from tensorflow.python.ops.nn_ops) with keep_prob is deprecated and will be removed in a future version.
Instructions for updating:
Please use `rate` instead of `keep_prob`. Rate should be set to `rate = 1 - keep_prob`.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/optimizers.py:790: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3376: The name tf.log is deprecated. Please use tf.math.log instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/tensorflow_core/python/ops/nn_impl.py:183: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:986: The name tf.assign_add is deprecated. Please use tf.compat.v1.assign_add instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:973: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/callbacks.py:850: The name tf.summary.merge_all is deprecated. Please use tf.compat.v1.summary.merge_all instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/callbacks.py:853: The name tf.summary.FileWriter is deprecated. Please use tf.compat.v1.summary.FileWriter instead.

Embedding matrix shape: (11934, 50)
Null word embeddings: 1
Train on 18000 samples, validate on 2000 samples
Epoch 1/200

   64/18000 [..............................] - ETA: 13:25 - loss: 0.8098 - acc: 0.6094
  192/18000 [..............................] - ETA: 4:34 - loss: 0.8041 - acc: 0.6094 
  320/18000 [..............................] - ETA: 2:47 - loss: 0.7109 - acc: 0.6531
  448/18000 [..............................] - ETA: 2:01 - loss: 0.6950 - acc: 0.6562
  576/18000 [..............................] - ETA: 1:35 - loss: 0.6676 - acc: 0.6753
  704/18000 [>.............................] - ETA: 1:19 - loss: 0.6700 - acc: 0.6832
  832/18000 [>.............................] - ETA: 1:08 - loss: 0.6690 - acc: 0.6827
  960/18000 [>.............................] - ETA: 59s - loss: 0.6536 - acc: 0.6927 
 1088/18000 [>.............................] - ETA: 53s - loss: 0.6574 - acc: 0.6930
 1216/18000 [=>............................] - ETA: 48s - loss: 0.6485 - acc: 0.6982
 1344/18000 [=>............................] - ETA: 44s - loss: 0.6391 - acc: 0.7024
 1472/18000 [=>............................] - ETA: 40s - loss: 0.6306 - acc: 0.7065
 1600/18000 [=>............................] - ETA: 37s - loss: 0.6162 - acc: 0.7131
 1728/18000 [=>............................] - ETA: 35s - loss: 0.6086 - acc: 0.7164
 1856/18000 [==>...........................] - ETA: 33s - loss: 0.6015 - acc: 0.7204
 1984/18000 [==>...........................] - ETA: 31s - loss: 0.5910 - acc: 0.7263
 2112/18000 [==>...........................] - ETA: 29s - loss: 0.5806 - acc: 0.7315
 2240/18000 [==>...........................] - ETA: 28s - loss: 0.5746 - acc: 0.7339
 2368/18000 [==>...........................] - ETA: 26s - loss: 0.5674 - acc: 0.7365
 2496/18000 [===>..........................] - ETA: 25s - loss: 0.5574 - acc: 0.7420
 2624/18000 [===>..........................] - ETA: 24s - loss: 0.5523 - acc: 0.7435
 2752/18000 [===>..........................] - ETA: 23s - loss: 0.5490 - acc: 0.7453
 2880/18000 [===>..........................] - ETA: 22s - loss: 0.5439 - acc: 0.7483
 3008/18000 [====>.........................] - ETA: 21s - loss: 0.5359 - acc: 0.7523
 3136/18000 [====>.........................] - ETA: 21s - loss: 0.5295 - acc: 0.7557
 3264/18000 [====>.........................] - ETA: 20s - loss: 0.5255 - acc: 0.7577
 3392/18000 [====>.........................] - ETA: 19s - loss: 0.5264 - acc: 0.7577
 3520/18000 [====>.........................] - ETA: 19s - loss: 0.5234 - acc: 0.7588
 3648/18000 [=====>........................] - ETA: 18s - loss: 0.5205 - acc: 0.7612
 3776/18000 [=====>........................] - ETA: 17s - loss: 0.5149 - acc: 0.7640
 3904/18000 [=====>........................] - ETA: 17s - loss: 0.5103 - acc: 0.7661
 4032/18000 [=====>........................] - ETA: 16s - loss: 0.5068 - acc: 0.7674
 4160/18000 [=====>........................] - ETA: 16s - loss: 0.5053 - acc: 0.7671
 4288/18000 [======>.......................] - ETA: 16s - loss: 0.5003 - acc: 0.7703
 4416/18000 [======>.......................] - ETA: 15s - loss: 0.4986 - acc: 0.7717
 4544/18000 [======>.......................] - ETA: 15s - loss: 0.4941 - acc: 0.7742
 4672/18000 [======>.......................] - ETA: 14s - loss: 0.4931 - acc: 0.7748
 4800/18000 [=======>......................] - ETA: 14s - loss: 0.4901 - acc: 0.7758
 4928/18000 [=======>......................] - ETA: 14s - loss: 0.4894 - acc: 0.7764
 5056/18000 [=======>......................] - ETA: 13s - loss: 0.4853 - acc: 0.7785
 5184/18000 [=======>......................] - ETA: 13s - loss: 0.4821 - acc: 0.7805
 5312/18000 [=======>......................] - ETA: 13s - loss: 0.4796 - acc: 0.7816
 5440/18000 [========>.....................] - ETA: 12s - loss: 0.4785 - acc: 0.7825
 5568/18000 [========>.....................] - ETA: 12s - loss: 0.4755 - acc: 0.7845
 5696/18000 [========>.....................] - ETA: 12s - loss: 0.4740 - acc: 0.7848
 5824/18000 [========>.....................] - ETA: 12s - loss: 0.4716 - acc: 0.7852
 5952/18000 [========>.....................] - ETA: 11s - loss: 0.4672 - acc: 0.7873
 6080/18000 [=========>....................] - ETA: 11s - loss: 0.4638 - acc: 0.7890
 6208/18000 [=========>....................] - ETA: 11s - loss: 0.4616 - acc: 0.7901
 6336/18000 [=========>....................] - ETA: 11s - loss: 0.4601 - acc: 0.7912
 6464/18000 [=========>....................] - ETA: 10s - loss: 0.4555 - acc: 0.7929
 6592/18000 [=========>....................] - ETA: 10s - loss: 0.4566 - acc: 0.7929
 6720/18000 [==========>...................] - ETA: 10s - loss: 0.4551 - acc: 0.7930
 6848/18000 [==========>...................] - ETA: 10s - loss: 0.4528 - acc: 0.7941
 6976/18000 [==========>...................] - ETA: 9s - loss: 0.4503 - acc: 0.7952 
 7104/18000 [==========>...................] - ETA: 9s - loss: 0.4486 - acc: 0.7960
 7232/18000 [===========>..................] - ETA: 9s - loss: 0.4465 - acc: 0.7972
 7360/18000 [===========>..................] - ETA: 9s - loss: 0.4454 - acc: 0.7976
 7488/18000 [===========>..................] - ETA: 9s - loss: 0.4441 - acc: 0.7974
 7616/18000 [===========>..................] - ETA: 9s - loss: 0.4437 - acc: 0.7979
 7744/18000 [===========>..................] - ETA: 8s - loss: 0.4429 - acc: 0.7986
 7872/18000 [============>.................] - ETA: 8s - loss: 0.4418 - acc: 0.7994
 8000/18000 [============>.................] - ETA: 8s - loss: 0.4411 - acc: 0.7997
 8128/18000 [============>.................] - ETA: 8s - loss: 0.4391 - acc: 0.8009
 8256/18000 [============>.................] - ETA: 8s - loss: 0.4378 - acc: 0.8012
 8384/18000 [============>.................] - ETA: 8s - loss: 0.4350 - acc: 0.8025
 8512/18000 [=============>................] - ETA: 7s - loss: 0.4335 - acc: 0.8030
 8640/18000 [=============>................] - ETA: 7s - loss: 0.4320 - acc: 0.8038
 8768/18000 [=============>................] - ETA: 7s - loss: 0.4304 - acc: 0.8044
 8896/18000 [=============>................] - ETA: 7s - loss: 0.4293 - acc: 0.8050
 9024/18000 [==============>...............] - ETA: 7s - loss: 0.4277 - acc: 0.8056
 9152/18000 [==============>...............] - ETA: 7s - loss: 0.4273 - acc: 0.8061
 9280/18000 [==============>...............] - ETA: 7s - loss: 0.4252 - acc: 0.8071
 9408/18000 [==============>...............] - ETA: 6s - loss: 0.4232 - acc: 0.8085
 9536/18000 [==============>...............] - ETA: 6s - loss: 0.4227 - acc: 0.8086
 9664/18000 [===============>..............] - ETA: 6s - loss: 0.4216 - acc: 0.8089
 9792/18000 [===============>..............] - ETA: 6s - loss: 0.4229 - acc: 0.8085
 9920/18000 [===============>..............] - ETA: 6s - loss: 0.4221 - acc: 0.8088
10048/18000 [===============>..............] - ETA: 6s - loss: 0.4214 - acc: 0.8091
10176/18000 [===============>..............] - ETA: 6s - loss: 0.4198 - acc: 0.8097
10304/18000 [================>.............] - ETA: 5s - loss: 0.4177 - acc: 0.8110
10432/18000 [================>.............] - ETA: 5s - loss: 0.4172 - acc: 0.8112
10560/18000 [================>.............] - ETA: 5s - loss: 0.4156 - acc: 0.8121
10688/18000 [================>.............] - ETA: 5s - loss: 0.4141 - acc: 0.8128
10816/18000 [=================>............] - ETA: 5s - loss: 0.4136 - acc: 0.8131
10944/18000 [=================>............] - ETA: 5s - loss: 0.4111 - acc: 0.8146
11072/18000 [=================>............] - ETA: 5s - loss: 0.4095 - acc: 0.8155
11136/18000 [=================>............] - ETA: 5s - loss: 0.4084 - acc: 0.8159
11264/18000 [=================>............] - ETA: 5s - loss: 0.4093 - acc: 0.8155
11392/18000 [=================>............] - ETA: 4s - loss: 0.4080 - acc: 0.8161
11520/18000 [==================>...........] - ETA: 4s - loss: 0.4073 - acc: 0.8166
11648/18000 [==================>...........] - ETA: 4s - loss: 0.4057 - acc: 0.8174
11776/18000 [==================>...........] - ETA: 4s - loss: 0.4049 - acc: 0.8177
11904/18000 [==================>...........] - ETA: 4s - loss: 0.4041 - acc: 0.8181
12032/18000 [===================>..........] - ETA: 4s - loss: 0.4036 - acc: 0.8187
12160/18000 [===================>..........] - ETA: 4s - loss: 0.4027 - acc: 0.8192
12288/18000 [===================>..........] - ETA: 4s - loss: 0.4016 - acc: 0.8197
12416/18000 [===================>..........] - ETA: 4s - loss: 0.4012 - acc: 0.8203
12544/18000 [===================>..........] - ETA: 3s - loss: 0.3997 - acc: 0.8209
12672/18000 [====================>.........] - ETA: 3s - loss: 0.3985 - acc: 0.8217
12800/18000 [====================>.........] - ETA: 3s - loss: 0.3973 - acc: 0.8223
12928/18000 [====================>.........] - ETA: 3s - loss: 0.3966 - acc: 0.8226
13056/18000 [====================>.........] - ETA: 3s - loss: 0.3957 - acc: 0.8231
13184/18000 [====================>.........] - ETA: 3s - loss: 0.3948 - acc: 0.8237
13312/18000 [=====================>........] - ETA: 3s - loss: 0.3935 - acc: 0.8245
13440/18000 [=====================>........] - ETA: 3s - loss: 0.3931 - acc: 0.8249
13568/18000 [=====================>........] - ETA: 3s - loss: 0.3918 - acc: 0.8258
13696/18000 [=====================>........] - ETA: 3s - loss: 0.3920 - acc: 0.8256
13824/18000 [======================>.......] - ETA: 2s - loss: 0.3906 - acc: 0.8261
13952/18000 [======================>.......] - ETA: 2s - loss: 0.3902 - acc: 0.8263
14080/18000 [======================>.......] - ETA: 2s - loss: 0.3892 - acc: 0.8267
14208/18000 [======================>.......] - ETA: 2s - loss: 0.3888 - acc: 0.8271
14336/18000 [======================>.......] - ETA: 2s - loss: 0.3882 - acc: 0.8276
14464/18000 [=======================>......] - ETA: 2s - loss: 0.3878 - acc: 0.8278
14592/18000 [=======================>......] - ETA: 2s - loss: 0.3869 - acc: 0.8281
14720/18000 [=======================>......] - ETA: 2s - loss: 0.3868 - acc: 0.8281
14848/18000 [=======================>......] - ETA: 2s - loss: 0.3864 - acc: 0.8285
14976/18000 [=======================>......] - ETA: 2s - loss: 0.3859 - acc: 0.8289
15104/18000 [========================>.....] - ETA: 1s - loss: 0.3851 - acc: 0.8293
15232/18000 [========================>.....] - ETA: 1s - loss: 0.3854 - acc: 0.8292
15360/18000 [========================>.....] - ETA: 1s - loss: 0.3847 - acc: 0.8298
15488/18000 [========================>.....] - ETA: 1s - loss: 0.3847 - acc: 0.8297
15616/18000 [=========================>....] - ETA: 1s - loss: 0.3849 - acc: 0.8296
15744/18000 [=========================>....] - ETA: 1s - loss: 0.3841 - acc: 0.8300
15872/18000 [=========================>....] - ETA: 1s - loss: 0.3841 - acc: 0.8301
16000/18000 [=========================>....] - ETA: 1s - loss: 0.3841 - acc: 0.8301
16128/18000 [=========================>....] - ETA: 1s - loss: 0.3831 - acc: 0.8308
16256/18000 [==========================>...] - ETA: 1s - loss: 0.3825 - acc: 0.8311
16384/18000 [==========================>...] - ETA: 1s - loss: 0.3817 - acc: 0.8315
16512/18000 [==========================>...] - ETA: 0s - loss: 0.3810 - acc: 0.8318
16640/18000 [==========================>...] - ETA: 0s - loss: 0.3816 - acc: 0.8314
16768/18000 [==========================>...] - ETA: 0s - loss: 0.3806 - acc: 0.8316
16896/18000 [===========================>..] - ETA: 0s - loss: 0.3799 - acc: 0.8321
17024/18000 [===========================>..] - ETA: 0s - loss: 0.3794 - acc: 0.8324
17152/18000 [===========================>..] - ETA: 0s - loss: 0.3795 - acc: 0.8322
17280/18000 [===========================>..] - ETA: 0s - loss: 0.3789 - acc: 0.8325
17408/18000 [============================>.] - ETA: 0s - loss: 0.3777 - acc: 0.8332
17536/18000 [============================>.] - ETA: 0s - loss: 0.3769 - acc: 0.8334
17664/18000 [============================>.] - ETA: 0s - loss: 0.3767 - acc: 0.8333
17792/18000 [============================>.] - ETA: 0s - loss: 0.3763 - acc: 0.8334
17920/18000 [============================>.] - ETA: 0s - loss: 0.3761 - acc: 0.8331
18000/18000 [==============================] - 13s 696us/step - loss: 0.3757 - acc: 0.8331 - val_loss: 0.4154 - val_acc: 0.7970
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/callbacks.py:995: The name tf.Summary is deprecated. Please use tf.compat.v1.Summary instead.

Epoch 2/200

   64/18000 [..............................] - ETA: 8s - loss: 0.3054 - acc: 0.8438
  192/18000 [..............................] - ETA: 9s - loss: 0.2740 - acc: 0.8698
  320/18000 [..............................] - ETA: 8s - loss: 0.3138 - acc: 0.8625
  448/18000 [..............................] - ETA: 8s - loss: 0.3035 - acc: 0.8750
  576/18000 [..............................] - ETA: 8s - loss: 0.2974 - acc: 0.8715
  704/18000 [>.............................] - ETA: 8s - loss: 0.3112 - acc: 0.8665
  832/18000 [>.............................] - ETA: 8s - loss: 0.2974 - acc: 0.8762
  960/18000 [>.............................] - ETA: 8s - loss: 0.2998 - acc: 0.8729
 1088/18000 [>.............................] - ETA: 8s - loss: 0.3014 - acc: 0.8722
 1216/18000 [=>............................] - ETA: 8s - loss: 0.3015 - acc: 0.8734
 1344/18000 [=>............................] - ETA: 8s - loss: 0.2910 - acc: 0.8787
 1472/18000 [=>............................] - ETA: 8s - loss: 0.2949 - acc: 0.8764
 1600/18000 [=>............................] - ETA: 8s - loss: 0.2966 - acc: 0.8750
 1728/18000 [=>............................] - ETA: 8s - loss: 0.2989 - acc: 0.8733
 1856/18000 [==>...........................] - ETA: 8s - loss: 0.3016 - acc: 0.8728
 1984/18000 [==>...........................] - ETA: 7s - loss: 0.3036 - acc: 0.8710
 2112/18000 [==>...........................] - ETA: 7s - loss: 0.3031 - acc: 0.8731
 2240/18000 [==>...........................] - ETA: 7s - loss: 0.3021 - acc: 0.8754
 2368/18000 [==>...........................] - ETA: 7s - loss: 0.3011 - acc: 0.8771
 2496/18000 [===>..........................] - ETA: 7s - loss: 0.2984 - acc: 0.8782
 2624/18000 [===>..........................] - ETA: 7s - loss: 0.2991 - acc: 0.8769
 2752/18000 [===>..........................] - ETA: 7s - loss: 0.2978 - acc: 0.8775
 2880/18000 [===>..........................] - ETA: 7s - loss: 0.2981 - acc: 0.8778
 3008/18000 [====>.........................] - ETA: 7s - loss: 0.2972 - acc: 0.8780
 3136/18000 [====>.........................] - ETA: 7s - loss: 0.2989 - acc: 0.8776
 3264/18000 [====>.........................] - ETA: 7s - loss: 0.3037 - acc: 0.8750
 3392/18000 [====>.........................] - ETA: 7s - loss: 0.3039 - acc: 0.8750
 3520/18000 [====>.........................] - ETA: 7s - loss: 0.3021 - acc: 0.8744
 3584/18000 [====>.........................] - ETA: 7s - loss: 0.3034 - acc: 0.8733
 3648/18000 [=====>........................] - ETA: 7s - loss: 0.3038 - acc: 0.8736
 3712/18000 [=====>........................] - ETA: 7s - loss: 0.3034 - acc: 0.8731
 3776/18000 [=====>........................] - ETA: 7s - loss: 0.3044 - acc: 0.8724
 3840/18000 [=====>........................] - ETA: 7s - loss: 0.3024 - acc: 0.8734
 3904/18000 [=====>........................] - ETA: 8s - loss: 0.3016 - acc: 0.8740
 3968/18000 [=====>........................] - ETA: 8s - loss: 0.3031 - acc: 0.8730
 4032/18000 [=====>........................] - ETA: 8s - loss: 0.3037 - acc: 0.8730
 4160/18000 [=====>........................] - ETA: 8s - loss: 0.3033 - acc: 0.8726
 4288/18000 [======>.......................] - ETA: 8s - loss: 0.3051 - acc: 0.8713
 4416/18000 [======>.......................] - ETA: 7s - loss: 0.3039 - acc: 0.8714
 4544/18000 [======>.......................] - ETA: 7s - loss: 0.3059 - acc: 0.8715
 4672/18000 [======>.......................] - ETA: 7s - loss: 0.3039 - acc: 0.8726
 4800/18000 [=======>......................] - ETA: 7s - loss: 0.3038 - acc: 0.8725
 4928/18000 [=======>......................] - ETA: 7s - loss: 0.3045 - acc: 0.8711
 5056/18000 [=======>......................] - ETA: 7s - loss: 0.3062 - acc: 0.8703
 5184/18000 [=======>......................] - ETA: 7s - loss: 0.3064 - acc: 0.8706
 5312/18000 [=======>......................] - ETA: 7s - loss: 0.3049 - acc: 0.8720
 5440/18000 [========>.....................] - ETA: 7s - loss: 0.3031 - acc: 0.8730
 5568/18000 [========>.....................] - ETA: 7s - loss: 0.3034 - acc: 0.8727
 5696/18000 [========>.....................] - ETA: 7s - loss: 0.3043 - acc: 0.8718
 5824/18000 [========>.....................] - ETA: 6s - loss: 0.3045 - acc: 0.8716
 5952/18000 [========>.....................] - ETA: 6s - loss: 0.3033 - acc: 0.8720
 6080/18000 [=========>....................] - ETA: 6s - loss: 0.3022 - acc: 0.8727
 6208/18000 [=========>....................] - ETA: 6s - loss: 0.3001 - acc: 0.8737
 6336/18000 [=========>....................] - ETA: 6s - loss: 0.3002 - acc: 0.8729
 6464/18000 [=========>....................] - ETA: 6s - loss: 0.3024 - acc: 0.8721
 6592/18000 [=========>....................] - ETA: 6s - loss: 0.3024 - acc: 0.8717
 6720/18000 [==========>...................] - ETA: 6s - loss: 0.3017 - acc: 0.8717
 6848/18000 [==========>...................] - ETA: 6s - loss: 0.3019 - acc: 0.8718
 6976/18000 [==========>...................] - ETA: 6s - loss: 0.3007 - acc: 0.8727
 7104/18000 [==========>...................] - ETA: 6s - loss: 0.3008 - acc: 0.8723
 7232/18000 [===========>..................] - ETA: 5s - loss: 0.3002 - acc: 0.8729
 7360/18000 [===========>..................] - ETA: 5s - loss: 0.2988 - acc: 0.8740
 7488/18000 [===========>..................] - ETA: 5s - loss: 0.2984 - acc: 0.8739
 7616/18000 [===========>..................] - ETA: 5s - loss: 0.2974 - acc: 0.8746
 7744/18000 [===========>..................] - ETA: 5s - loss: 0.2978 - acc: 0.8741
 7872/18000 [============>.................] - ETA: 5s - loss: 0.2978 - acc: 0.8737
 8000/18000 [============>.................] - ETA: 5s - loss: 0.2988 - acc: 0.8735
 8128/18000 [============>.................] - ETA: 5s - loss: 0.2989 - acc: 0.8735
 8256/18000 [============>.................] - ETA: 5s - loss: 0.2996 - acc: 0.8728
 8384/18000 [============>.................] - ETA: 5s - loss: 0.3004 - acc: 0.8726
 8512/18000 [=============>................] - ETA: 5s - loss: 0.2994 - acc: 0.8730
 8640/18000 [=============>................] - ETA: 5s - loss: 0.3007 - acc: 0.8719
 8768/18000 [=============>................] - ETA: 5s - loss: 0.3005 - acc: 0.8714
 8896/18000 [=============>................] - ETA: 4s - loss: 0.3019 - acc: 0.8713
 9024/18000 [==============>...............] - ETA: 4s - loss: 0.3021 - acc: 0.8710
 9152/18000 [==============>...............] - ETA: 4s - loss: 0.3014 - acc: 0.8715
 9280/18000 [==============>...............] - ETA: 4s - loss: 0.3010 - acc: 0.8716
 9408/18000 [==============>...............] - ETA: 4s - loss: 0.3022 - acc: 0.8706
 9536/18000 [==============>...............] - ETA: 4s - loss: 0.3019 - acc: 0.8706
 9664/18000 [===============>..............] - ETA: 4s - loss: 0.3013 - acc: 0.8709
 9792/18000 [===============>..............] - ETA: 4s - loss: 0.3011 - acc: 0.8712
 9920/18000 [===============>..............] - ETA: 4s - loss: 0.3018 - acc: 0.8712
10048/18000 [===============>..............] - ETA: 4s - loss: 0.3017 - acc: 0.8709
10176/18000 [===============>..............] - ETA: 4s - loss: 0.3016 - acc: 0.8708
10304/18000 [================>.............] - ETA: 4s - loss: 0.3021 - acc: 0.8705
10432/18000 [================>.............] - ETA: 4s - loss: 0.3025 - acc: 0.8708
10560/18000 [================>.............] - ETA: 4s - loss: 0.3023 - acc: 0.8711
10688/18000 [================>.............] - ETA: 3s - loss: 0.3033 - acc: 0.8710
10816/18000 [=================>............] - ETA: 3s - loss: 0.3027 - acc: 0.8711
10944/18000 [=================>............] - ETA: 3s - loss: 0.3023 - acc: 0.8712
11072/18000 [=================>............] - ETA: 3s - loss: 0.3029 - acc: 0.8711
11200/18000 [=================>............] - ETA: 3s - loss: 0.3032 - acc: 0.8711
11328/18000 [=================>............] - ETA: 3s - loss: 0.3032 - acc: 0.8710
11456/18000 [==================>...........] - ETA: 3s - loss: 0.3036 - acc: 0.8710
11584/18000 [==================>...........] - ETA: 3s - loss: 0.3037 - acc: 0.8708
11712/18000 [==================>...........] - ETA: 3s - loss: 0.3040 - acc: 0.8710
11840/18000 [==================>...........] - ETA: 3s - loss: 0.3036 - acc: 0.8714
11968/18000 [==================>...........] - ETA: 3s - loss: 0.3035 - acc: 0.8715
12096/18000 [===================>..........] - ETA: 3s - loss: 0.3028 - acc: 0.8718
12224/18000 [===================>..........] - ETA: 3s - loss: 0.3024 - acc: 0.8716
12352/18000 [===================>..........] - ETA: 3s - loss: 0.3020 - acc: 0.8717
12480/18000 [===================>..........] - ETA: 2s - loss: 0.3027 - acc: 0.8716
12608/18000 [====================>.........] - ETA: 2s - loss: 0.3025 - acc: 0.8718
12736/18000 [====================>.........] - ETA: 2s - loss: 0.3035 - acc: 0.8717
12864/18000 [====================>.........] - ETA: 2s - loss: 0.3029 - acc: 0.8720
12992/18000 [====================>.........] - ETA: 2s - loss: 0.3027 - acc: 0.8717
13120/18000 [====================>.........] - ETA: 2s - loss: 0.3025 - acc: 0.8720
13248/18000 [=====================>........] - ETA: 2s - loss: 0.3021 - acc: 0.8722
13376/18000 [=====================>........] - ETA: 2s - loss: 0.3018 - acc: 0.8724
13504/18000 [=====================>........] - ETA: 2s - loss: 0.3016 - acc: 0.8726
13632/18000 [=====================>........] - ETA: 2s - loss: 0.3016 - acc: 0.8725
13760/18000 [=====================>........] - ETA: 2s - loss: 0.3016 - acc: 0.8725
13888/18000 [======================>.......] - ETA: 2s - loss: 0.3026 - acc: 0.8721
14016/18000 [======================>.......] - ETA: 2s - loss: 0.3027 - acc: 0.8721
14144/18000 [======================>.......] - ETA: 2s - loss: 0.3033 - acc: 0.8716
14272/18000 [======================>.......] - ETA: 1s - loss: 0.3035 - acc: 0.8716
14400/18000 [=======================>......] - ETA: 1s - loss: 0.3030 - acc: 0.8717
14528/18000 [=======================>......] - ETA: 1s - loss: 0.3025 - acc: 0.8720
14656/18000 [=======================>......] - ETA: 1s - loss: 0.3026 - acc: 0.8720
14784/18000 [=======================>......] - ETA: 1s - loss: 0.3027 - acc: 0.8717
14912/18000 [=======================>......] - ETA: 1s - loss: 0.3021 - acc: 0.8719
15040/18000 [========================>.....] - ETA: 1s - loss: 0.3024 - acc: 0.8717
15168/18000 [========================>.....] - ETA: 1s - loss: 0.3029 - acc: 0.8716
15296/18000 [========================>.....] - ETA: 1s - loss: 0.3020 - acc: 0.8723
15424/18000 [========================>.....] - ETA: 1s - loss: 0.3018 - acc: 0.8723
15552/18000 [========================>.....] - ETA: 1s - loss: 0.3022 - acc: 0.8720
15680/18000 [=========================>....] - ETA: 1s - loss: 0.3024 - acc: 0.8720
15808/18000 [=========================>....] - ETA: 1s - loss: 0.3027 - acc: 0.8722
15936/18000 [=========================>....] - ETA: 1s - loss: 0.3033 - acc: 0.8720
16064/18000 [=========================>....] - ETA: 1s - loss: 0.3040 - acc: 0.8716
16192/18000 [=========================>....] - ETA: 0s - loss: 0.3038 - acc: 0.8718
16320/18000 [==========================>...] - ETA: 0s - loss: 0.3032 - acc: 0.8721
16448/18000 [==========================>...] - ETA: 0s - loss: 0.3033 - acc: 0.8716
16576/18000 [==========================>...] - ETA: 0s - loss: 0.3031 - acc: 0.8719
16704/18000 [==========================>...] - ETA: 0s - loss: 0.3037 - acc: 0.8718
16832/18000 [===========================>..] - ETA: 0s - loss: 0.3039 - acc: 0.8717
16960/18000 [===========================>..] - ETA: 0s - loss: 0.3045 - acc: 0.8715
17088/18000 [===========================>..] - ETA: 0s - loss: 0.3045 - acc: 0.8714
17216/18000 [===========================>..] - ETA: 0s - loss: 0.3051 - acc: 0.8711
17344/18000 [===========================>..] - ETA: 0s - loss: 0.3051 - acc: 0.8711
17472/18000 [============================>.] - ETA: 0s - loss: 0.3052 - acc: 0.8711
17600/18000 [============================>.] - ETA: 0s - loss: 0.3053 - acc: 0.8709
17728/18000 [============================>.] - ETA: 0s - loss: 0.3056 - acc: 0.8709
17856/18000 [============================>.] - ETA: 0s - loss: 0.3061 - acc: 0.8706
17984/18000 [============================>.] - ETA: 0s - loss: 0.3059 - acc: 0.8707
18000/18000 [==============================] - 10s 533us/step - loss: 0.3058 - acc: 0.8707 - val_loss: 0.2489 - val_acc: 0.8940
Epoch 3/200

   64/18000 [..............................] - ETA: 8s - loss: 0.2931 - acc: 0.9062
  192/18000 [..............................] - ETA: 8s - loss: 0.2768 - acc: 0.8802
  320/18000 [..............................] - ETA: 8s - loss: 0.2629 - acc: 0.8875
  448/18000 [..............................] - ETA: 8s - loss: 0.2723 - acc: 0.8862
  576/18000 [..............................] - ETA: 8s - loss: 0.2875 - acc: 0.8802
  704/18000 [>.............................] - ETA: 8s - loss: 0.3059 - acc: 0.8707
  832/18000 [>.............................] - ETA: 8s - loss: 0.2992 - acc: 0.8750
  960/18000 [>.............................] - ETA: 8s - loss: 0.3093 - acc: 0.8677
 1088/18000 [>.............................] - ETA: 8s - loss: 0.3099 - acc: 0.8704
 1216/18000 [=>............................] - ETA: 8s - loss: 0.3074 - acc: 0.8717
 1344/18000 [=>............................] - ETA: 8s - loss: 0.3040 - acc: 0.8735
 1472/18000 [=>............................] - ETA: 8s - loss: 0.3001 - acc: 0.8750
 1600/18000 [=>............................] - ETA: 8s - loss: 0.3032 - acc: 0.8725
 1728/18000 [=>............................] - ETA: 8s - loss: 0.3001 - acc: 0.8744
 1856/18000 [==>...........................] - ETA: 7s - loss: 0.2956 - acc: 0.8755
 1984/18000 [==>...........................] - ETA: 8s - loss: 0.2915 - acc: 0.8780
 2112/18000 [==>...........................] - ETA: 7s - loss: 0.2897 - acc: 0.8793
 2240/18000 [==>...........................] - ETA: 7s - loss: 0.2902 - acc: 0.8795
 2368/18000 [==>...........................] - ETA: 7s - loss: 0.2895 - acc: 0.8788
 2496/18000 [===>..........................] - ETA: 7s - loss: 0.2867 - acc: 0.8802
 2624/18000 [===>..........................] - ETA: 7s - loss: 0.2899 - acc: 0.8792
 2752/18000 [===>..........................] - ETA: 7s - loss: 0.2899 - acc: 0.8786
 2880/18000 [===>..........................] - ETA: 7s - loss: 0.2903 - acc: 0.8778
 3008/18000 [====>.........................] - ETA: 7s - loss: 0.2934 - acc: 0.8763
 3136/18000 [====>.........................] - ETA: 7s - loss: 0.2953 - acc: 0.8744
 3264/18000 [====>.........................] - ETA: 7s - loss: 0.2927 - acc: 0.8765
 3392/18000 [====>.........................] - ETA: 7s - loss: 0.2895 - acc: 0.8782
 3520/18000 [====>.........................] - ETA: 7s - loss: 0.2883 - acc: 0.8793
 3648/18000 [=====>........................] - ETA: 7s - loss: 0.2867 - acc: 0.8797
 3776/18000 [=====>........................] - ETA: 7s - loss: 0.2867 - acc: 0.8795
 3904/18000 [=====>........................] - ETA: 6s - loss: 0.2881 - acc: 0.8794
 4032/18000 [=====>........................] - ETA: 6s - loss: 0.2880 - acc: 0.8797
 4160/18000 [=====>........................] - ETA: 6s - loss: 0.2860 - acc: 0.8808
 4288/18000 [======>.......................] - ETA: 6s - loss: 0.2861 - acc: 0.8804
 4416/18000 [======>.......................] - ETA: 6s - loss: 0.2871 - acc: 0.8802
 4544/18000 [======>.......................] - ETA: 6s - loss: 0.2872 - acc: 0.8801
 4672/18000 [======>.......................] - ETA: 6s - loss: 0.2853 - acc: 0.8808
 4800/18000 [=======>......................] - ETA: 6s - loss: 0.2878 - acc: 0.8800
 4928/18000 [=======>......................] - ETA: 6s - loss: 0.2883 - acc: 0.8797
 5056/18000 [=======>......................] - ETA: 6s - loss: 0.2878 - acc: 0.8797
 5184/18000 [=======>......................] - ETA: 6s - loss: 0.2911 - acc: 0.8787
 5312/18000 [=======>......................] - ETA: 6s - loss: 0.2905 - acc: 0.8793
 5440/18000 [========>.....................] - ETA: 6s - loss: 0.2914 - acc: 0.8790
 5568/18000 [========>.....................] - ETA: 6s - loss: 0.2897 - acc: 0.8795
 5696/18000 [========>.....................] - ETA: 6s - loss: 0.2882 - acc: 0.8801
 5824/18000 [========>.....................] - ETA: 6s - loss: 0.2870 - acc: 0.8810
 5952/18000 [========>.....................] - ETA: 5s - loss: 0.2871 - acc: 0.8802
 6080/18000 [=========>....................] - ETA: 5s - loss: 0.2867 - acc: 0.8803
 6208/18000 [=========>....................] - ETA: 5s - loss: 0.2868 - acc: 0.8802
 6336/18000 [=========>....................] - ETA: 5s - loss: 0.2872 - acc: 0.8805
 6464/18000 [=========>....................] - ETA: 5s - loss: 0.2862 - acc: 0.8815
 6592/18000 [=========>....................] - ETA: 5s - loss: 0.2862 - acc: 0.8815
 6720/18000 [==========>...................] - ETA: 5s - loss: 0.2871 - acc: 0.8807
 6848/18000 [==========>...................] - ETA: 5s - loss: 0.2849 - acc: 0.8822
 6976/18000 [==========>...................] - ETA: 5s - loss: 0.2858 - acc: 0.8813
 7104/18000 [==========>...................] - ETA: 5s - loss: 0.2853 - acc: 0.8818
 7232/18000 [===========>..................] - ETA: 5s - loss: 0.2856 - acc: 0.8815
 7360/18000 [===========>..................] - ETA: 5s - loss: 0.2843 - acc: 0.8822
 7488/18000 [===========>..................] - ETA: 5s - loss: 0.2843 - acc: 0.8819
 7616/18000 [===========>..................] - ETA: 5s - loss: 0.2842 - acc: 0.8818
 7744/18000 [===========>..................] - ETA: 5s - loss: 0.2843 - acc: 0.8813
 7872/18000 [============>.................] - ETA: 5s - loss: 0.2826 - acc: 0.8824
 8000/18000 [============>.................] - ETA: 4s - loss: 0.2833 - acc: 0.8826
 8128/18000 [============>.................] - ETA: 4s - loss: 0.2848 - acc: 0.8815
 8256/18000 [============>.................] - ETA: 4s - loss: 0.2853 - acc: 0.8812
 8384/18000 [============>.................] - ETA: 4s - loss: 0.2854 - acc: 0.8812
 8512/18000 [=============>................] - ETA: 4s - loss: 0.2848 - acc: 0.8815
 8640/18000 [=============>................] - ETA: 4s - loss: 0.2843 - acc: 0.8818
 8768/18000 [=============>................] - ETA: 4s - loss: 0.2850 - acc: 0.8812
 8896/18000 [=============>................] - ETA: 4s - loss: 0.2839 - acc: 0.8816
 9024/18000 [==============>...............] - ETA: 4s - loss: 0.2846 - acc: 0.8816
 9152/18000 [==============>...............] - ETA: 4s - loss: 0.2847 - acc: 0.8816
 9280/18000 [==============>...............] - ETA: 4s - loss: 0.2837 - acc: 0.8822
 9408/18000 [==============>...............] - ETA: 4s - loss: 0.2836 - acc: 0.8824
 9536/18000 [==============>...............] - ETA: 4s - loss: 0.2845 - acc: 0.8821
 9664/18000 [===============>..............] - ETA: 4s - loss: 0.2845 - acc: 0.8822
 9792/18000 [===============>..............] - ETA: 4s - loss: 0.2833 - acc: 0.8831
 9920/18000 [===============>..............] - ETA: 4s - loss: 0.2842 - acc: 0.8826
10048/18000 [===============>..............] - ETA: 3s - loss: 0.2843 - acc: 0.8827
10176/18000 [===============>..............] - ETA: 3s - loss: 0.2843 - acc: 0.8829
10304/18000 [================>.............] - ETA: 3s - loss: 0.2849 - acc: 0.8827
10432/18000 [================>.............] - ETA: 3s - loss: 0.2844 - acc: 0.8826
10560/18000 [================>.............] - ETA: 3s - loss: 0.2831 - acc: 0.8832
10688/18000 [================>.............] - ETA: 3s - loss: 0.2834 - acc: 0.8829
10816/18000 [=================>............] - ETA: 3s - loss: 0.2829 - acc: 0.8833
10944/18000 [=================>............] - ETA: 3s - loss: 0.2824 - acc: 0.8835
11072/18000 [=================>............] - ETA: 3s - loss: 0.2839 - acc: 0.8827
11200/18000 [=================>............] - ETA: 3s - loss: 0.2828 - acc: 0.8833
11328/18000 [=================>............] - ETA: 3s - loss: 0.2826 - acc: 0.8835
11456/18000 [==================>...........] - ETA: 3s - loss: 0.2829 - acc: 0.8835
11584/18000 [==================>...........] - ETA: 3s - loss: 0.2826 - acc: 0.8836
11712/18000 [==================>...........] - ETA: 3s - loss: 0.2823 - acc: 0.8831
11840/18000 [==================>...........] - ETA: 3s - loss: 0.2824 - acc: 0.8830
11968/18000 [==================>...........] - ETA: 3s - loss: 0.2815 - acc: 0.8834
12096/18000 [===================>..........] - ETA: 2s - loss: 0.2817 - acc: 0.8837
12224/18000 [===================>..........] - ETA: 2s - loss: 0.2832 - acc: 0.8829
12352/18000 [===================>..........] - ETA: 2s - loss: 0.2830 - acc: 0.8827
12480/18000 [===================>..........] - ETA: 2s - loss: 0.2834 - acc: 0.8827
12608/18000 [====================>.........] - ETA: 2s - loss: 0.2844 - acc: 0.8824
12736/18000 [====================>.........] - ETA: 2s - loss: 0.2838 - acc: 0.8824
12864/18000 [====================>.........] - ETA: 2s - loss: 0.2841 - acc: 0.8820
12992/18000 [====================>.........] - ETA: 2s - loss: 0.2839 - acc: 0.8822
13120/18000 [====================>.........] - ETA: 2s - loss: 0.2833 - acc: 0.8825
13248/18000 [=====================>........] - ETA: 2s - loss: 0.2841 - acc: 0.8821
13376/18000 [=====================>........] - ETA: 2s - loss: 0.2837 - acc: 0.8824
13504/18000 [=====================>........] - ETA: 2s - loss: 0.2844 - acc: 0.8821
13632/18000 [=====================>........] - ETA: 2s - loss: 0.2847 - acc: 0.8823
13760/18000 [=====================>........] - ETA: 2s - loss: 0.2854 - acc: 0.8820
13888/18000 [======================>.......] - ETA: 2s - loss: 0.2856 - acc: 0.8816
14016/18000 [======================>.......] - ETA: 1s - loss: 0.2865 - acc: 0.8812
14144/18000 [======================>.......] - ETA: 1s - loss: 0.2867 - acc: 0.8808
14272/18000 [======================>.......] - ETA: 1s - loss: 0.2864 - acc: 0.8809
14400/18000 [=======================>......] - ETA: 1s - loss: 0.2867 - acc: 0.8808
14528/18000 [=======================>......] - ETA: 1s - loss: 0.2875 - acc: 0.8804
14656/18000 [=======================>......] - ETA: 1s - loss: 0.2884 - acc: 0.8798
14784/18000 [=======================>......] - ETA: 1s - loss: 0.2887 - acc: 0.8797
14912/18000 [=======================>......] - ETA: 1s - loss: 0.2898 - acc: 0.8793
15040/18000 [========================>.....] - ETA: 1s - loss: 0.2897 - acc: 0.8792
15168/18000 [========================>.....] - ETA: 1s - loss: 0.2894 - acc: 0.8793
15296/18000 [========================>.....] - ETA: 1s - loss: 0.2890 - acc: 0.8795
15424/18000 [========================>.....] - ETA: 1s - loss: 0.2887 - acc: 0.8799
15552/18000 [========================>.....] - ETA: 1s - loss: 0.2888 - acc: 0.8796
15680/18000 [=========================>....] - ETA: 1s - loss: 0.2897 - acc: 0.8791
15808/18000 [=========================>....] - ETA: 1s - loss: 0.2901 - acc: 0.8790
15936/18000 [=========================>....] - ETA: 1s - loss: 0.2909 - acc: 0.8789
16064/18000 [=========================>....] - ETA: 0s - loss: 0.2918 - acc: 0.8783
16192/18000 [=========================>....] - ETA: 0s - loss: 0.2914 - acc: 0.8786
16320/18000 [==========================>...] - ETA: 0s - loss: 0.2914 - acc: 0.8787
16448/18000 [==========================>...] - ETA: 0s - loss: 0.2914 - acc: 0.8786
16576/18000 [==========================>...] - ETA: 0s - loss: 0.2915 - acc: 0.8787
16704/18000 [==========================>...] - ETA: 0s - loss: 0.2915 - acc: 0.8784
16832/18000 [===========================>..] - ETA: 0s - loss: 0.2918 - acc: 0.8783
16960/18000 [===========================>..] - ETA: 0s - loss: 0.2918 - acc: 0.8784
17088/18000 [===========================>..] - ETA: 0s - loss: 0.2917 - acc: 0.8784
17216/18000 [===========================>..] - ETA: 0s - loss: 0.2916 - acc: 0.8784
17344/18000 [===========================>..] - ETA: 0s - loss: 0.2912 - acc: 0.8786
17472/18000 [============================>.] - ETA: 0s - loss: 0.2911 - acc: 0.8789
17600/18000 [============================>.] - ETA: 0s - loss: 0.2909 - acc: 0.8788
17728/18000 [============================>.] - ETA: 0s - loss: 0.2908 - acc: 0.8788
17856/18000 [============================>.] - ETA: 0s - loss: 0.2903 - acc: 0.8790
17984/18000 [============================>.] - ETA: 0s - loss: 0.2900 - acc: 0.8789
18000/18000 [==============================] - 9s 513us/step - loss: 0.2899 - acc: 0.8790 - val_loss: 0.2516 - val_acc: 0.8860
Epoch 4/200

   64/18000 [..............................] - ETA: 9s - loss: 0.4894 - acc: 0.7969
  192/18000 [..............................] - ETA: 9s - loss: 0.3674 - acc: 0.8385
  320/18000 [..............................] - ETA: 9s - loss: 0.3517 - acc: 0.8438
  448/18000 [..............................] - ETA: 9s - loss: 0.3184 - acc: 0.8594
  576/18000 [..............................] - ETA: 9s - loss: 0.3173 - acc: 0.8628
  704/18000 [>.............................] - ETA: 9s - loss: 0.3102 - acc: 0.8693
  832/18000 [>.............................] - ETA: 8s - loss: 0.3134 - acc: 0.8666
  960/18000 [>.............................] - ETA: 8s - loss: 0.3060 - acc: 0.8698
 1088/18000 [>.............................] - ETA: 8s - loss: 0.2997 - acc: 0.8722
 1216/18000 [=>............................] - ETA: 8s - loss: 0.2963 - acc: 0.8766
 1344/18000 [=>............................] - ETA: 8s - loss: 0.2967 - acc: 0.8765
 1472/18000 [=>............................] - ETA: 8s - loss: 0.2908 - acc: 0.8784
 1600/18000 [=>............................] - ETA: 8s - loss: 0.2907 - acc: 0.8781
 1728/18000 [=>............................] - ETA: 8s - loss: 0.2942 - acc: 0.8762
 1856/18000 [==>...........................] - ETA: 8s - loss: 0.2918 - acc: 0.8761
 1984/18000 [==>...........................] - ETA: 8s - loss: 0.2843 - acc: 0.8800
 2112/18000 [==>...........................] - ETA: 8s - loss: 0.2842 - acc: 0.8807
 2240/18000 [==>...........................] - ETA: 8s - loss: 0.2850 - acc: 0.8804
 2368/18000 [==>...........................] - ETA: 7s - loss: 0.2846 - acc: 0.8809
 2496/18000 [===>..........................] - ETA: 7s - loss: 0.2806 - acc: 0.8826
 2624/18000 [===>..........................] - ETA: 7s - loss: 0.2785 - acc: 0.8834
 2752/18000 [===>..........................] - ETA: 7s - loss: 0.2792 - acc: 0.8819
 2880/18000 [===>..........................] - ETA: 7s - loss: 0.2808 - acc: 0.8799
 3008/18000 [====>.........................] - ETA: 7s - loss: 0.2788 - acc: 0.8807
 3136/18000 [====>.........................] - ETA: 7s - loss: 0.2802 - acc: 0.8795
 3264/18000 [====>.........................] - ETA: 7s - loss: 0.2771 - acc: 0.8814
 3392/18000 [====>.........................] - ETA: 7s - loss: 0.2772 - acc: 0.8818
 3520/18000 [====>.........................] - ETA: 7s - loss: 0.2766 - acc: 0.8832
 3648/18000 [=====>........................] - ETA: 7s - loss: 0.2747 - acc: 0.8843
 3776/18000 [=====>........................] - ETA: 7s - loss: 0.2731 - acc: 0.8845
 3904/18000 [=====>........................] - ETA: 7s - loss: 0.2747 - acc: 0.8832
 4032/18000 [=====>........................] - ETA: 7s - loss: 0.2741 - acc: 0.8834
 4160/18000 [=====>........................] - ETA: 7s - loss: 0.2738 - acc: 0.8832
 4288/18000 [======>.......................] - ETA: 6s - loss: 0.2725 - acc: 0.8839
 4416/18000 [======>.......................] - ETA: 6s - loss: 0.2708 - acc: 0.8841
 4544/18000 [======>.......................] - ETA: 6s - loss: 0.2732 - acc: 0.8838
 4672/18000 [======>.......................] - ETA: 6s - loss: 0.2743 - acc: 0.8838
 4800/18000 [=======>......................] - ETA: 6s - loss: 0.2758 - acc: 0.8833
 4928/18000 [=======>......................] - ETA: 6s - loss: 0.2759 - acc: 0.8837
 5056/18000 [=======>......................] - ETA: 6s - loss: 0.2749 - acc: 0.8847
 5184/18000 [=======>......................] - ETA: 6s - loss: 0.2749 - acc: 0.8848
 5312/18000 [=======>......................] - ETA: 6s - loss: 0.2759 - acc: 0.8846
 5440/18000 [========>.....................] - ETA: 6s - loss: 0.2757 - acc: 0.8855
 5504/18000 [========>.....................] - ETA: 6s - loss: 0.2761 - acc: 0.8857
 5632/18000 [========>.....................] - ETA: 6s - loss: 0.2735 - acc: 0.8867
 5760/18000 [========>.....................] - ETA: 6s - loss: 0.2765 - acc: 0.8854
 5888/18000 [========>.....................] - ETA: 6s - loss: 0.2753 - acc: 0.8857
 6016/18000 [=========>....................] - ETA: 6s - loss: 0.2751 - acc: 0.8858
 6144/18000 [=========>....................] - ETA: 6s - loss: 0.2748 - acc: 0.8861
 6272/18000 [=========>....................] - ETA: 6s - loss: 0.2759 - acc: 0.8852
 6400/18000 [=========>....................] - ETA: 5s - loss: 0.2754 - acc: 0.8853
 6528/18000 [=========>....................] - ETA: 5s - loss: 0.2759 - acc: 0.8854
 6656/18000 [==========>...................] - ETA: 5s - loss: 0.2755 - acc: 0.8852
 6784/18000 [==========>...................] - ETA: 5s - loss: 0.2753 - acc: 0.8852
 6912/18000 [==========>...................] - ETA: 5s - loss: 0.2770 - acc: 0.8848
 7040/18000 [==========>...................] - ETA: 5s - loss: 0.2783 - acc: 0.8842
 7168/18000 [==========>...................] - ETA: 5s - loss: 0.2796 - acc: 0.8836
 7296/18000 [===========>..................] - ETA: 5s - loss: 0.2795 - acc: 0.8832
 7424/18000 [===========>..................] - ETA: 5s - loss: 0.2791 - acc: 0.8831
 7552/18000 [===========>..................] - ETA: 5s - loss: 0.2803 - acc: 0.8825
 7680/18000 [===========>..................] - ETA: 5s - loss: 0.2805 - acc: 0.8823
 7808/18000 [============>.................] - ETA: 5s - loss: 0.2807 - acc: 0.8826
 7936/18000 [============>.................] - ETA: 5s - loss: 0.2801 - acc: 0.8832
 8064/18000 [============>.................] - ETA: 5s - loss: 0.2795 - acc: 0.8836
 8192/18000 [============>.................] - ETA: 5s - loss: 0.2795 - acc: 0.8837
 8320/18000 [============>.................] - ETA: 4s - loss: 0.2805 - acc: 0.8834
 8448/18000 [=============>................] - ETA: 4s - loss: 0.2813 - acc: 0.8828
 8576/18000 [=============>................] - ETA: 4s - loss: 0.2835 - acc: 0.8818
 8704/18000 [=============>................] - ETA: 4s - loss: 0.2845 - acc: 0.8817
 8832/18000 [=============>................] - ETA: 4s - loss: 0.2834 - acc: 0.8818
 8960/18000 [=============>................] - ETA: 4s - loss: 0.2832 - acc: 0.8817
 9088/18000 [==============>...............] - ETA: 4s - loss: 0.2838 - acc: 0.8813
 9152/18000 [==============>...............] - ETA: 4s - loss: 0.2834 - acc: 0.8812
 9280/18000 [==============>...............] - ETA: 4s - loss: 0.2826 - acc: 0.8815
 9408/18000 [==============>...............] - ETA: 4s - loss: 0.2815 - acc: 0.8821
 9536/18000 [==============>...............] - ETA: 4s - loss: 0.2818 - acc: 0.8821
 9664/18000 [===============>..............] - ETA: 4s - loss: 0.2819 - acc: 0.8821
 9792/18000 [===============>..............] - ETA: 4s - loss: 0.2816 - acc: 0.8823
 9920/18000 [===============>..............] - ETA: 4s - loss: 0.2812 - acc: 0.8823
10048/18000 [===============>..............] - ETA: 4s - loss: 0.2814 - acc: 0.8823
10176/18000 [===============>..............] - ETA: 4s - loss: 0.2817 - acc: 0.8822
10304/18000 [================>.............] - ETA: 4s - loss: 0.2810 - acc: 0.8825
10432/18000 [================>.............] - ETA: 4s - loss: 0.2807 - acc: 0.8828
10560/18000 [================>.............] - ETA: 3s - loss: 0.2804 - acc: 0.8829
10688/18000 [================>.............] - ETA: 3s - loss: 0.2809 - acc: 0.8827
10816/18000 [=================>............] - ETA: 3s - loss: 0.2821 - acc: 0.8822
10880/18000 [=================>............] - ETA: 3s - loss: 0.2816 - acc: 0.8823
11008/18000 [=================>............] - ETA: 3s - loss: 0.2823 - acc: 0.8819
11136/18000 [=================>............] - ETA: 3s - loss: 0.2822 - acc: 0.8821
11264/18000 [=================>............] - ETA: 3s - loss: 0.2817 - acc: 0.8825
11392/18000 [=================>............] - ETA: 3s - loss: 0.2816 - acc: 0.8825
11520/18000 [==================>...........] - ETA: 3s - loss: 0.2818 - acc: 0.8826
11648/18000 [==================>...........] - ETA: 3s - loss: 0.2813 - acc: 0.8827
11776/18000 [==================>...........] - ETA: 3s - loss: 0.2808 - acc: 0.8832
11904/18000 [==================>...........] - ETA: 3s - loss: 0.2804 - acc: 0.8833
12032/18000 [===================>..........] - ETA: 3s - loss: 0.2806 - acc: 0.8831
12160/18000 [===================>..........] - ETA: 3s - loss: 0.2808 - acc: 0.8832
12288/18000 [===================>..........] - ETA: 3s - loss: 0.2822 - acc: 0.8825
12416/18000 [===================>..........] - ETA: 2s - loss: 0.2818 - acc: 0.8825
12544/18000 [===================>..........] - ETA: 2s - loss: 0.2821 - acc: 0.8823
12672/18000 [====================>.........] - ETA: 2s - loss: 0.2821 - acc: 0.8823
12800/18000 [====================>.........] - ETA: 2s - loss: 0.2827 - acc: 0.8820
12928/18000 [====================>.........] - ETA: 2s - loss: 0.2818 - acc: 0.8824
13056/18000 [====================>.........] - ETA: 2s - loss: 0.2815 - acc: 0.8827
13184/18000 [====================>.........] - ETA: 2s - loss: 0.2819 - acc: 0.8821
13312/18000 [=====================>........] - ETA: 2s - loss: 0.2819 - acc: 0.8821
13440/18000 [=====================>........] - ETA: 2s - loss: 0.2812 - acc: 0.8821
13568/18000 [=====================>........] - ETA: 2s - loss: 0.2802 - acc: 0.8826
13696/18000 [=====================>........] - ETA: 2s - loss: 0.2809 - acc: 0.8822
13824/18000 [======================>.......] - ETA: 2s - loss: 0.2808 - acc: 0.8823
13952/18000 [======================>.......] - ETA: 2s - loss: 0.2802 - acc: 0.8825
14080/18000 [======================>.......] - ETA: 2s - loss: 0.2810 - acc: 0.8820
14208/18000 [======================>.......] - ETA: 2s - loss: 0.2810 - acc: 0.8820
14336/18000 [======================>.......] - ETA: 1s - loss: 0.2810 - acc: 0.8821
14464/18000 [=======================>......] - ETA: 1s - loss: 0.2813 - acc: 0.8819
14592/18000 [=======================>......] - ETA: 1s - loss: 0.2809 - acc: 0.8823
14720/18000 [=======================>......] - ETA: 1s - loss: 0.2810 - acc: 0.8823
14848/18000 [=======================>......] - ETA: 1s - loss: 0.2808 - acc: 0.8824
14976/18000 [=======================>......] - ETA: 1s - loss: 0.2806 - acc: 0.8824
15104/18000 [========================>.....] - ETA: 1s - loss: 0.2805 - acc: 0.8826
15232/18000 [========================>.....] - ETA: 1s - loss: 0.2802 - acc: 0.8827
15360/18000 [========================>.....] - ETA: 1s - loss: 0.2797 - acc: 0.8830
15488/18000 [========================>.....] - ETA: 1s - loss: 0.2792 - acc: 0.8833
15616/18000 [=========================>....] - ETA: 1s - loss: 0.2798 - acc: 0.8830
15744/18000 [=========================>....] - ETA: 1s - loss: 0.2797 - acc: 0.8831
15872/18000 [=========================>....] - ETA: 1s - loss: 0.2798 - acc: 0.8829
16000/18000 [=========================>....] - ETA: 1s - loss: 0.2794 - acc: 0.8832
16128/18000 [=========================>....] - ETA: 1s - loss: 0.2790 - acc: 0.8832
16256/18000 [==========================>...] - ETA: 0s - loss: 0.2791 - acc: 0.8830
16384/18000 [==========================>...] - ETA: 0s - loss: 0.2792 - acc: 0.8829
16512/18000 [==========================>...] - ETA: 0s - loss: 0.2788 - acc: 0.8832
16640/18000 [==========================>...] - ETA: 0s - loss: 0.2795 - acc: 0.8828
16768/18000 [==========================>...] - ETA: 0s - loss: 0.2795 - acc: 0.8826
16896/18000 [===========================>..] - ETA: 0s - loss: 0.2798 - acc: 0.8825
17024/18000 [===========================>..] - ETA: 0s - loss: 0.2806 - acc: 0.8820
17152/18000 [===========================>..] - ETA: 0s - loss: 0.2807 - acc: 0.8819
17280/18000 [===========================>..] - ETA: 0s - loss: 0.2811 - acc: 0.8816
17408/18000 [============================>.] - ETA: 0s - loss: 0.2808 - acc: 0.8819
17536/18000 [============================>.] - ETA: 0s - loss: 0.2810 - acc: 0.8817
17664/18000 [============================>.] - ETA: 0s - loss: 0.2811 - acc: 0.8817
17792/18000 [============================>.] - ETA: 0s - loss: 0.2812 - acc: 0.8816
17920/18000 [============================>.] - ETA: 0s - loss: 0.2813 - acc: 0.8816
18000/18000 [==============================] - 10s 548us/step - loss: 0.2813 - acc: 0.8816 - val_loss: 0.2440 - val_acc: 0.8980
Epoch 5/200

   64/18000 [..............................] - ETA: 9s - loss: 0.3027 - acc: 0.8906
  192/18000 [..............................] - ETA: 10s - loss: 0.3158 - acc: 0.8594
  320/18000 [..............................] - ETA: 9s - loss: 0.3316 - acc: 0.8562 
  448/18000 [..............................] - ETA: 9s - loss: 0.2918 - acc: 0.8772
  576/18000 [..............................] - ETA: 9s - loss: 0.2905 - acc: 0.8750
  704/18000 [>.............................] - ETA: 9s - loss: 0.2826 - acc: 0.8793
  832/18000 [>.............................] - ETA: 9s - loss: 0.2700 - acc: 0.8870
  960/18000 [>.............................] - ETA: 9s - loss: 0.2652 - acc: 0.8896
 1088/18000 [>.............................] - ETA: 9s - loss: 0.2707 - acc: 0.8842
 1216/18000 [=>............................] - ETA: 9s - loss: 0.2755 - acc: 0.8832
 1344/18000 [=>............................] - ETA: 8s - loss: 0.2813 - acc: 0.8802
 1472/18000 [=>............................] - ETA: 8s - loss: 0.2859 - acc: 0.8777
 1600/18000 [=>............................] - ETA: 8s - loss: 0.2867 - acc: 0.8756
 1728/18000 [=>............................] - ETA: 8s - loss: 0.2885 - acc: 0.8756
 1856/18000 [==>...........................] - ETA: 8s - loss: 0.2872 - acc: 0.8777
 1984/18000 [==>...........................] - ETA: 8s - loss: 0.2829 - acc: 0.8805
 2112/18000 [==>...........................] - ETA: 8s - loss: 0.2830 - acc: 0.8793
 2240/18000 [==>...........................] - ETA: 8s - loss: 0.2888 - acc: 0.8763
 2368/18000 [==>...........................] - ETA: 8s - loss: 0.2896 - acc: 0.8775
 2496/18000 [===>..........................] - ETA: 8s - loss: 0.2875 - acc: 0.8794
 2624/18000 [===>..........................] - ETA: 8s - loss: 0.2877 - acc: 0.8796
 2752/18000 [===>..........................] - ETA: 7s - loss: 0.2843 - acc: 0.8815
 2880/18000 [===>..........................] - ETA: 7s - loss: 0.2859 - acc: 0.8816
 3008/18000 [====>.........................] - ETA: 7s - loss: 0.2831 - acc: 0.8826
 3136/18000 [====>.........................] - ETA: 7s - loss: 0.2825 - acc: 0.8827
 3264/18000 [====>.........................] - ETA: 7s - loss: 0.2813 - acc: 0.8839
 3392/18000 [====>.........................] - ETA: 7s - loss: 0.2806 - acc: 0.8844
 3520/18000 [====>.........................] - ETA: 7s - loss: 0.2766 - acc: 0.8872
 3648/18000 [=====>........................] - ETA: 7s - loss: 0.2744 - acc: 0.8882
 3776/18000 [=====>........................] - ETA: 7s - loss: 0.2749 - acc: 0.8880
 3904/18000 [=====>........................] - ETA: 7s - loss: 0.2746 - acc: 0.8881
 4032/18000 [=====>........................] - ETA: 7s - loss: 0.2745 - acc: 0.8881
 4160/18000 [=====>........................] - ETA: 7s - loss: 0.2750 - acc: 0.8880
 4288/18000 [======>.......................] - ETA: 7s - loss: 0.2757 - acc: 0.8883
 4416/18000 [======>.......................] - ETA: 7s - loss: 0.2745 - acc: 0.8895
 4544/18000 [======>.......................] - ETA: 7s - loss: 0.2744 - acc: 0.8891
 4672/18000 [======>.......................] - ETA: 7s - loss: 0.2744 - acc: 0.8889
 4800/18000 [=======>......................] - ETA: 7s - loss: 0.2753 - acc: 0.8888
 4928/18000 [=======>......................] - ETA: 7s - loss: 0.2750 - acc: 0.8894
 5056/18000 [=======>......................] - ETA: 6s - loss: 0.2767 - acc: 0.8884
 5184/18000 [=======>......................] - ETA: 6s - loss: 0.2752 - acc: 0.8887
 5312/18000 [=======>......................] - ETA: 6s - loss: 0.2766 - acc: 0.8880
 5440/18000 [========>.....................] - ETA: 6s - loss: 0.2771 - acc: 0.8879
 5568/18000 [========>.....................] - ETA: 6s - loss: 0.2762 - acc: 0.8885
 5696/18000 [========>.....................] - ETA: 6s - loss: 0.2746 - acc: 0.8892
 5824/18000 [========>.....................] - ETA: 6s - loss: 0.2748 - acc: 0.8887
 5952/18000 [========>.....................] - ETA: 6s - loss: 0.2768 - acc: 0.8888
 6080/18000 [=========>....................] - ETA: 6s - loss: 0.2770 - acc: 0.8885
 6208/18000 [=========>....................] - ETA: 6s - loss: 0.2754 - acc: 0.8889
 6336/18000 [=========>....................] - ETA: 6s - loss: 0.2751 - acc: 0.8890
 6464/18000 [=========>....................] - ETA: 6s - loss: 0.2751 - acc: 0.8886
 6592/18000 [=========>....................] - ETA: 6s - loss: 0.2762 - acc: 0.8879
 6720/18000 [==========>...................] - ETA: 5s - loss: 0.2744 - acc: 0.8890
 6848/18000 [==========>...................] - ETA: 5s - loss: 0.2750 - acc: 0.8884
 6976/18000 [==========>...................] - ETA: 5s - loss: 0.2752 - acc: 0.8883
 7104/18000 [==========>...................] - ETA: 5s - loss: 0.2762 - acc: 0.8877
 7232/18000 [===========>..................] - ETA: 5s - loss: 0.2753 - acc: 0.8880
 7360/18000 [===========>..................] - ETA: 5s - loss: 0.2742 - acc: 0.8886
 7488/18000 [===========>..................] - ETA: 5s - loss: 0.2744 - acc: 0.8884
 7616/18000 [===========>..................] - ETA: 5s - loss: 0.2749 - acc: 0.8880
 7744/18000 [===========>..................] - ETA: 5s - loss: 0.2749 - acc: 0.8880
 7872/18000 [============>.................] - ETA: 5s - loss: 0.2746 - acc: 0.8882
 8000/18000 [============>.................] - ETA: 5s - loss: 0.2744 - acc: 0.8884
 8128/18000 [============>.................] - ETA: 5s - loss: 0.2743 - acc: 0.8885
 8256/18000 [============>.................] - ETA: 5s - loss: 0.2744 - acc: 0.8882
 8384/18000 [============>.................] - ETA: 5s - loss: 0.2741 - acc: 0.8882
 8512/18000 [=============>................] - ETA: 5s - loss: 0.2728 - acc: 0.8890
 8640/18000 [=============>................] - ETA: 5s - loss: 0.2727 - acc: 0.8890
 8768/18000 [=============>................] - ETA: 4s - loss: 0.2725 - acc: 0.8890
 8896/18000 [=============>................] - ETA: 4s - loss: 0.2718 - acc: 0.8893
 9024/18000 [==============>...............] - ETA: 4s - loss: 0.2715 - acc: 0.8895
 9152/18000 [==============>...............] - ETA: 4s - loss: 0.2717 - acc: 0.8896
 9280/18000 [==============>...............] - ETA: 4s - loss: 0.2718 - acc: 0.8898
 9408/18000 [==============>...............] - ETA: 4s - loss: 0.2712 - acc: 0.8899
 9536/18000 [==============>...............] - ETA: 4s - loss: 0.2708 - acc: 0.8897
 9664/18000 [===============>..............] - ETA: 4s - loss: 0.2703 - acc: 0.8902
 9792/18000 [===============>..............] - ETA: 4s - loss: 0.2700 - acc: 0.8901
 9920/18000 [===============>..............] - ETA: 4s - loss: 0.2708 - acc: 0.8896
10048/18000 [===============>..............] - ETA: 4s - loss: 0.2714 - acc: 0.8892
10176/18000 [===============>..............] - ETA: 4s - loss: 0.2712 - acc: 0.8894
10304/18000 [================>.............] - ETA: 4s - loss: 0.2709 - acc: 0.8894
10432/18000 [================>.............] - ETA: 4s - loss: 0.2711 - acc: 0.8896
10560/18000 [================>.............] - ETA: 3s - loss: 0.2717 - acc: 0.8891
10688/18000 [================>.............] - ETA: 3s - loss: 0.2714 - acc: 0.8893
10816/18000 [=================>............] - ETA: 3s - loss: 0.2713 - acc: 0.8895
10944/18000 [=================>............] - ETA: 3s - loss: 0.2719 - acc: 0.8889
11072/18000 [=================>............] - ETA: 3s - loss: 0.2727 - acc: 0.8890
11200/18000 [=================>............] - ETA: 3s - loss: 0.2727 - acc: 0.8889
11328/18000 [=================>............] - ETA: 3s - loss: 0.2727 - acc: 0.8890
11456/18000 [==================>...........] - ETA: 3s - loss: 0.2726 - acc: 0.8889
11584/18000 [==================>...........] - ETA: 3s - loss: 0.2733 - acc: 0.8888
11712/18000 [==================>...........] - ETA: 3s - loss: 0.2735 - acc: 0.8887
11840/18000 [==================>...........] - ETA: 3s - loss: 0.2747 - acc: 0.8884
11968/18000 [==================>...........] - ETA: 3s - loss: 0.2746 - acc: 0.8883
12096/18000 [===================>..........] - ETA: 3s - loss: 0.2744 - acc: 0.8883
12224/18000 [===================>..........] - ETA: 3s - loss: 0.2741 - acc: 0.8884
12352/18000 [===================>..........] - ETA: 3s - loss: 0.2739 - acc: 0.8888
12480/18000 [===================>..........] - ETA: 2s - loss: 0.2745 - acc: 0.8889
12608/18000 [====================>.........] - ETA: 2s - loss: 0.2744 - acc: 0.8890
12736/18000 [====================>.........] - ETA: 2s - loss: 0.2741 - acc: 0.8894
12864/18000 [====================>.........] - ETA: 2s - loss: 0.2742 - acc: 0.8895
12992/18000 [====================>.........] - ETA: 2s - loss: 0.2744 - acc: 0.8892
13120/18000 [====================>.........] - ETA: 2s - loss: 0.2740 - acc: 0.8896
13248/18000 [=====================>........] - ETA: 2s - loss: 0.2742 - acc: 0.8892
13376/18000 [=====================>........] - ETA: 2s - loss: 0.2756 - acc: 0.8885
13504/18000 [=====================>........] - ETA: 2s - loss: 0.2760 - acc: 0.8880
13632/18000 [=====================>........] - ETA: 2s - loss: 0.2764 - acc: 0.8877
13760/18000 [=====================>........] - ETA: 2s - loss: 0.2766 - acc: 0.8875
13888/18000 [======================>.......] - ETA: 2s - loss: 0.2772 - acc: 0.8873
14016/18000 [======================>.......] - ETA: 2s - loss: 0.2782 - acc: 0.8868
14144/18000 [======================>.......] - ETA: 2s - loss: 0.2782 - acc: 0.8865
14272/18000 [======================>.......] - ETA: 1s - loss: 0.2781 - acc: 0.8865
14400/18000 [=======================>......] - ETA: 1s - loss: 0.2783 - acc: 0.8865
14528/18000 [=======================>......] - ETA: 1s - loss: 0.2786 - acc: 0.8865
14592/18000 [=======================>......] - ETA: 1s - loss: 0.2781 - acc: 0.8867
14720/18000 [=======================>......] - ETA: 1s - loss: 0.2780 - acc: 0.8865
14848/18000 [=======================>......] - ETA: 1s - loss: 0.2781 - acc: 0.8868
14976/18000 [=======================>......] - ETA: 1s - loss: 0.2778 - acc: 0.8872
15104/18000 [========================>.....] - ETA: 1s - loss: 0.2779 - acc: 0.8872
15232/18000 [========================>.....] - ETA: 1s - loss: 0.2777 - acc: 0.8873
15360/18000 [========================>.....] - ETA: 1s - loss: 0.2777 - acc: 0.8872
15488/18000 [========================>.....] - ETA: 1s - loss: 0.2774 - acc: 0.8873
15616/18000 [=========================>....] - ETA: 1s - loss: 0.2773 - acc: 0.8875
15744/18000 [=========================>....] - ETA: 1s - loss: 0.2773 - acc: 0.8875
15872/18000 [=========================>....] - ETA: 1s - loss: 0.2778 - acc: 0.8874
16000/18000 [=========================>....] - ETA: 1s - loss: 0.2779 - acc: 0.8871
16128/18000 [=========================>....] - ETA: 1s - loss: 0.2779 - acc: 0.8872
16256/18000 [==========================>...] - ETA: 0s - loss: 0.2783 - acc: 0.8871
16384/18000 [==========================>...] - ETA: 0s - loss: 0.2779 - acc: 0.8871
16512/18000 [==========================>...] - ETA: 0s - loss: 0.2780 - acc: 0.8871
16640/18000 [==========================>...] - ETA: 0s - loss: 0.2779 - acc: 0.8869
16768/18000 [==========================>...] - ETA: 0s - loss: 0.2778 - acc: 0.8869
16896/18000 [===========================>..] - ETA: 0s - loss: 0.2776 - acc: 0.8870
17024/18000 [===========================>..] - ETA: 0s - loss: 0.2777 - acc: 0.8869
17152/18000 [===========================>..] - ETA: 0s - loss: 0.2789 - acc: 0.8865
17280/18000 [===========================>..] - ETA: 0s - loss: 0.2800 - acc: 0.8859
17408/18000 [============================>.] - ETA: 0s - loss: 0.2798 - acc: 0.8859
17536/18000 [============================>.] - ETA: 0s - loss: 0.2800 - acc: 0.8859
17664/18000 [============================>.] - ETA: 0s - loss: 0.2797 - acc: 0.8862
17792/18000 [============================>.] - ETA: 0s - loss: 0.2802 - acc: 0.8860
17920/18000 [============================>.] - ETA: 0s - loss: 0.2801 - acc: 0.8862
18000/18000 [==============================] - 10s 550us/step - loss: 0.2800 - acc: 0.8861 - val_loss: 0.3092 - val_acc: 0.8575
Epoch 6/200

   64/18000 [..............................] - ETA: 10s - loss: 0.1285 - acc: 0.9688
  192/18000 [..............................] - ETA: 10s - loss: 0.1644 - acc: 0.9583
  320/18000 [..............................] - ETA: 10s - loss: 0.2071 - acc: 0.9437
  448/18000 [..............................] - ETA: 9s - loss: 0.2422 - acc: 0.9241 
  576/18000 [..............................] - ETA: 9s - loss: 0.2442 - acc: 0.9115
  704/18000 [>.............................] - ETA: 9s - loss: 0.2455 - acc: 0.9048
  832/18000 [>.............................] - ETA: 9s - loss: 0.2526 - acc: 0.8990
  960/18000 [>.............................] - ETA: 9s - loss: 0.2572 - acc: 0.8969
 1088/18000 [>.............................] - ETA: 9s - loss: 0.2565 - acc: 0.8943
 1216/18000 [=>............................] - ETA: 9s - loss: 0.2516 - acc: 0.8964
 1344/18000 [=>............................] - ETA: 9s - loss: 0.2461 - acc: 0.8996
 1472/18000 [=>............................] - ETA: 9s - loss: 0.2455 - acc: 0.8995
 1600/18000 [=>............................] - ETA: 9s - loss: 0.2424 - acc: 0.9012
 1728/18000 [=>............................] - ETA: 8s - loss: 0.2442 - acc: 0.8981
 1856/18000 [==>...........................] - ETA: 8s - loss: 0.2502 - acc: 0.8960
 1984/18000 [==>...........................] - ETA: 8s - loss: 0.2504 - acc: 0.8967
 2112/18000 [==>...........................] - ETA: 8s - loss: 0.2519 - acc: 0.8977
 2240/18000 [==>...........................] - ETA: 8s - loss: 0.2516 - acc: 0.8991
 2368/18000 [==>...........................] - ETA: 8s - loss: 0.2531 - acc: 0.8982
 2496/18000 [===>..........................] - ETA: 8s - loss: 0.2561 - acc: 0.8962
 2624/18000 [===>..........................] - ETA: 8s - loss: 0.2583 - acc: 0.8952
 2752/18000 [===>..........................] - ETA: 8s - loss: 0.2616 - acc: 0.8932
 2880/18000 [===>..........................] - ETA: 8s - loss: 0.2612 - acc: 0.8931
 3008/18000 [====>.........................] - ETA: 8s - loss: 0.2608 - acc: 0.8936
 3136/18000 [====>.........................] - ETA: 7s - loss: 0.2609 - acc: 0.8932
 3264/18000 [====>.........................] - ETA: 7s - loss: 0.2603 - acc: 0.8934
 3392/18000 [====>.........................] - ETA: 7s - loss: 0.2582 - acc: 0.8942
 3520/18000 [====>.........................] - ETA: 7s - loss: 0.2618 - acc: 0.8923
 3648/18000 [=====>........................] - ETA: 7s - loss: 0.2623 - acc: 0.8914
 3776/18000 [=====>........................] - ETA: 7s - loss: 0.2653 - acc: 0.8901
 3904/18000 [=====>........................] - ETA: 7s - loss: 0.2649 - acc: 0.8899
 4032/18000 [=====>........................] - ETA: 7s - loss: 0.2654 - acc: 0.8899
 4160/18000 [=====>........................] - ETA: 7s - loss: 0.2682 - acc: 0.8885
 4288/18000 [======>.......................] - ETA: 7s - loss: 0.2683 - acc: 0.8883
 4416/18000 [======>.......................] - ETA: 7s - loss: 0.2675 - acc: 0.8888
 4544/18000 [======>.......................] - ETA: 7s - loss: 0.2675 - acc: 0.8886
 4672/18000 [======>.......................] - ETA: 7s - loss: 0.2677 - acc: 0.8887
 4800/18000 [=======>......................] - ETA: 7s - loss: 0.2676 - acc: 0.8896
 4928/18000 [=======>......................] - ETA: 7s - loss: 0.2650 - acc: 0.8910
 5056/18000 [=======>......................] - ETA: 6s - loss: 0.2658 - acc: 0.8906
 5184/18000 [=======>......................] - ETA: 6s - loss: 0.2653 - acc: 0.8904
 5312/18000 [=======>......................] - ETA: 6s - loss: 0.2661 - acc: 0.8899
 5440/18000 [========>.....................] - ETA: 6s - loss: 0.2655 - acc: 0.8901
 5568/18000 [========>.....................] - ETA: 6s - loss: 0.2646 - acc: 0.8908
 5696/18000 [========>.....................] - ETA: 6s - loss: 0.2648 - acc: 0.8904
 5824/18000 [========>.....................] - ETA: 6s - loss: 0.2659 - acc: 0.8899
 5952/18000 [========>.....................] - ETA: 6s - loss: 0.2666 - acc: 0.8893
 6080/18000 [=========>....................] - ETA: 6s - loss: 0.2670 - acc: 0.8885
 6208/18000 [=========>....................] - ETA: 6s - loss: 0.2656 - acc: 0.8895
 6336/18000 [=========>....................] - ETA: 6s - loss: 0.2662 - acc: 0.8890
 6464/18000 [=========>....................] - ETA: 6s - loss: 0.2663 - acc: 0.8889
 6592/18000 [=========>....................] - ETA: 6s - loss: 0.2666 - acc: 0.8888
 6720/18000 [==========>...................] - ETA: 6s - loss: 0.2665 - acc: 0.8888
 6848/18000 [==========>...................] - ETA: 5s - loss: 0.2661 - acc: 0.8895
 6976/18000 [==========>...................] - ETA: 5s - loss: 0.2663 - acc: 0.8893
 7104/18000 [==========>...................] - ETA: 5s - loss: 0.2659 - acc: 0.8902
 7232/18000 [===========>..................] - ETA: 5s - loss: 0.2657 - acc: 0.8902
 7360/18000 [===========>..................] - ETA: 5s - loss: 0.2652 - acc: 0.8901
 7488/18000 [===========>..................] - ETA: 5s - loss: 0.2646 - acc: 0.8904
 7616/18000 [===========>..................] - ETA: 5s - loss: 0.2645 - acc: 0.8901
 7744/18000 [===========>..................] - ETA: 5s - loss: 0.2650 - acc: 0.8900
 7872/18000 [============>.................] - ETA: 5s - loss: 0.2648 - acc: 0.8902
 8000/18000 [============>.................] - ETA: 5s - loss: 0.2658 - acc: 0.8898
 8128/18000 [============>.................] - ETA: 5s - loss: 0.2655 - acc: 0.8901
 8256/18000 [============>.................] - ETA: 5s - loss: 0.2642 - acc: 0.8906
 8384/18000 [============>.................] - ETA: 5s - loss: 0.2641 - acc: 0.8907
 8512/18000 [=============>................] - ETA: 5s - loss: 0.2629 - acc: 0.8913
 8640/18000 [=============>................] - ETA: 5s - loss: 0.2626 - acc: 0.8913
 8768/18000 [=============>................] - ETA: 4s - loss: 0.2628 - acc: 0.8911
 8896/18000 [=============>................] - ETA: 4s - loss: 0.2618 - acc: 0.8914
 9024/18000 [==============>...............] - ETA: 4s - loss: 0.2622 - acc: 0.8912
 9152/18000 [==============>...............] - ETA: 4s - loss: 0.2624 - acc: 0.8915
 9280/18000 [==============>...............] - ETA: 4s - loss: 0.2619 - acc: 0.8920
 9408/18000 [==============>...............] - ETA: 4s - loss: 0.2616 - acc: 0.8926
 9536/18000 [==============>...............] - ETA: 4s - loss: 0.2611 - acc: 0.8927
 9664/18000 [===============>..............] - ETA: 4s - loss: 0.2609 - acc: 0.8930
 9792/18000 [===============>..............] - ETA: 4s - loss: 0.2614 - acc: 0.8924
 9920/18000 [===============>..............] - ETA: 4s - loss: 0.2620 - acc: 0.8920
10048/18000 [===============>..............] - ETA: 4s - loss: 0.2630 - acc: 0.8914
10176/18000 [===============>..............] - ETA: 4s - loss: 0.2631 - acc: 0.8915
10304/18000 [================>.............] - ETA: 4s - loss: 0.2620 - acc: 0.8922
10432/18000 [================>.............] - ETA: 4s - loss: 0.2623 - acc: 0.8918
10560/18000 [================>.............] - ETA: 3s - loss: 0.2627 - acc: 0.8913
10688/18000 [================>.............] - ETA: 3s - loss: 0.2630 - acc: 0.8914
10816/18000 [=================>............] - ETA: 3s - loss: 0.2626 - acc: 0.8914
10880/18000 [=================>............] - ETA: 3s - loss: 0.2630 - acc: 0.8914
11008/18000 [=================>............] - ETA: 3s - loss: 0.2633 - acc: 0.8910
11136/18000 [=================>............] - ETA: 3s - loss: 0.2636 - acc: 0.8911
11264/18000 [=================>............] - ETA: 3s - loss: 0.2627 - acc: 0.8911
11392/18000 [=================>............] - ETA: 3s - loss: 0.2635 - acc: 0.8908
11520/18000 [==================>...........] - ETA: 3s - loss: 0.2639 - acc: 0.8907
11648/18000 [==================>...........] - ETA: 3s - loss: 0.2637 - acc: 0.8909
11776/18000 [==================>...........] - ETA: 3s - loss: 0.2633 - acc: 0.8912
11904/18000 [==================>...........] - ETA: 3s - loss: 0.2635 - acc: 0.8910
12032/18000 [===================>..........] - ETA: 3s - loss: 0.2639 - acc: 0.8908
12160/18000 [===================>..........] - ETA: 3s - loss: 0.2633 - acc: 0.8911
12288/18000 [===================>..........] - ETA: 3s - loss: 0.2631 - acc: 0.8913
12416/18000 [===================>..........] - ETA: 3s - loss: 0.2645 - acc: 0.8909
12544/18000 [===================>..........] - ETA: 2s - loss: 0.2644 - acc: 0.8909
12672/18000 [====================>.........] - ETA: 2s - loss: 0.2643 - acc: 0.8909
12800/18000 [====================>.........] - ETA: 2s - loss: 0.2651 - acc: 0.8907
12928/18000 [====================>.........] - ETA: 2s - loss: 0.2657 - acc: 0.8902
13056/18000 [====================>.........] - ETA: 2s - loss: 0.2661 - acc: 0.8900
13184/18000 [====================>.........] - ETA: 2s - loss: 0.2669 - acc: 0.8898
13312/18000 [=====================>........] - ETA: 2s - loss: 0.2672 - acc: 0.8897
13440/18000 [=====================>........] - ETA: 2s - loss: 0.2675 - acc: 0.8893
13568/18000 [=====================>........] - ETA: 2s - loss: 0.2681 - acc: 0.8890
13696/18000 [=====================>........] - ETA: 2s - loss: 0.2680 - acc: 0.8889
13824/18000 [======================>.......] - ETA: 2s - loss: 0.2678 - acc: 0.8891
13952/18000 [======================>.......] - ETA: 2s - loss: 0.2687 - acc: 0.8889
14080/18000 [======================>.......] - ETA: 2s - loss: 0.2690 - acc: 0.8888
14208/18000 [======================>.......] - ETA: 2s - loss: 0.2689 - acc: 0.8889
14336/18000 [======================>.......] - ETA: 1s - loss: 0.2691 - acc: 0.8889
14464/18000 [=======================>......] - ETA: 1s - loss: 0.2696 - acc: 0.8887
14592/18000 [=======================>......] - ETA: 1s - loss: 0.2695 - acc: 0.8886
14720/18000 [=======================>......] - ETA: 1s - loss: 0.2694 - acc: 0.8886
14848/18000 [=======================>......] - ETA: 1s - loss: 0.2690 - acc: 0.8885
14976/18000 [=======================>......] - ETA: 1s - loss: 0.2689 - acc: 0.8886
15104/18000 [========================>.....] - ETA: 1s - loss: 0.2689 - acc: 0.8888
15232/18000 [========================>.....] - ETA: 1s - loss: 0.2685 - acc: 0.8888
15360/18000 [========================>.....] - ETA: 1s - loss: 0.2686 - acc: 0.8885
15488/18000 [========================>.....] - ETA: 1s - loss: 0.2696 - acc: 0.8882
15616/18000 [=========================>....] - ETA: 1s - loss: 0.2702 - acc: 0.8881
15744/18000 [=========================>....] - ETA: 1s - loss: 0.2700 - acc: 0.8883
15872/18000 [=========================>....] - ETA: 1s - loss: 0.2697 - acc: 0.8884
16000/18000 [=========================>....] - ETA: 1s - loss: 0.2703 - acc: 0.8881
16128/18000 [=========================>....] - ETA: 1s - loss: 0.2704 - acc: 0.8882
16256/18000 [==========================>...] - ETA: 0s - loss: 0.2702 - acc: 0.8883
16384/18000 [==========================>...] - ETA: 0s - loss: 0.2697 - acc: 0.8885
16512/18000 [==========================>...] - ETA: 0s - loss: 0.2697 - acc: 0.8886
16640/18000 [==========================>...] - ETA: 0s - loss: 0.2695 - acc: 0.8888
16768/18000 [==========================>...] - ETA: 0s - loss: 0.2696 - acc: 0.8885
16896/18000 [===========================>..] - ETA: 0s - loss: 0.2694 - acc: 0.8887
17024/18000 [===========================>..] - ETA: 0s - loss: 0.2697 - acc: 0.8885
17152/18000 [===========================>..] - ETA: 0s - loss: 0.2702 - acc: 0.8884
17280/18000 [===========================>..] - ETA: 0s - loss: 0.2710 - acc: 0.8880
17408/18000 [============================>.] - ETA: 0s - loss: 0.2710 - acc: 0.8879
17536/18000 [============================>.] - ETA: 0s - loss: 0.2710 - acc: 0.8880
17664/18000 [============================>.] - ETA: 0s - loss: 0.2707 - acc: 0.8882
17792/18000 [============================>.] - ETA: 0s - loss: 0.2719 - acc: 0.8877
17920/18000 [============================>.] - ETA: 0s - loss: 0.2719 - acc: 0.8878
18000/18000 [==============================] - 10s 554us/step - loss: 0.2721 - acc: 0.8876 - val_loss: 0.2929 - val_acc: 0.8660
Epoch 7/200

   64/18000 [..............................] - ETA: 9s - loss: 0.2257 - acc: 0.9062
  192/18000 [..............................] - ETA: 9s - loss: 0.2629 - acc: 0.8854
  320/18000 [..............................] - ETA: 9s - loss: 0.2880 - acc: 0.8719
  448/18000 [..............................] - ETA: 9s - loss: 0.2753 - acc: 0.8795
  576/18000 [..............................] - ETA: 8s - loss: 0.2708 - acc: 0.8802
  704/18000 [>.............................] - ETA: 8s - loss: 0.2619 - acc: 0.8793
  832/18000 [>.............................] - ETA: 8s - loss: 0.2648 - acc: 0.8798
  960/18000 [>.............................] - ETA: 8s - loss: 0.2709 - acc: 0.8792
 1088/18000 [>.............................] - ETA: 8s - loss: 0.2660 - acc: 0.8796
 1216/18000 [=>............................] - ETA: 8s - loss: 0.2638 - acc: 0.8783
 1344/18000 [=>............................] - ETA: 8s - loss: 0.2620 - acc: 0.8839
 1472/18000 [=>............................] - ETA: 8s - loss: 0.2583 - acc: 0.8865
 1600/18000 [=>............................] - ETA: 8s - loss: 0.2682 - acc: 0.8812
 1728/18000 [=>............................] - ETA: 8s - loss: 0.2629 - acc: 0.8848
 1856/18000 [==>...........................] - ETA: 8s - loss: 0.2592 - acc: 0.8885
 1984/18000 [==>...........................] - ETA: 8s - loss: 0.2557 - acc: 0.8911
 2112/18000 [==>...........................] - ETA: 8s - loss: 0.2551 - acc: 0.8911
 2240/18000 [==>...........................] - ETA: 8s - loss: 0.2520 - acc: 0.8915
 2368/18000 [==>...........................] - ETA: 8s - loss: 0.2544 - acc: 0.8902
 2496/18000 [===>..........................] - ETA: 8s - loss: 0.2594 - acc: 0.8886
 2624/18000 [===>..........................] - ETA: 8s - loss: 0.2631 - acc: 0.8861
 2752/18000 [===>..........................] - ETA: 8s - loss: 0.2662 - acc: 0.8855
 2880/18000 [===>..........................] - ETA: 8s - loss: 0.2670 - acc: 0.8847
 3008/18000 [====>.........................] - ETA: 8s - loss: 0.2650 - acc: 0.8860
 3136/18000 [====>.........................] - ETA: 8s - loss: 0.2641 - acc: 0.8868
 3264/18000 [====>.........................] - ETA: 8s - loss: 0.2636 - acc: 0.8879
 3392/18000 [====>.........................] - ETA: 8s - loss: 0.2666 - acc: 0.8874
 3520/18000 [====>.........................] - ETA: 7s - loss: 0.2674 - acc: 0.8872
 3648/18000 [=====>........................] - ETA: 7s - loss: 0.2668 - acc: 0.8876
 3776/18000 [=====>........................] - ETA: 7s - loss: 0.2671 - acc: 0.8882
 3904/18000 [=====>........................] - ETA: 7s - loss: 0.2665 - acc: 0.8896
 4032/18000 [=====>........................] - ETA: 7s - loss: 0.2653 - acc: 0.8914
 4160/18000 [=====>........................] - ETA: 7s - loss: 0.2643 - acc: 0.8918
 4288/18000 [======>.......................] - ETA: 7s - loss: 0.2655 - acc: 0.8902
 4416/18000 [======>.......................] - ETA: 7s - loss: 0.2653 - acc: 0.8895
 4544/18000 [======>.......................] - ETA: 7s - loss: 0.2662 - acc: 0.8889
 4672/18000 [======>.......................] - ETA: 7s - loss: 0.2660 - acc: 0.8893
 4800/18000 [=======>......................] - ETA: 7s - loss: 0.2666 - acc: 0.8888
 4928/18000 [=======>......................] - ETA: 7s - loss: 0.2671 - acc: 0.8888
 5056/18000 [=======>......................] - ETA: 7s - loss: 0.2659 - acc: 0.8898
 5184/18000 [=======>......................] - ETA: 7s - loss: 0.2659 - acc: 0.8900
 5312/18000 [=======>......................] - ETA: 6s - loss: 0.2655 - acc: 0.8906
 5440/18000 [========>.....................] - ETA: 6s - loss: 0.2660 - acc: 0.8899
 5568/18000 [========>.....................] - ETA: 6s - loss: 0.2659 - acc: 0.8901
 5696/18000 [========>.....................] - ETA: 6s - loss: 0.2673 - acc: 0.8896
 5824/18000 [========>.....................] - ETA: 6s - loss: 0.2674 - acc: 0.8898
 5952/18000 [========>.....................] - ETA: 6s - loss: 0.2675 - acc: 0.8889
 6080/18000 [=========>....................] - ETA: 6s - loss: 0.2687 - acc: 0.8878
 6208/18000 [=========>....................] - ETA: 6s - loss: 0.2692 - acc: 0.8874
 6336/18000 [=========>....................] - ETA: 6s - loss: 0.2706 - acc: 0.8867
 6464/18000 [=========>....................] - ETA: 6s - loss: 0.2709 - acc: 0.8860
 6592/18000 [=========>....................] - ETA: 6s - loss: 0.2708 - acc: 0.8864
 6720/18000 [==========>...................] - ETA: 6s - loss: 0.2727 - acc: 0.8856
 6848/18000 [==========>...................] - ETA: 6s - loss: 0.2719 - acc: 0.8862
 6976/18000 [==========>...................] - ETA: 5s - loss: 0.2722 - acc: 0.8859
 7104/18000 [==========>...................] - ETA: 5s - loss: 0.2721 - acc: 0.8858
 7232/18000 [===========>..................] - ETA: 5s - loss: 0.2722 - acc: 0.8861
 7360/18000 [===========>..................] - ETA: 5s - loss: 0.2715 - acc: 0.8865
 7488/18000 [===========>..................] - ETA: 5s - loss: 0.2712 - acc: 0.8868
 7616/18000 [===========>..................] - ETA: 5s - loss: 0.2711 - acc: 0.8864
 7744/18000 [===========>..................] - ETA: 5s - loss: 0.2719 - acc: 0.8856
 7872/18000 [============>.................] - ETA: 5s - loss: 0.2719 - acc: 0.8859
 8000/18000 [============>.................] - ETA: 5s - loss: 0.2724 - acc: 0.8858
 8128/18000 [============>.................] - ETA: 5s - loss: 0.2727 - acc: 0.8856
 8256/18000 [============>.................] - ETA: 5s - loss: 0.2744 - acc: 0.8848
 8384/18000 [============>.................] - ETA: 5s - loss: 0.2745 - acc: 0.8850
 8512/18000 [=============>................] - ETA: 5s - loss: 0.2758 - acc: 0.8843
 8640/18000 [=============>................] - ETA: 5s - loss: 0.2774 - acc: 0.8833
 8768/18000 [=============>................] - ETA: 5s - loss: 0.2765 - acc: 0.8841
 8896/18000 [=============>................] - ETA: 4s - loss: 0.2766 - acc: 0.8839
 9024/18000 [==============>...............] - ETA: 4s - loss: 0.2758 - acc: 0.8843
 9152/18000 [==============>...............] - ETA: 4s - loss: 0.2757 - acc: 0.8843
 9280/18000 [==============>...............] - ETA: 4s - loss: 0.2758 - acc: 0.8844
 9408/18000 [==============>...............] - ETA: 4s - loss: 0.2749 - acc: 0.8844
 9536/18000 [==============>...............] - ETA: 4s - loss: 0.2749 - acc: 0.8844
 9664/18000 [===============>..............] - ETA: 4s - loss: 0.2746 - acc: 0.8845
 9792/18000 [===============>..............] - ETA: 4s - loss: 0.2742 - acc: 0.8847
 9920/18000 [===============>..............] - ETA: 4s - loss: 0.2750 - acc: 0.8849
10048/18000 [===============>..............] - ETA: 4s - loss: 0.2740 - acc: 0.8856
10176/18000 [===============>..............] - ETA: 4s - loss: 0.2732 - acc: 0.8860
10304/18000 [================>.............] - ETA: 4s - loss: 0.2739 - acc: 0.8854
10432/18000 [================>.............] - ETA: 4s - loss: 0.2745 - acc: 0.8851
10496/18000 [================>.............] - ETA: 4s - loss: 0.2744 - acc: 0.8851
10624/18000 [================>.............] - ETA: 4s - loss: 0.2746 - acc: 0.8853
10752/18000 [================>.............] - ETA: 3s - loss: 0.2757 - acc: 0.8845
10880/18000 [=================>............] - ETA: 3s - loss: 0.2758 - acc: 0.8845
11008/18000 [=================>............] - ETA: 3s - loss: 0.2753 - acc: 0.8845
11136/18000 [=================>............] - ETA: 3s - loss: 0.2753 - acc: 0.8841
11264/18000 [=================>............] - ETA: 3s - loss: 0.2754 - acc: 0.8840
11392/18000 [=================>............] - ETA: 3s - loss: 0.2764 - acc: 0.8835
11520/18000 [==================>...........] - ETA: 3s - loss: 0.2763 - acc: 0.8835
11648/18000 [==================>...........] - ETA: 3s - loss: 0.2765 - acc: 0.8836
11776/18000 [==================>...........] - ETA: 3s - loss: 0.2757 - acc: 0.8839
11904/18000 [==================>...........] - ETA: 3s - loss: 0.2749 - acc: 0.8843
12032/18000 [===================>..........] - ETA: 3s - loss: 0.2764 - acc: 0.8837
12160/18000 [===================>..........] - ETA: 3s - loss: 0.2757 - acc: 0.8841
12288/18000 [===================>..........] - ETA: 3s - loss: 0.2752 - acc: 0.8842
12416/18000 [===================>..........] - ETA: 3s - loss: 0.2743 - acc: 0.8847
12544/18000 [===================>..........] - ETA: 2s - loss: 0.2740 - acc: 0.8846
12672/18000 [====================>.........] - ETA: 2s - loss: 0.2747 - acc: 0.8842
12800/18000 [====================>.........] - ETA: 2s - loss: 0.2751 - acc: 0.8841
12928/18000 [====================>.........] - ETA: 2s - loss: 0.2748 - acc: 0.8842
13056/18000 [====================>.........] - ETA: 2s - loss: 0.2744 - acc: 0.8845
13184/18000 [====================>.........] - ETA: 2s - loss: 0.2743 - acc: 0.8849
13312/18000 [=====================>........] - ETA: 2s - loss: 0.2738 - acc: 0.8851
13440/18000 [=====================>........] - ETA: 2s - loss: 0.2742 - acc: 0.8848
13568/18000 [=====================>........] - ETA: 2s - loss: 0.2743 - acc: 0.8846
13696/18000 [=====================>........] - ETA: 2s - loss: 0.2741 - acc: 0.8847
13824/18000 [======================>.......] - ETA: 2s - loss: 0.2746 - acc: 0.8845
13952/18000 [======================>.......] - ETA: 2s - loss: 0.2753 - acc: 0.8842
14080/18000 [======================>.......] - ETA: 2s - loss: 0.2757 - acc: 0.8839
14208/18000 [======================>.......] - ETA: 2s - loss: 0.2756 - acc: 0.8839
14336/18000 [======================>.......] - ETA: 2s - loss: 0.2752 - acc: 0.8842
14464/18000 [=======================>......] - ETA: 1s - loss: 0.2753 - acc: 0.8843
14592/18000 [=======================>......] - ETA: 1s - loss: 0.2751 - acc: 0.8845
14720/18000 [=======================>......] - ETA: 1s - loss: 0.2744 - acc: 0.8849
14848/18000 [=======================>......] - ETA: 1s - loss: 0.2745 - acc: 0.8849
14976/18000 [=======================>......] - ETA: 1s - loss: 0.2739 - acc: 0.8853
15104/18000 [========================>.....] - ETA: 1s - loss: 0.2742 - acc: 0.8851
15232/18000 [========================>.....] - ETA: 1s - loss: 0.2743 - acc: 0.8853
15360/18000 [========================>.....] - ETA: 1s - loss: 0.2739 - acc: 0.8855
15488/18000 [========================>.....] - ETA: 1s - loss: 0.2736 - acc: 0.8856
15616/18000 [=========================>....] - ETA: 1s - loss: 0.2730 - acc: 0.8858
15744/18000 [=========================>....] - ETA: 1s - loss: 0.2732 - acc: 0.8859
15872/18000 [=========================>....] - ETA: 1s - loss: 0.2723 - acc: 0.8862
16000/18000 [=========================>....] - ETA: 1s - loss: 0.2719 - acc: 0.8862
16128/18000 [=========================>....] - ETA: 1s - loss: 0.2717 - acc: 0.8862
16256/18000 [==========================>...] - ETA: 0s - loss: 0.2723 - acc: 0.8860
16384/18000 [==========================>...] - ETA: 0s - loss: 0.2716 - acc: 0.8863
16512/18000 [==========================>...] - ETA: 0s - loss: 0.2716 - acc: 0.8861
16640/18000 [==========================>...] - ETA: 0s - loss: 0.2722 - acc: 0.8856
16768/18000 [==========================>...] - ETA: 0s - loss: 0.2726 - acc: 0.8854
16896/18000 [===========================>..] - ETA: 0s - loss: 0.2724 - acc: 0.8855
17024/18000 [===========================>..] - ETA: 0s - loss: 0.2725 - acc: 0.8853
17152/18000 [===========================>..] - ETA: 0s - loss: 0.2724 - acc: 0.8854
17280/18000 [===========================>..] - ETA: 0s - loss: 0.2723 - acc: 0.8855
17408/18000 [============================>.] - ETA: 0s - loss: 0.2718 - acc: 0.8857
17536/18000 [============================>.] - ETA: 0s - loss: 0.2727 - acc: 0.8856
17664/18000 [============================>.] - ETA: 0s - loss: 0.2729 - acc: 0.8858
17792/18000 [============================>.] - ETA: 0s - loss: 0.2726 - acc: 0.8860
17920/18000 [============================>.] - ETA: 0s - loss: 0.2726 - acc: 0.8859
18000/18000 [==============================] - 10s 559us/step - loss: 0.2726 - acc: 0.8859 - val_loss: 0.2632 - val_acc: 0.8840

real	1m24.144s
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ...  
လက်ရှိ para နဲ့ not-para ဒေတာစုစုပေါင်း နှစ်သောင်းရဲ့ 80% တစ်သောင်းရှစ်ထောင်ကိုသုံး training လုပ်ပြီး၊   
20% ဖြစ်တဲ့ နှစ်ထောင် ကိုသုံး validation လုပ်သွားတာမှာ validation loss: 0.2632 နဲ့ validation accuracy: 0.8840 ရပါတယ်။   
မဆိုးပါဘူး။ ဒီထက် ရလဒ်ကောင်းအောင် ကတော့ ဒေတာတိုးတာ network architecture ပြောင်းတာ၊ parameter tuning စတာတွေကိုလုပ်သွားရပါလိမ့်မယ်။    

## Editing testing python file

တကယ်လို့ ဆောက်ထားပြီးသားမော်ဒယ်ကို test-data နဲ့ similarity တိုင်းတာတာမျိုး လုပ်ချင်ရင်တော့ example testing ပရိုဂရမ်ကို ကော်ပီကူးပြီး လုပ်သွားပါ။ ဥပမာ အနေနဲ့ test-para1.py ဆိုပြီးကော်ပီကူးထားရင် အဲဒီဖိုင်ကို gedit နဲ့ဖွင့်ပြီး ဝင်ပြင်တာလုပ်ရပါလိမ့်မယ်။   

```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ gedit test-para1.py
```

အနည်းဆုံးတော့ မော်ဒယ် ရှိတဲ့ path နဲ့ model ဖိုင်နာမည်ကို ရိုက်ထည့်ပေးရမယ်။ ပုံမှန်အားဖြင့် မော်ဒယ်က checkpoints ဆိုတဲ့ အောက်မှာ သိမ်းလိမ့်မယ်။ နံပါတ်အကြီးဆုံးဟာက နောက်ဆုံး မော်ဒယ်၊ အကောင်းဆုံးမော်ဒယ်ပါ။ configuration setting ပေါ်မူတည်ပြီး epoch တိုင်းရဲ့ မော်ဒယ်ကို သိမ်းပေးခိုင်းထားခဲ့ရင် အဲဒီဖိုလ်ဒါအောက်မှာ မော်ဒယ်တွေက တစ်ခုထက်မက ရှိနေပါလိမ့်မယ်။  

ဆရာက အောက်ပါအတိုင်း ပြင်ဆင်တာတွေလုပ်ခဲ့တယ်။ မော်ဒယ်ဖိုင်ရဲ့ extension ကတော့ .h5 ပါ။ .h5 ဆိုတာက Hierarchical Data Format (HDF) ရဲ့ file extension ပါ။  

```python
#model = load_model("/media/ye/project1/tool/lstm-siamese-text-similarity/checkpoints/1605650354/lstm_50_50_0.17_0.25.h5")
model = load_model("/media/ye/project1/tool/lstm-siamese-text-similarity/checkpoints/1608068575/lstm_50_50_0.17_0.25.h5")
```

လက်ရှိ testing လုပ်တဲ့ python ဖိုင် မှာက စာကြောင်းအချို့ကို ရိုက်ထည့်ထားပြီး စမ်းထားတာမို့ အဲဒါကို အရင် အစားထိုးကြည့်ပြီး testing လုပ်ခဲ့တယ်။ ဗမာစာကြောင်းတွေက test ဖိုင်ကနေ ယူထားတယ်။  

```python
#test_sentence_pairs = [('What can make Physics easy to learn?','How can you make physics easy to learn?'),('How many times a day do a clocks hands overlap?','What does it mean that every time I look at the clock the numbers are the same?')]
test_sentence_pairs = [('ဦးခိုက်ရှိခိုး ပါ ၏','ဦးခိုက် ပါ တယ်'),('ဆရာတော် ကြီး များ သက်တော် ရာ ကျော် ရှည် ပါ စေ','ဆရာတော် ကြီး များ ကျန်းမာ သက် ရှည် ပါ စေ'),('ကြိုက် သွား ပြီ','ကြိုဆို လိုက် ပါ'),('စောက် လုပ် ကို ရှုပ် တယ်','စောက် လုပ် တွေ က ရှုပ် နေ တာ ပဲ'),('သူ နဲ့ ကင်းကွာ နေ တာ ကြာ ပြီ','သူ နဲ့ အနီးဆုံး မှာ ပဲ နေ ပါ တယ်'),('ထမင်း ကို ဖိတ်စင် အောင် မ စား ပါ နဲ့ ။','ရေ ကို ဖိတ်စင် အောင် မ ခပ် ပါ နဲ့ ။'),('မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း များ သည် ဗွက် ဖြစ် နေ သည် ။','မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း မှာ ကောင်းကောင်း သွား မ ရ ပါ ။'),('ရွဲ့လားစောင်းလား မ လုပ် နဲ့ နော်','စောင်း ပြော နေ တာ လား'),('ဝမ်းမြောက် ဝမ်းသာ ဖြစ် မိ ပါ သည်','ဝမ်းမြောက် ဝမ်းသာ ရှိ လှ ပေ စွ'),('တော် တယ် ဆက် ပြီး တော့ ကြိုးစား ပါ','တော် တယ် ဆက် ကြိုးစား ပါ')]
```

## Testing-1

test-para1.py နဲ့ testing လုပ်ခဲ့တော့ အောက်ပါအတိုင်း output/result တွေကို ရရှိခဲ့...  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ time python ./test-para1.py 2>&1 | tee test-para1.log1
Using TensorFlow backend.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:517: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:74: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:4138: The name tf.random_uniform is deprecated. Please use tf.random.uniform instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:133: The name tf.placeholder_with_default is deprecated. Please use tf.compat.v1.placeholder_with_default instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3445: calling dropout (from tensorflow.python.ops.nn_ops) with keep_prob is deprecated and will be removed in a future version.
Instructions for updating:
Please use `rate` instead of `keep_prob`. Rate should be set to `rate = 1 - keep_prob`.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:174: The name tf.get_default_session is deprecated. Please use tf.compat.v1.get_default_session instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:181: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:186: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2020-12-16 04:43:19.535172: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2893330000 Hz
2020-12-16 04:43:19.535738: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x5636da116c70 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-12-16 04:43:19.535779: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:190: The name tf.global_variables is deprecated. Please use tf.compat.v1.global_variables instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:199: The name tf.is_variable_initialized is deprecated. Please use tf.compat.v1.is_variable_initialized instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:206: The name tf.variables_initializer is deprecated. Please use tf.compat.v1.variables_initializer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/optimizers.py:790: The name tf.train.Optimizer is deprecated. Please use tf.compat.v1.train.Optimizer instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:3376: The name tf.log is deprecated. Please use tf.math.log instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/tensorflow_core/python/ops/nn_impl.py:183: where (from tensorflow.python.ops.array_ops) is deprecated and will be removed in a future version.
Instructions for updating:
Use tf.where in 2.0, which has the same broadcast rule as np.where
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:986: The name tf.assign_add is deprecated. Please use tf.compat.v1.assign_add instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:973: The name tf.assign is deprecated. Please use tf.compat.v1.assign instead.


10/10 [==============================] - 1s 65ms/step
[('ဦးခိုက်ရှိခိုး ပါ ၏', 'ဦးခိုက် ပါ တယ်', 0.9751325), ('ဆရာတော် ကြီး များ သက်တော် ရာ ကျော် ရှည် ပါ စေ', 'ဆရာတော် ကြီး များ ကျန်းမာ သက် ရှည် ပါ စေ', 0.9751325), ('ကြိုက် သွား ပြီ', 'ကြိုဆို လိုက် ပါ', 0.9751325), ('စောက် လုပ် ကို ရှုပ် တယ်', 'စောက် လုပ် တွေ က ရှုပ် နေ တာ ပဲ', 0.9751325), ('သူ နဲ့ ကင်းကွာ နေ တာ ကြာ ပြီ', 'သူ နဲ့ အနီးဆုံး မှာ ပဲ နေ ပါ တယ်', 0.9751325), ('ထမင်း ကို ဖိတ်စင် အောင် မ စား ပါ နဲ့ ။', 'ရေ ကို ဖိတ်စင် အောင် မ ခပ် ပါ နဲ့ ။', 0.9751325), ('မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း များ သည် ဗွက် ဖြစ် နေ သည် ။', 'မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း မှာ ကောင်းကောင်း သွား မ ရ ပါ ။', 0.9751325), ('ရွဲ့လားစောင်းလား မ လုပ် နဲ့ နော်', 'စောင်း ပြော နေ တာ လား', 0.9751325), ('ဝမ်းမြောက် ဝမ်းသာ ဖြစ် မိ ပါ သည်', 'ဝမ်းမြောက် ဝမ်းသာ ရှိ လှ ပေ စွ', 0.9751325), ('တော် တယ် ဆက် ပြီး တော့ ကြိုးစား ပါ', 'တော် တယ် ဆက် ကြိုးစား ပါ', 0.9751325)]

real	0m8.444s
user	0m8.614s
sys	0m0.843s
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

## How about increasing no. of epoch for training?!

model.py ဖိုင်မှာ အောက်ပါ statement ကို တွေ့ခဲ့။ နှစ်နေရာရှိတယ် ...  

```python
        model.fit([train_data_x1, train_data_x2, leaks_train], train_labels,
                  validation_data=([val_data_x1, val_data_x2, leaks_val], val_labels),
                  epochs=50, batch_size=3, shuffle=True,
                  callbacks=[early_stopping, model_checkpoint, tensorboard])
```

code ကတော့ အသေတွေဖြစ်နေလို့ coding ဖိုင်ထဲကို ဝင်ပြင်မှရတဲ့ ပုံစံတော့ ဖြစ်နေတယ်။ ပြင်ချင်ရင် အဲဒီမှာ epochs=100 ထားကြည့်တာမျိုး လုပ်လို့ရတယ်။  

epoch=100 နဲ့ run ကြည့်ခဲ့သေးတယ်။  ဘာသွားတွေ့ရသလဲ ဆိုတော့ epoch က 100 ထိသွားစရာမလိုပဲ early stop နဲ့ learning လုပ်တာက ရပ်သွားတာကို တွေ့ရ။ ဆိုလိုတာက မော်ဒယ်က ဒီရလဒ်က အကောင်းဆုံးပါပဲ။  

ဆရာ training/validation ဒေတာပမာဏ ကိုလည်းအတိုးအလျော့လုပ်ပြီး စမ်းခဲ့ပါသေးတယ်။  
ဥပမာ စုစုပေါင်း ဒေတာ ရှစ်ထောင်နဲ့ပဲ စမ်းတဲ့အခါမှာ အောက်ပါအတိုင်းရပါတယ်။  

1st time training တုန်းက  
```
7200/7200 [==============================] - 4s 515us/step - loss: 0.3297 - acc: 0.8583 - val_loss: 0.2858 - val_acc: 0.8761
```

အခု 2nd time training မှာက  
```
7200/7200 [==============================] - 4s 560us/step - loss: 0.2900 - acc: 0.8775 - val_loss: 0.2673 - val_acc: 0.8911
```
ဆိုတော ... နည်းနည်းတက်လာတာတော့ တွေ့ရ  

## Some More Error Notes

တကယ်လို့ training/validation လုပ်တဲ့ဒေတာမှာ blank field တွေ ရှိနေရင် အောက်ပါအတိုင်း error ပေးပါလိမ့်မယ်။  

```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ time python ./train-para1.py 2>&1 | tee ./para-tst-1/para1.train.log3
Using TensorFlow backend.
Traceback (most recent call last):
  File "./train-para1.py", line 18, in <module>
    tokenizer, embedding_matrix = word_embed_meta_data(sentences1 + sentences2,  siamese_config['EMBEDDING_DIM'])
  File "/media/ye/project1/tool/lstm-siamese-text-similarity/inputHandler.py", line 59, in word_embed_meta_data
    documents = [x.lower().split() for x in documents]
  File "/media/ye/project1/tool/lstm-siamese-text-similarity/inputHandler.py", line 59, in <listcomp>
    documents = [x.lower().split() for x in documents]
AttributeError: 'float' object has no attribute 'lower'

real	0m2.136s
user	0m2.247s
sys	0m0.428s
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$
```

training/validation လုပ်မယ့် CSV ဖိုင်တွေရဲ့ အကြောင်းတိုင်းမှာ ကော်မာအရေအတွက်က အတူတူရှိရပါမယ်။ မရှိရင် မော်ဒယ်ဆောက်တဲ့အခါမှာ အထက်ပါကဲ့သို့သော် error တွေကို ရနိုင်ပါတယ်။  

## Checking fields

ကိုယ့်ဒေတာဖိုင်ထဲမှာ blank field ရှိမရှိ စစ်တာနဲ့ ပတ်သက်တဲ့ shell command တချို့ကိုပါ လေ့လာနိုင်အောင် note ရေးပေးထားလိုက်မယ်။  

```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ grep '^,\|,,\|,$' ./line-no.para-no-para.shuf.final
,sentences1,sentences2,is_similar
20000,
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ tail ./line-no.para-no-para.shuf.final
19991,ထောင်ချ ပစ် ရ မှာ,ထောင် ထဲ မှာ ပစ် ထား တယ်,0
19992,ကလေး တွေ ခုန်ပေါက်ပြေးလွှား ပြီး ကစား နေ ကြ တယ် ။,ကလေး တွေ ပျော်ရွှင် စွာ ရေကူး နေ ကြ တယ် ။,0
19993,တို့ ဆီ ကို မင်း ဘယ်တော့ လာ လည် မှာ လဲ ။,မင်း တို့ ဆီ ကို ဘယ်တော့ ပြန်လာ မှာ လဲ ။,0
19994,တံခါး သွက်သွက် ဖွင့် စမ်း ။,တံခါး မြန်မြန် ပိတ် လိုက် ပါ ။,0
19995,ပြတင်းပေါက် ကို ဖွင့် မ ရ ဘူး ဖြစ် နေ ပါ တယ် ။,ပြတင်းပေါက် ကို ဖွင့် ထား လိုက် ပါ ။,0
19996,ကူညီ ပေး ပါ ရ စေ,ကူညီ ချင် လိုက် တာ,1
19997,ဂွ တော့ အတော် ကျ ကုန် ပြီ,ဂွ ကျ သွား လို့ ကောက် ပေး ပါ,0
19998,ရှိခိုး ဦးချ ပါ တယ်,အမေ့ ကို ရှိခိုး မယ်,0
19999,အကြောင်း အရာ လေး စုံစမ်း ကြည့် ဦး ။,သတင်း လေး စုံစမ်း ကြည့် ဦး ။,1
20000,
```

အထက်က အမှားက လိုင်းနံပါတ်က Zero က စထားတာကို ဆရာက ဂရုမပြုမိလို့ ဖြစ်ခဲ့တဲ့ အမှားမျိုးပါ ....  
ဖိုင်ရဲ့ နောက်ဆုံးစာကြောင်းတစ်ကြောင်းတည်းကို ဖျက်တာလုပ်ချင်ရင် sed command နဲ့ အလွယ်တကူလုပ်လို့ ရပါတယ်။ အောက်ပါအတိုင်းပါ ...  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ sed '$d' < ./2k.test.csv  > tmp.tst
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ mv tmp.tst ./2k.test.csv
```

ဖျက်သွားမသွားကို ပြန်စစ်ကြည့်...  
```
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ tail ./2k.test.csv 
19990,ငါ့ ကို ဘယ်သူ တွေ မေးမြန်း ခဲ့ ကြသေးလဲ ။,ငါ့ ကို ဘယ်သူ တွေ မေး ခဲ့ သေးလဲ ။,1
19991,ထောင်ချ ပစ် ရ မှာ,ထောင် ထဲ မှာ ပစ် ထား တယ်,0
19992,ကလေး တွေ ခုန်ပေါက်ပြေးလွှား ပြီး ကစား နေ ကြ တယ် ။,ကလေး တွေ ပျော်ရွှင် စွာ ရေကူး နေ ကြ တယ် ။,0
19993,တို့ ဆီ ကို မင်း ဘယ်တော့ လာ လည် မှာ လဲ ။,မင်း တို့ ဆီ ကို ဘယ်တော့ ပြန်လာ မှာ လဲ ။,0
19994,တံခါး သွက်သွက် ဖွင့် စမ်း ။,တံခါး မြန်မြန် ပိတ် လိုက် ပါ ။,0
19995,ပြတင်းပေါက် ကို ဖွင့် မ ရ ဘူး ဖြစ် နေ ပါ တယ် ။,ပြတင်းပေါက် ကို ဖွင့် ထား လိုက် ပါ ။,0
19996,ကူညီ ပေး ပါ ရ စေ,ကူညီ ချင် လိုက် တာ,1
19997,ဂွ တော့ အတော် ကျ ကုန် ပြီ,ဂွ ကျ သွား လို့ ကောက် ပေး ပါ,0
19998,ရှိခိုး ဦးချ ပါ တယ်,အမေ့ ကို ရှိခိုး မယ်,0
19999,အကြောင်း အရာ လေး စုံစမ်း ကြည့် ဦး ။,သတင်း လေး စုံစမ်း ကြည့် ဦး ။,1
```

## Some Reference Links

[https://github.com/amansrivastava17/lstm-siamese-text-similarity](https://github.com/amansrivastava17/lstm-siamese-text-similarity)  
[https://www.unix.com/shell-programming-and-scripting/172723-checking-csv-files-empty-fields.html](https://www.unix.com/shell-programming-and-scripting/172723-checking-csv-files-empty-fields.html)

