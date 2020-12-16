# LSTM-Siamese-Text-Similarities-Installation

Some notes of installation/training of LSTM based Siamese Network for my PhD student Myint Myint Htay (UTYCC).  
အရင်ဆုံး git clone https://github.com/amansrivastava17/lstm-siamese-text-similarity လုပ်ခဲ့တယ်။   

## Creating a New Conda Environment

Tensorflow framework နဲ့ Keras ကိုလည်း သုံးထားတာမို့၊ ကောင်းတာက အရင်ဆုံး conda environment အသစ်လုပ်ပြီး ဖြစ်နိုင်သ၍  
သုံးမယ့် lstm-siamese code က သုံးထားတဲ့ library လိုအပ်ချက်တွေကို ပြင်ဆင်တာက ကောင်းတာမို့ ...   
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

LSTM-Siamese model ကို training လုပ်ဖို့အတွက် ရှာကြည့်တော့ train-sample.py ဆိုတဲ့ python script ကိုရှာတွေ့လို့ အဲဒီ code နဲ့  
တင်ပေးထားတဲ့ sample data ကို သုံးပြီး စမ်းကြည့်တော့ အောက်ပါအတိုင်း error တွေ့ရ...  
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

Very fast!!!
Accuracy က သိပ်အကောင်းကြီး မဟုတ်ပေမဲ့ လက်ရှိဒေတာနဲ့ လက်ရှိ setting နဲ့ အချိန်တိုတိုအတွင်းမှာ similarity measure လုပ်နိုင်တာမို့   
ရည်ရွယ်ထားတဲ့ paraphrase experiment အတွက် အဆင်ပြေနိုင်တယ် ... :)

## Testing

Testing ကိုလည်း သူ့မှာ ပါတဲ့ original script ဖြစ်တဲ့ test-sample.py နဲ့ စမ်းကြည့်ခဲ့တယ်။  
Error အမျိုးမျိုး ပေးတယ်။  

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

ဒီ testing code မှာက similarity ကိုတိုင်းတာချင်တဲ့ စာကြောင်းတွေကို source code ထဲကနေ ပေးထားတယ်။  
output မှာတော့ အထက်မှာ မြင်ရတဲ့အတိုင်း score တွေကို သေချာထုတ်ပေးလို့ အဆင်ပြေတယ်။  

## Testing with paraphrase data

မနေ့ကညကလား ပို့ထားတဲ့ manual ပြင်ဆင်နေတဲ့ paraphrase မဟုတ်တဲ့ စာကြောင်း တစ်သောင်းနဲ့   
လက်ရှိ ရှိနေတဲ့ paraphrase စာကြောင်း ရှစ်သောင်းကျော်ကနေ တစ်သောင်းကို ဆွဲထုတ်ယူပြီး test experiment လုပ်ကြည့်မယ်။  
အရင်ဆုံး အောက်ပါအတိုင်း ဒေတာတွေကို ပြင်ဆင်တယ်။

```
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ cp /media/ye/project1/student/utycc-newR/seminar/6thSeminar/MyintMyintHtay/23Nov2020/forsec/paraphrase_sentence.final .

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ cp /media/ye/project1/student/utycc-newR/seminar/6thSeminar/MyintMyintHtay/16Dec2020/not-para-human.5k.txt .

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head -n 10000 ./paraphrase_sentence.final > 10k.para

original paraphrase data 10k ရဲ့ format က အောက်ပါအတိုင်း

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

sed command ကို သုံးပြီးတော့ format ပြောင်းတယ်။
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ sed 's/\(.*\)/\1,1/;s/\t/,/' < ./10k.para > ./10k.para.format

လိုချင်တဲ့ format တော့ ရသွားပြီ။ အောက်ပါအတိုင်း

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

non-paraphrase ပြင်ဆင်တယ်။ အောက်ပါအတိုင်း

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

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ sed 's/\t/,/g' < ./not-para-human.5k.txt > ./not-para-human.5k.txt.format

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

paraphrase data + not paraphrase data (နှစ်မျိုးကို ပေါင်းတယ်)

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ cat ./10k.para.format ./not-para-human.5k.txt.format > para-not-para
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ wc ./para-not-para 
  20000  288758 3962466 ./para-not-para

shuffle လုပ်တယ်
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ shuf ./para-not-para > ./para-not-para.shuf

Format checking ကို အကြမ်းလုပ်ခဲ့။ It looks OK ...

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

## prepare line number

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

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ paste line-no ./para-not-para.shuf -d"," > ./line-no.para-no-para.shuf

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

## Adding column header

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ (echo ",sentences1,sentences2,is_similar" && cat ./line-no.para-no-para.shuf) > line-no.para-no-para.shuf.final

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

သူ Python code ကသုံးထားတဲ့ column header အတိုင်းပဲ ထားထားလိုက်တယ်။
နာမည်က သိပ်ပြဿနာမရှိလို့ နောက်ပြီး code အထဲက ဖတ်ထားတဲ့ စာကြောင်းတွေကိုလည်း ဝင်မပြင်ချင်လို့ ...


## Split Training Data and Test Data

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ head -n 8000 ./line-no.para-no-para.shuf.final > ../8k.train.csv
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ tail -n 2000 ./line-no.para-no-para.shuf.final > ../2k.test.csv 
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ cd ..
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ ls
2k.test.csv  8k.train.csv  original

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ wc *.csv
   2000   29501  416641 2k.test.csv
   8000  115563 1621115 8k.train.csv
  10000  145064 2037756 total

Check the file again:
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ head ./8k.train.csv 
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
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ head ./2k.test.csv 
18001,ဦးခိုက်ရှိခိုး ပါ ၏,ဦးခိုက် ပါ တယ်,1
18002,ဆရာတော် ကြီး များ သက်တော် ရာ ကျော် ရှည် ပါ စေ,ဆရာတော် ကြီး များ ကျန်းမာ သက် ရှည် ပါ စေ,1
18003,ကြိုက် သွား ပြီ,ကြိုဆို လိုက် ပါ,0
18004,စောက် လုပ် ကို ရှုပ် တယ်,စောက် လုပ် တွေ က ရှုပ် နေ တာ ပဲ,1
18005,သူ နဲ့ ကင်းကွာ နေ တာ ကြာ ပြီ,သူ နဲ့ အနီးဆုံး မှာ ပဲ နေ ပါ တယ်,0
18006,ထမင်း ကို ဖိတ်စင် အောင် မ စား ပါ နဲ့ ။,ရေ ကို ဖိတ်စင် အောင် မ ခပ် ပါ နဲ့ ။,0
18007,မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း များ သည် ဗွက် ဖြစ် နေ သည် ။,မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း မှာ ကောင်းကောင်း သွား မ ရ ပါ ။,0
18008,ရွဲ့လားစောင်းလား မ လုပ် နဲ့ နော်,စောင်း ပြော နေ တာ လား,1
18009,ဝမ်းမြောက် ဝမ်းသာ ဖြစ် မိ ပါ သည်,ဝမ်းမြောက် ဝမ်းသာ ရှိ လှ ပေ စွ,1
18010,တော် တယ် ဆက် ပြီး တော့ ကြိုးစား ပါ,တော် တယ် ဆက် ကြိုးစား ပါ,1

## Copy and Editing the Python Script

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ cp train-sample.py train-para1.py
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ gedit train-para1.py

အောက်ပါလိုင်းတွေကို update လုပ်ခဲ့ ...
#df = pd.read_csv('sample_data.csv')
df = pd.read_csv('./para-tst-1/8k.train.csv')

## Backup checkpoints folder
(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ mv checkpoints/ checkpoints.bak

(base) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ conda activate tensor1.15.4_keras2.2.4
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ 

## Training-1

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ time python ./train-para1.py 2>&1 | tee ./para-tst-1/para1.train.log1
Using TensorFlow backend.
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:74: The name tf.get_default_graph is deprecated. Please use tf.compat.v1.get_default_graph instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:517: The name tf.placeholder is deprecated. Please use tf.compat.v1.placeholder instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:4138: The name tf.random_uniform is deprecated. Please use tf.random.uniform instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:174: The name tf.get_default_session is deprecated. Please use tf.compat.v1.get_default_session instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:181: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/backend/tensorflow_backend.py:186: The name tf.Session is deprecated. Please use tf.compat.v1.Session instead.

2020-12-16 04:12:53.959375: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2893330000 Hz
2020-12-16 04:12:53.959812: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55f0960cdb50 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-12-16 04:12:53.959848: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
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

Embedding matrix shape: (7528, 50)
Null word embeddings: 1
Train on 7200 samples, validate on 799 samples
Epoch 1/200

  64/7200 [..............................] - ETA: 5:37 - loss: 1.0756 - acc: 0.3750
 192/7200 [..............................] - ETA: 1:52 - loss: 0.8809 - acc: 0.5729
 320/7200 [>.............................] - ETA: 1:07 - loss: 0.8457 - acc: 0.5844
 448/7200 [>.............................] - ETA: 48s - loss: 0.7863 - acc: 0.6138 
 576/7200 [=>............................] - ETA: 37s - loss: 0.7826 - acc: 0.6198
 704/7200 [=>............................] - ETA: 31s - loss: 0.7631 - acc: 0.6179
 832/7200 [==>...........................] - ETA: 26s - loss: 0.7399 - acc: 0.6250
 960/7200 [===>..........................] - ETA: 22s - loss: 0.7098 - acc: 0.6385
1088/7200 [===>..........................] - ETA: 19s - loss: 0.7016 - acc: 0.6434
1216/7200 [====>.........................] - ETA: 17s - loss: 0.6818 - acc: 0.6554
1344/7200 [====>.........................] - ETA: 16s - loss: 0.6699 - acc: 0.6644
1472/7200 [=====>........................] - ETA: 14s - loss: 0.6610 - acc: 0.6746
1600/7200 [=====>........................] - ETA: 13s - loss: 0.6551 - acc: 0.6787
1728/7200 [======>.......................] - ETA: 12s - loss: 0.6493 - acc: 0.6817
1856/7200 [======>.......................] - ETA: 11s - loss: 0.6391 - acc: 0.6891
1984/7200 [=======>......................] - ETA: 10s - loss: 0.6257 - acc: 0.6951
2112/7200 [=======>......................] - ETA: 9s - loss: 0.6232 - acc: 0.6984 
2240/7200 [========>.....................] - ETA: 9s - loss: 0.6117 - acc: 0.7031
2368/7200 [========>.....................] - ETA: 8s - loss: 0.5995 - acc: 0.7103
2496/7200 [=========>....................] - ETA: 8s - loss: 0.5957 - acc: 0.7119
2624/7200 [=========>....................] - ETA: 7s - loss: 0.5879 - acc: 0.7157
2752/7200 [==========>...................] - ETA: 7s - loss: 0.5801 - acc: 0.7198
2880/7200 [===========>..................] - ETA: 6s - loss: 0.5753 - acc: 0.7233
3008/7200 [===========>..................] - ETA: 6s - loss: 0.5686 - acc: 0.7277
3136/7200 [============>.................] - ETA: 5s - loss: 0.5645 - acc: 0.7318
3264/7200 [============>.................] - ETA: 5s - loss: 0.5553 - acc: 0.7365
3392/7200 [=============>................] - ETA: 5s - loss: 0.5541 - acc: 0.7385
3520/7200 [=============>................] - ETA: 4s - loss: 0.5504 - acc: 0.7415
3648/7200 [==============>...............] - ETA: 4s - loss: 0.5436 - acc: 0.7453
3776/7200 [==============>...............] - ETA: 4s - loss: 0.5371 - acc: 0.7487
3904/7200 [===============>..............] - ETA: 4s - loss: 0.5308 - acc: 0.7533
4032/7200 [===============>..............] - ETA: 3s - loss: 0.5273 - acc: 0.7560
4160/7200 [================>.............] - ETA: 3s - loss: 0.5240 - acc: 0.7575
4288/7200 [================>.............] - ETA: 3s - loss: 0.5207 - acc: 0.7586
4416/7200 [=================>............] - ETA: 3s - loss: 0.5207 - acc: 0.7591
4544/7200 [=================>............] - ETA: 3s - loss: 0.5177 - acc: 0.7606
4672/7200 [==================>...........] - ETA: 2s - loss: 0.5157 - acc: 0.7616
4800/7200 [===================>..........] - ETA: 2s - loss: 0.5140 - acc: 0.7635
4928/7200 [===================>..........] - ETA: 2s - loss: 0.5120 - acc: 0.7652
5056/7200 [====================>.........] - ETA: 2s - loss: 0.5086 - acc: 0.7678
5184/7200 [====================>.........] - ETA: 2s - loss: 0.5053 - acc: 0.7697
5312/7200 [=====================>........] - ETA: 2s - loss: 0.5011 - acc: 0.7713
5440/7200 [=====================>........] - ETA: 1s - loss: 0.4998 - acc: 0.7713
5568/7200 [======================>.......] - ETA: 1s - loss: 0.4972 - acc: 0.7733
5696/7200 [======================>.......] - ETA: 1s - loss: 0.4954 - acc: 0.7741
5824/7200 [=======================>......] - ETA: 1s - loss: 0.4903 - acc: 0.7771
5952/7200 [=======================>......] - ETA: 1s - loss: 0.4876 - acc: 0.7786
6080/7200 [========================>.....] - ETA: 1s - loss: 0.4866 - acc: 0.7801
6208/7200 [========================>.....] - ETA: 0s - loss: 0.4849 - acc: 0.7811
6336/7200 [=========================>....] - ETA: 0s - loss: 0.4822 - acc: 0.7827
6464/7200 [=========================>....] - ETA: 0s - loss: 0.4797 - acc: 0.7845
6592/7200 [==========================>...] - ETA: 0s - loss: 0.4765 - acc: 0.7861
6720/7200 [===========================>..] - ETA: 0s - loss: 0.4748 - acc: 0.7856
6848/7200 [===========================>..] - ETA: 0s - loss: 0.4766 - acc: 0.7848
6976/7200 [============================>.] - ETA: 0s - loss: 0.4755 - acc: 0.7856
7104/7200 [============================>.] - ETA: 0s - loss: 0.4739 - acc: 0.7862
7200/7200 [==============================] - 7s 1ms/step - loss: 0.4728 - acc: 0.7864 - val_loss: 0.2934 - val_acc: 0.8686
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/tensor1.15.4_keras2.2.4/lib/python3.6/site-packages/keras/callbacks.py:995: The name tf.Summary is deprecated. Please use tf.compat.v1.Summary instead.

Epoch 2/200

  64/7200 [..............................] - ETA: 4s - loss: 0.2450 - acc: 0.9219
 192/7200 [..............................] - ETA: 3s - loss: 0.3554 - acc: 0.8542
 320/7200 [>.............................] - ETA: 3s - loss: 0.3335 - acc: 0.8562
 448/7200 [>.............................] - ETA: 3s - loss: 0.3719 - acc: 0.8460
 576/7200 [=>............................] - ETA: 3s - loss: 0.3940 - acc: 0.8368
 704/7200 [=>............................] - ETA: 3s - loss: 0.3976 - acc: 0.8338
 832/7200 [==>...........................] - ETA: 3s - loss: 0.3938 - acc: 0.8329
 960/7200 [===>..........................] - ETA: 3s - loss: 0.3948 - acc: 0.8323
1088/7200 [===>..........................] - ETA: 3s - loss: 0.3915 - acc: 0.8336
1216/7200 [====>.........................] - ETA: 3s - loss: 0.4046 - acc: 0.8289
1344/7200 [====>.........................] - ETA: 2s - loss: 0.3910 - acc: 0.8348
1472/7200 [=====>........................] - ETA: 2s - loss: 0.3946 - acc: 0.8356
1600/7200 [=====>........................] - ETA: 2s - loss: 0.3917 - acc: 0.8369
1728/7200 [======>.......................] - ETA: 2s - loss: 0.3900 - acc: 0.8362
1856/7200 [======>.......................] - ETA: 2s - loss: 0.3925 - acc: 0.8335
1984/7200 [=======>......................] - ETA: 2s - loss: 0.3898 - acc: 0.8332
2112/7200 [=======>......................] - ETA: 2s - loss: 0.3900 - acc: 0.8329
2240/7200 [========>.....................] - ETA: 2s - loss: 0.3847 - acc: 0.8357
2368/7200 [========>.....................] - ETA: 2s - loss: 0.3868 - acc: 0.8349
2496/7200 [=========>....................] - ETA: 2s - loss: 0.3910 - acc: 0.8329
2624/7200 [=========>....................] - ETA: 2s - loss: 0.3877 - acc: 0.8342
2752/7200 [==========>...................] - ETA: 2s - loss: 0.3874 - acc: 0.8347
2880/7200 [===========>..................] - ETA: 2s - loss: 0.3876 - acc: 0.8337
3008/7200 [===========>..................] - ETA: 2s - loss: 0.3871 - acc: 0.8338
3136/7200 [============>.................] - ETA: 2s - loss: 0.3884 - acc: 0.8335
3264/7200 [============>.................] - ETA: 1s - loss: 0.3873 - acc: 0.8321
3392/7200 [=============>................] - ETA: 1s - loss: 0.3852 - acc: 0.8328
3520/7200 [=============>................] - ETA: 1s - loss: 0.3850 - acc: 0.8330
3648/7200 [==============>...............] - ETA: 1s - loss: 0.3863 - acc: 0.8320
3776/7200 [==============>...............] - ETA: 1s - loss: 0.3854 - acc: 0.8324
3840/7200 [===============>..............] - ETA: 1s - loss: 0.3845 - acc: 0.8328
3968/7200 [===============>..............] - ETA: 1s - loss: 0.3840 - acc: 0.8332
4096/7200 [================>.............] - ETA: 1s - loss: 0.3863 - acc: 0.8320
4224/7200 [================>.............] - ETA: 1s - loss: 0.3853 - acc: 0.8319
4352/7200 [=================>............] - ETA: 1s - loss: 0.3820 - acc: 0.8339
4480/7200 [=================>............] - ETA: 1s - loss: 0.3830 - acc: 0.8335
4608/7200 [==================>...........] - ETA: 1s - loss: 0.3843 - acc: 0.8320
4736/7200 [==================>...........] - ETA: 1s - loss: 0.3871 - acc: 0.8302
4864/7200 [===================>..........] - ETA: 1s - loss: 0.3841 - acc: 0.8316
4992/7200 [===================>..........] - ETA: 1s - loss: 0.3834 - acc: 0.8319
5120/7200 [====================>.........] - ETA: 1s - loss: 0.3830 - acc: 0.8322
5248/7200 [====================>.........] - ETA: 0s - loss: 0.3819 - acc: 0.8335
5376/7200 [=====================>........] - ETA: 0s - loss: 0.3810 - acc: 0.8344
5504/7200 [=====================>........] - ETA: 0s - loss: 0.3810 - acc: 0.8348
5632/7200 [======================>.......] - ETA: 0s - loss: 0.3799 - acc: 0.8352
5760/7200 [=======================>......] - ETA: 0s - loss: 0.3777 - acc: 0.8366
5888/7200 [=======================>......] - ETA: 0s - loss: 0.3788 - acc: 0.8361
6016/7200 [========================>.....] - ETA: 0s - loss: 0.3822 - acc: 0.8349
6144/7200 [========================>.....] - ETA: 0s - loss: 0.3814 - acc: 0.8354
6272/7200 [=========================>....] - ETA: 0s - loss: 0.3805 - acc: 0.8359
6400/7200 [=========================>....] - ETA: 0s - loss: 0.3816 - acc: 0.8350
6528/7200 [==========================>...] - ETA: 0s - loss: 0.3801 - acc: 0.8349
6656/7200 [==========================>...] - ETA: 0s - loss: 0.3794 - acc: 0.8356
6784/7200 [===========================>..] - ETA: 0s - loss: 0.3789 - acc: 0.8356
6912/7200 [===========================>..] - ETA: 0s - loss: 0.3783 - acc: 0.8362
7040/7200 [============================>.] - ETA: 0s - loss: 0.3787 - acc: 0.8362
7168/7200 [============================>.] - ETA: 0s - loss: 0.3794 - acc: 0.8355
7200/7200 [==============================] - 4s 520us/step - loss: 0.3785 - acc: 0.8361 - val_loss: 0.2804 - val_acc: 0.8811
Epoch 3/200

  64/7200 [..............................] - ETA: 3s - loss: 0.2440 - acc: 0.9062
 192/7200 [..............................] - ETA: 3s - loss: 0.2645 - acc: 0.9167
 320/7200 [>.............................] - ETA: 3s - loss: 0.2831 - acc: 0.8906
 448/7200 [>.............................] - ETA: 3s - loss: 0.3022 - acc: 0.8862
 576/7200 [=>............................] - ETA: 3s - loss: 0.2934 - acc: 0.8837
 704/7200 [=>............................] - ETA: 3s - loss: 0.3097 - acc: 0.8736
 832/7200 [==>...........................] - ETA: 3s - loss: 0.3168 - acc: 0.8714
 960/7200 [===>..........................] - ETA: 3s - loss: 0.3318 - acc: 0.8635
1088/7200 [===>..........................] - ETA: 3s - loss: 0.3378 - acc: 0.8621
1216/7200 [====>.........................] - ETA: 3s - loss: 0.3420 - acc: 0.8594
1344/7200 [====>.........................] - ETA: 2s - loss: 0.3445 - acc: 0.8571
1472/7200 [=====>........................] - ETA: 2s - loss: 0.3517 - acc: 0.8553
1600/7200 [=====>........................] - ETA: 2s - loss: 0.3535 - acc: 0.8562
1728/7200 [======>.......................] - ETA: 2s - loss: 0.3548 - acc: 0.8542
1856/7200 [======>.......................] - ETA: 2s - loss: 0.3492 - acc: 0.8561
1984/7200 [=======>......................] - ETA: 2s - loss: 0.3462 - acc: 0.8553
2112/7200 [=======>......................] - ETA: 2s - loss: 0.3400 - acc: 0.8589
2240/7200 [========>.....................] - ETA: 2s - loss: 0.3485 - acc: 0.8540
2368/7200 [========>.....................] - ETA: 2s - loss: 0.3486 - acc: 0.8543
2496/7200 [=========>....................] - ETA: 2s - loss: 0.3496 - acc: 0.8514
2624/7200 [=========>....................] - ETA: 2s - loss: 0.3533 - acc: 0.8491
2752/7200 [==========>...................] - ETA: 2s - loss: 0.3556 - acc: 0.8481
2880/7200 [===========>..................] - ETA: 2s - loss: 0.3504 - acc: 0.8524
3008/7200 [===========>..................] - ETA: 2s - loss: 0.3492 - acc: 0.8531
3136/7200 [============>.................] - ETA: 2s - loss: 0.3495 - acc: 0.8520
3264/7200 [============>.................] - ETA: 1s - loss: 0.3514 - acc: 0.8514
3392/7200 [=============>................] - ETA: 1s - loss: 0.3492 - acc: 0.8517
3520/7200 [=============>................] - ETA: 1s - loss: 0.3490 - acc: 0.8523
3648/7200 [==============>...............] - ETA: 1s - loss: 0.3506 - acc: 0.8525
3776/7200 [==============>...............] - ETA: 1s - loss: 0.3504 - acc: 0.8514
3904/7200 [===============>..............] - ETA: 1s - loss: 0.3498 - acc: 0.8514
4032/7200 [===============>..............] - ETA: 1s - loss: 0.3492 - acc: 0.8512
4160/7200 [================>.............] - ETA: 1s - loss: 0.3492 - acc: 0.8517
4288/7200 [================>.............] - ETA: 1s - loss: 0.3504 - acc: 0.8510
4416/7200 [=================>............] - ETA: 1s - loss: 0.3531 - acc: 0.8492
4544/7200 [=================>............] - ETA: 1s - loss: 0.3527 - acc: 0.8499
4672/7200 [==================>...........] - ETA: 1s - loss: 0.3545 - acc: 0.8489
4800/7200 [===================>..........] - ETA: 1s - loss: 0.3549 - acc: 0.8488
4928/7200 [===================>..........] - ETA: 1s - loss: 0.3521 - acc: 0.8500
5056/7200 [====================>.........] - ETA: 1s - loss: 0.3525 - acc: 0.8501
5184/7200 [====================>.........] - ETA: 1s - loss: 0.3520 - acc: 0.8499
5312/7200 [=====================>........] - ETA: 0s - loss: 0.3516 - acc: 0.8498
5440/7200 [=====================>........] - ETA: 0s - loss: 0.3506 - acc: 0.8496
5568/7200 [======================>.......] - ETA: 0s - loss: 0.3487 - acc: 0.8508
5696/7200 [======================>.......] - ETA: 0s - loss: 0.3507 - acc: 0.8499
5824/7200 [=======================>......] - ETA: 0s - loss: 0.3510 - acc: 0.8498
5952/7200 [=======================>......] - ETA: 0s - loss: 0.3499 - acc: 0.8501
6080/7200 [========================>.....] - ETA: 0s - loss: 0.3493 - acc: 0.8498
6208/7200 [========================>.....] - ETA: 0s - loss: 0.3483 - acc: 0.8507
6336/7200 [=========================>....] - ETA: 0s - loss: 0.3479 - acc: 0.8505
6464/7200 [=========================>....] - ETA: 0s - loss: 0.3466 - acc: 0.8510
6592/7200 [==========================>...] - ETA: 0s - loss: 0.3446 - acc: 0.8519
6720/7200 [===========================>..] - ETA: 0s - loss: 0.3465 - acc: 0.8516
6848/7200 [===========================>..] - ETA: 0s - loss: 0.3457 - acc: 0.8519
6976/7200 [============================>.] - ETA: 0s - loss: 0.3477 - acc: 0.8512
7104/7200 [============================>.] - ETA: 0s - loss: 0.3503 - acc: 0.8506
7200/7200 [==============================] - 4s 523us/step - loss: 0.3509 - acc: 0.8508 - val_loss: 0.2647 - val_acc: 0.8961
Epoch 4/200

  64/7200 [..............................] - ETA: 3s - loss: 0.2784 - acc: 0.9062
 192/7200 [..............................] - ETA: 3s - loss: 0.3138 - acc: 0.8854
 320/7200 [>.............................] - ETA: 3s - loss: 0.3437 - acc: 0.8688
 448/7200 [>.............................] - ETA: 3s - loss: 0.3532 - acc: 0.8705
 576/7200 [=>............................] - ETA: 3s - loss: 0.3420 - acc: 0.8785
 704/7200 [=>............................] - ETA: 3s - loss: 0.3423 - acc: 0.8778
 832/7200 [==>...........................] - ETA: 3s - loss: 0.3416 - acc: 0.8774
 960/7200 [===>..........................] - ETA: 3s - loss: 0.3476 - acc: 0.8698
1088/7200 [===>..........................] - ETA: 3s - loss: 0.3599 - acc: 0.8603
1216/7200 [====>.........................] - ETA: 3s - loss: 0.3647 - acc: 0.8561
1344/7200 [====>.........................] - ETA: 2s - loss: 0.3646 - acc: 0.8571
1472/7200 [=====>........................] - ETA: 2s - loss: 0.3645 - acc: 0.8560
1600/7200 [=====>........................] - ETA: 2s - loss: 0.3624 - acc: 0.8556
1728/7200 [======>.......................] - ETA: 2s - loss: 0.3588 - acc: 0.8565
1856/7200 [======>.......................] - ETA: 2s - loss: 0.3554 - acc: 0.8594
1984/7200 [=======>......................] - ETA: 2s - loss: 0.3592 - acc: 0.8558
2112/7200 [=======>......................] - ETA: 2s - loss: 0.3626 - acc: 0.8542
2240/7200 [========>.....................] - ETA: 2s - loss: 0.3644 - acc: 0.8513
2368/7200 [========>.....................] - ETA: 2s - loss: 0.3632 - acc: 0.8522
2496/7200 [=========>....................] - ETA: 2s - loss: 0.3650 - acc: 0.8514
2624/7200 [=========>....................] - ETA: 2s - loss: 0.3639 - acc: 0.8506
2752/7200 [==========>...................] - ETA: 2s - loss: 0.3654 - acc: 0.8499
2880/7200 [===========>..................] - ETA: 2s - loss: 0.3630 - acc: 0.8500
3008/7200 [===========>..................] - ETA: 2s - loss: 0.3630 - acc: 0.8511
3136/7200 [============>.................] - ETA: 2s - loss: 0.3642 - acc: 0.8495
3264/7200 [============>.................] - ETA: 1s - loss: 0.3621 - acc: 0.8493
3392/7200 [=============>................] - ETA: 1s - loss: 0.3630 - acc: 0.8479
3520/7200 [=============>................] - ETA: 1s - loss: 0.3616 - acc: 0.8486
3648/7200 [==============>...............] - ETA: 1s - loss: 0.3594 - acc: 0.8495
3776/7200 [==============>...............] - ETA: 1s - loss: 0.3577 - acc: 0.8496
3904/7200 [===============>..............] - ETA: 1s - loss: 0.3576 - acc: 0.8494
4032/7200 [===============>..............] - ETA: 1s - loss: 0.3562 - acc: 0.8502
4160/7200 [================>.............] - ETA: 1s - loss: 0.3574 - acc: 0.8498
4288/7200 [================>.............] - ETA: 1s - loss: 0.3575 - acc: 0.8493
4416/7200 [=================>............] - ETA: 1s - loss: 0.3556 - acc: 0.8508
4544/7200 [=================>............] - ETA: 1s - loss: 0.3546 - acc: 0.8508
4672/7200 [==================>...........] - ETA: 1s - loss: 0.3567 - acc: 0.8502
4800/7200 [===================>..........] - ETA: 1s - loss: 0.3551 - acc: 0.8510
4928/7200 [===================>..........] - ETA: 1s - loss: 0.3560 - acc: 0.8502
5056/7200 [====================>.........] - ETA: 1s - loss: 0.3585 - acc: 0.8491
5184/7200 [====================>.........] - ETA: 1s - loss: 0.3590 - acc: 0.8484
5312/7200 [=====================>........] - ETA: 0s - loss: 0.3588 - acc: 0.8486
5440/7200 [=====================>........] - ETA: 0s - loss: 0.3603 - acc: 0.8487
5568/7200 [======================>.......] - ETA: 0s - loss: 0.3604 - acc: 0.8479
5696/7200 [======================>.......] - ETA: 0s - loss: 0.3584 - acc: 0.8490
5824/7200 [=======================>......] - ETA: 0s - loss: 0.3565 - acc: 0.8498
5952/7200 [=======================>......] - ETA: 0s - loss: 0.3559 - acc: 0.8501
6080/7200 [========================>.....] - ETA: 0s - loss: 0.3543 - acc: 0.8515
6208/7200 [========================>.....] - ETA: 0s - loss: 0.3518 - acc: 0.8528
6336/7200 [=========================>....] - ETA: 0s - loss: 0.3513 - acc: 0.8531
6464/7200 [=========================>....] - ETA: 0s - loss: 0.3485 - acc: 0.8544
6592/7200 [==========================>...] - ETA: 0s - loss: 0.3488 - acc: 0.8547
6720/7200 [===========================>..] - ETA: 0s - loss: 0.3499 - acc: 0.8536
6848/7200 [===========================>..] - ETA: 0s - loss: 0.3492 - acc: 0.8532
6976/7200 [============================>.] - ETA: 0s - loss: 0.3485 - acc: 0.8531
7104/7200 [============================>.] - ETA: 0s - loss: 0.3497 - acc: 0.8526
7200/7200 [==============================] - 4s 518us/step - loss: 0.3502 - acc: 0.8528 - val_loss: 0.2691 - val_acc: 0.8961
Epoch 5/200

  64/7200 [..............................] - ETA: 3s - loss: 0.3862 - acc: 0.8594
 192/7200 [..............................] - ETA: 3s - loss: 0.3303 - acc: 0.8490
 320/7200 [>.............................] - ETA: 3s - loss: 0.3520 - acc: 0.8438
 448/7200 [>.............................] - ETA: 3s - loss: 0.3484 - acc: 0.8415
 576/7200 [=>............................] - ETA: 3s - loss: 0.3367 - acc: 0.8507
 704/7200 [=>............................] - ETA: 3s - loss: 0.3455 - acc: 0.8494
 832/7200 [==>...........................] - ETA: 3s - loss: 0.3500 - acc: 0.8438
 960/7200 [===>..........................] - ETA: 3s - loss: 0.3451 - acc: 0.8500
1088/7200 [===>..........................] - ETA: 3s - loss: 0.3601 - acc: 0.8392
1216/7200 [====>.........................] - ETA: 3s - loss: 0.3559 - acc: 0.8446
1344/7200 [====>.........................] - ETA: 2s - loss: 0.3565 - acc: 0.8445
1472/7200 [=====>........................] - ETA: 2s - loss: 0.3512 - acc: 0.8471
1600/7200 [=====>........................] - ETA: 2s - loss: 0.3483 - acc: 0.8500
1728/7200 [======>.......................] - ETA: 2s - loss: 0.3464 - acc: 0.8507
1856/7200 [======>.......................] - ETA: 2s - loss: 0.3458 - acc: 0.8497
1984/7200 [=======>......................] - ETA: 2s - loss: 0.3385 - acc: 0.8518
2112/7200 [=======>......................] - ETA: 2s - loss: 0.3344 - acc: 0.8532
2240/7200 [========>.....................] - ETA: 2s - loss: 0.3367 - acc: 0.8518
2368/7200 [========>.....................] - ETA: 2s - loss: 0.3379 - acc: 0.8509
2496/7200 [=========>....................] - ETA: 2s - loss: 0.3364 - acc: 0.8526
2624/7200 [=========>....................] - ETA: 2s - loss: 0.3392 - acc: 0.8529
2752/7200 [==========>...................] - ETA: 2s - loss: 0.3412 - acc: 0.8521
2880/7200 [===========>..................] - ETA: 2s - loss: 0.3396 - acc: 0.8531
3008/7200 [===========>..................] - ETA: 2s - loss: 0.3375 - acc: 0.8544
3136/7200 [============>.................] - ETA: 2s - loss: 0.3368 - acc: 0.8530
3264/7200 [============>.................] - ETA: 1s - loss: 0.3373 - acc: 0.8529
3392/7200 [=============>................] - ETA: 1s - loss: 0.3374 - acc: 0.8526
3520/7200 [=============>................] - ETA: 1s - loss: 0.3384 - acc: 0.8520
3648/7200 [==============>...............] - ETA: 1s - loss: 0.3357 - acc: 0.8533
3776/7200 [==============>...............] - ETA: 1s - loss: 0.3343 - acc: 0.8533
3904/7200 [===============>..............] - ETA: 1s - loss: 0.3376 - acc: 0.8514
4032/7200 [===============>..............] - ETA: 1s - loss: 0.3394 - acc: 0.8497
4160/7200 [================>.............] - ETA: 1s - loss: 0.3382 - acc: 0.8507
4288/7200 [================>.............] - ETA: 1s - loss: 0.3388 - acc: 0.8505
4416/7200 [=================>............] - ETA: 1s - loss: 0.3379 - acc: 0.8508
4544/7200 [=================>............] - ETA: 1s - loss: 0.3376 - acc: 0.8504
4672/7200 [==================>...........] - ETA: 1s - loss: 0.3370 - acc: 0.8502
4800/7200 [===================>..........] - ETA: 1s - loss: 0.3387 - acc: 0.8498
4928/7200 [===================>..........] - ETA: 1s - loss: 0.3365 - acc: 0.8513
5056/7200 [====================>.........] - ETA: 1s - loss: 0.3344 - acc: 0.8523
5184/7200 [====================>.........] - ETA: 1s - loss: 0.3334 - acc: 0.8526
5312/7200 [=====================>........] - ETA: 0s - loss: 0.3314 - acc: 0.8537
5440/7200 [=====================>........] - ETA: 0s - loss: 0.3311 - acc: 0.8533
5568/7200 [======================>.......] - ETA: 0s - loss: 0.3321 - acc: 0.8540
5696/7200 [======================>.......] - ETA: 0s - loss: 0.3332 - acc: 0.8539
5824/7200 [=======================>......] - ETA: 0s - loss: 0.3343 - acc: 0.8535
5952/7200 [=======================>......] - ETA: 0s - loss: 0.3353 - acc: 0.8533
6080/7200 [========================>.....] - ETA: 0s - loss: 0.3338 - acc: 0.8543
6208/7200 [========================>.....] - ETA: 0s - loss: 0.3345 - acc: 0.8544
6336/7200 [=========================>....] - ETA: 0s - loss: 0.3339 - acc: 0.8543
6464/7200 [=========================>....] - ETA: 0s - loss: 0.3328 - acc: 0.8554
6592/7200 [==========================>...] - ETA: 0s - loss: 0.3322 - acc: 0.8560
6720/7200 [===========================>..] - ETA: 0s - loss: 0.3324 - acc: 0.8560
6848/7200 [===========================>..] - ETA: 0s - loss: 0.3313 - acc: 0.8567
6976/7200 [============================>.] - ETA: 0s - loss: 0.3314 - acc: 0.8564
7104/7200 [============================>.] - ETA: 0s - loss: 0.3312 - acc: 0.8570
7200/7200 [==============================] - 4s 515us/step - loss: 0.3316 - acc: 0.8567 - val_loss: 0.2762 - val_acc: 0.8761
Epoch 6/200

  64/7200 [..............................] - ETA: 4s - loss: 0.3802 - acc: 0.8438
 192/7200 [..............................] - ETA: 3s - loss: 0.3610 - acc: 0.8542
 320/7200 [>.............................] - ETA: 3s - loss: 0.3430 - acc: 0.8531
 448/7200 [>.............................] - ETA: 3s - loss: 0.3222 - acc: 0.8683
 576/7200 [=>............................] - ETA: 3s - loss: 0.3055 - acc: 0.8767
 704/7200 [=>............................] - ETA: 3s - loss: 0.3121 - acc: 0.8778
 832/7200 [==>...........................] - ETA: 3s - loss: 0.3092 - acc: 0.8774
 960/7200 [===>..........................] - ETA: 3s - loss: 0.3081 - acc: 0.8781
1088/7200 [===>..........................] - ETA: 3s - loss: 0.3100 - acc: 0.8778
1216/7200 [====>.........................] - ETA: 2s - loss: 0.3096 - acc: 0.8775
1344/7200 [====>.........................] - ETA: 2s - loss: 0.3146 - acc: 0.8743
1472/7200 [=====>........................] - ETA: 2s - loss: 0.3144 - acc: 0.8730
1600/7200 [=====>........................] - ETA: 2s - loss: 0.3261 - acc: 0.8625
1728/7200 [======>.......................] - ETA: 2s - loss: 0.3218 - acc: 0.8640
1856/7200 [======>.......................] - ETA: 2s - loss: 0.3208 - acc: 0.8637
1984/7200 [=======>......................] - ETA: 2s - loss: 0.3180 - acc: 0.8639
2112/7200 [=======>......................] - ETA: 2s - loss: 0.3268 - acc: 0.8608
2240/7200 [========>.....................] - ETA: 2s - loss: 0.3259 - acc: 0.8625
2368/7200 [========>.....................] - ETA: 2s - loss: 0.3289 - acc: 0.8594
2496/7200 [=========>....................] - ETA: 2s - loss: 0.3286 - acc: 0.8594
2624/7200 [=========>....................] - ETA: 2s - loss: 0.3287 - acc: 0.8598
2752/7200 [==========>...................] - ETA: 2s - loss: 0.3271 - acc: 0.8605
2880/7200 [===========>..................] - ETA: 2s - loss: 0.3268 - acc: 0.8618
3008/7200 [===========>..................] - ETA: 2s - loss: 0.3276 - acc: 0.8614
3136/7200 [============>.................] - ETA: 2s - loss: 0.3279 - acc: 0.8607
3264/7200 [============>.................] - ETA: 1s - loss: 0.3278 - acc: 0.8606
3392/7200 [=============>................] - ETA: 1s - loss: 0.3273 - acc: 0.8611
3520/7200 [=============>................] - ETA: 1s - loss: 0.3281 - acc: 0.8608
3648/7200 [==============>...............] - ETA: 1s - loss: 0.3288 - acc: 0.8607
3776/7200 [==============>...............] - ETA: 1s - loss: 0.3299 - acc: 0.8607
3904/7200 [===============>..............] - ETA: 1s - loss: 0.3344 - acc: 0.8578
4032/7200 [===============>..............] - ETA: 1s - loss: 0.3377 - acc: 0.8559
4160/7200 [================>.............] - ETA: 1s - loss: 0.3362 - acc: 0.8562
4288/7200 [================>.............] - ETA: 1s - loss: 0.3358 - acc: 0.8566
4416/7200 [=================>............] - ETA: 1s - loss: 0.3341 - acc: 0.8573
4544/7200 [=================>............] - ETA: 1s - loss: 0.3323 - acc: 0.8578
4672/7200 [==================>...........] - ETA: 1s - loss: 0.3331 - acc: 0.8585
4800/7200 [===================>..........] - ETA: 1s - loss: 0.3343 - acc: 0.8588
4928/7200 [===================>..........] - ETA: 1s - loss: 0.3351 - acc: 0.8586
5056/7200 [====================>.........] - ETA: 1s - loss: 0.3343 - acc: 0.8584
5184/7200 [====================>.........] - ETA: 1s - loss: 0.3328 - acc: 0.8592
5312/7200 [=====================>........] - ETA: 0s - loss: 0.3323 - acc: 0.8586
5440/7200 [=====================>........] - ETA: 0s - loss: 0.3325 - acc: 0.8594
5568/7200 [======================>.......] - ETA: 0s - loss: 0.3311 - acc: 0.8597
5696/7200 [======================>.......] - ETA: 0s - loss: 0.3314 - acc: 0.8594
5824/7200 [=======================>......] - ETA: 0s - loss: 0.3316 - acc: 0.8590
5952/7200 [=======================>......] - ETA: 0s - loss: 0.3324 - acc: 0.8584
6080/7200 [========================>.....] - ETA: 0s - loss: 0.3328 - acc: 0.8577
6208/7200 [========================>.....] - ETA: 0s - loss: 0.3331 - acc: 0.8573
6336/7200 [=========================>....] - ETA: 0s - loss: 0.3324 - acc: 0.8580
6464/7200 [=========================>....] - ETA: 0s - loss: 0.3325 - acc: 0.8574
6592/7200 [==========================>...] - ETA: 0s - loss: 0.3302 - acc: 0.8586
6720/7200 [===========================>..] - ETA: 0s - loss: 0.3302 - acc: 0.8585
6848/7200 [===========================>..] - ETA: 0s - loss: 0.3306 - acc: 0.8582
6976/7200 [============================>.] - ETA: 0s - loss: 0.3304 - acc: 0.8582
7104/7200 [============================>.] - ETA: 0s - loss: 0.3296 - acc: 0.8581
7200/7200 [==============================] - 4s 515us/step - loss: 0.3297 - acc: 0.8583 - val_loss: 0.2858 - val_acc: 0.8761

real	0m37.131s
user	1m30.965s
sys	0m2.171s
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$

## Editing testing python file

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ gedit test-para1.py

မော်ဒယ် ရှိတဲ့ path နဲ့ model ဖိုင်နာမည်ကို ရိုက်ထည့်ပေးရမယ်။
ပုံမှန်အားဖြင့် မော်ဒယ်က checkpoints ဆိုတဲ့ အောက်မှာ သိမ်းလိမ့်မယ်။
နံပါတ်အကြီးဆုံးဟာက နောက်ဆုံး မော်ဒယ်လို့ စဉ်းစားလို့ ရတယ်။

#model = load_model("/media/ye/project1/tool/lstm-siamese-text-similarity/checkpoints/1605650354/lstm_50_50_0.17_0.25.h5")
model = load_model("/media/ye/project1/tool/lstm-siamese-text-similarity/checkpoints/1608068575/lstm_50_50_0.17_0.25.h5")

လက်ရှိ testing python ဖိုင် မှာက စာကြောင်းအချို့ကို ရိုက်ထည့်ထားပြီး စမ်းထားတာမို့ အဲဒါကို အရင် အစားထိုးကြည့်ပြီး testing လုပ်ခဲ့တယ်။ ဗမာစာကြောင်းတွေက test ဖိုင်ကနေ ယူထားတယ်။

#test_sentence_pairs = [('What can make Physics easy to learn?','How can you make physics easy to learn?'),('How many times a day do a clocks hands overlap?','What does it mean that every time I look at the clock the numbers are the same?')]
test_sentence_pairs = [('ဦးခိုက်ရှိခိုး ပါ ၏','ဦးခိုက် ပါ တယ်'),('ဆရာတော် ကြီး များ သက်တော် ရာ ကျော် ရှည် ပါ စေ','ဆရာတော် ကြီး များ ကျန်းမာ သက် ရှည် ပါ စေ'),('ကြိုက် သွား ပြီ','ကြိုဆို လိုက် ပါ'),('စောက် လုပ် ကို ရှုပ် တယ်','စောက် လုပ် တွေ က ရှုပ် နေ တာ ပဲ'),('သူ နဲ့ ကင်းကွာ နေ တာ ကြာ ပြီ','သူ နဲ့ အနီးဆုံး မှာ ပဲ နေ ပါ တယ်'),('ထမင်း ကို ဖိတ်စင် အောင် မ စား ပါ နဲ့ ။','ရေ ကို ဖိတ်စင် အောင် မ ခပ် ပါ နဲ့ ။'),('မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း များ သည် ဗွက် ဖြစ် နေ သည် ။','မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း မှာ ကောင်းကောင်း သွား မ ရ ပါ ။'),('ရွဲ့လားစောင်းလား မ လုပ် နဲ့ နော်','စောင်း ပြော နေ တာ လား'),('ဝမ်းမြောက် ဝမ်းသာ ဖြစ် မိ ပါ သည်','ဝမ်းမြောက် ဝမ်းသာ ရှိ လှ ပေ စွ'),('တော် တယ် ဆက် ပြီး တော့ ကြိုးစား ပါ','တော် တယ် ဆက် ကြိုးစား ပါ')]

## Testing-1

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

## How about increasing no. of epoch for training?!

model.py ဖိုင်မှာ အောက်ပါ statement ကို တွေ့ခဲ့

        model.fit([train_data_x1, train_data_x2, leaks_train], train_labels,
                  validation_data=([val_data_x1, val_data_x2, leaks_val], val_labels),
                  epochs=50, batch_size=3, shuffle=True,
                  callbacks=[early_stopping, model_checkpoint, tensorboard])

code ကတော့ အသေတွေဖြစ်နေလို့ coding ဖိုင်ထဲကို ဝင်ပြင်မှရတဲ့ ပုံစံတော့ ဖြစ်နေတယ်။
epochs=100 ထားကြည့်မယ်။

## Training with epoch 100

Epoch 15/200

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ time python ./train-para1.py 2>&1 | tee ./para-tst-1/para1.train.log2
...
...
  64/7200 [..............................] - ETA: 4s - loss: 0.5177 - acc: 0.7969
 192/7200 [..............................] - ETA: 4s - loss: 0.3482 - acc: 0.8542
 320/7200 [>.............................] - ETA: 3s - loss: 0.2993 - acc: 0.8781
 448/7200 [>.............................] - ETA: 3s - loss: 0.2853 - acc: 0.8929
 576/7200 [=>............................] - ETA: 3s - loss: 0.3203 - acc: 0.8767
 704/7200 [=>............................] - ETA: 3s - loss: 0.3018 - acc: 0.8835
 832/7200 [==>...........................] - ETA: 3s - loss: 0.3022 - acc: 0.8834
 960/7200 [===>..........................] - ETA: 3s - loss: 0.2991 - acc: 0.8823
1088/7200 [===>..........................] - ETA: 3s - loss: 0.3041 - acc: 0.8796
1216/7200 [====>.........................] - ETA: 3s - loss: 0.3039 - acc: 0.8775
1344/7200 [====>.........................] - ETA: 3s - loss: 0.3020 - acc: 0.8780
1472/7200 [=====>........................] - ETA: 3s - loss: 0.3010 - acc: 0.8784
1600/7200 [=====>........................] - ETA: 3s - loss: 0.2978 - acc: 0.8781
1728/7200 [======>.......................] - ETA: 2s - loss: 0.2971 - acc: 0.8767
1856/7200 [======>.......................] - ETA: 2s - loss: 0.2991 - acc: 0.8777
1984/7200 [=======>......................] - ETA: 2s - loss: 0.2970 - acc: 0.8785
2112/7200 [=======>......................] - ETA: 2s - loss: 0.2946 - acc: 0.8797
2240/7200 [========>.....................] - ETA: 2s - loss: 0.2950 - acc: 0.8781
2368/7200 [========>.....................] - ETA: 2s - loss: 0.2938 - acc: 0.8784
2496/7200 [=========>....................] - ETA: 2s - loss: 0.2943 - acc: 0.8782
2624/7200 [=========>....................] - ETA: 2s - loss: 0.2928 - acc: 0.8788
2752/7200 [==========>...................] - ETA: 2s - loss: 0.2912 - acc: 0.8808
2880/7200 [===========>..................] - ETA: 2s - loss: 0.2880 - acc: 0.8826
3008/7200 [===========>..................] - ETA: 2s - loss: 0.2880 - acc: 0.8826
3136/7200 [============>.................] - ETA: 2s - loss: 0.2863 - acc: 0.8827
3264/7200 [============>.................] - ETA: 2s - loss: 0.2850 - acc: 0.8833
3392/7200 [=============>................] - ETA: 2s - loss: 0.2866 - acc: 0.8818
3520/7200 [=============>................] - ETA: 1s - loss: 0.2856 - acc: 0.8815
3648/7200 [==============>...............] - ETA: 1s - loss: 0.2846 - acc: 0.8819
3776/7200 [==============>...............] - ETA: 1s - loss: 0.2876 - acc: 0.8803
3904/7200 [===============>..............] - ETA: 1s - loss: 0.2847 - acc: 0.8819
4032/7200 [===============>..............] - ETA: 1s - loss: 0.2853 - acc: 0.8822
4160/7200 [================>.............] - ETA: 1s - loss: 0.2861 - acc: 0.8820
4288/7200 [================>.............] - ETA: 1s - loss: 0.2838 - acc: 0.8829
4416/7200 [=================>............] - ETA: 1s - loss: 0.2845 - acc: 0.8816
4544/7200 [=================>............] - ETA: 1s - loss: 0.2849 - acc: 0.8816
4672/7200 [==================>...........] - ETA: 1s - loss: 0.2877 - acc: 0.8812
4800/7200 [===================>..........] - ETA: 1s - loss: 0.2867 - acc: 0.8815
4928/7200 [===================>..........] - ETA: 1s - loss: 0.2885 - acc: 0.8801
5056/7200 [====================>.........] - ETA: 1s - loss: 0.2913 - acc: 0.8792
5184/7200 [====================>.........] - ETA: 1s - loss: 0.2913 - acc: 0.8781
5312/7200 [=====================>........] - ETA: 1s - loss: 0.2905 - acc: 0.8784
5440/7200 [=====================>........] - ETA: 0s - loss: 0.2892 - acc: 0.8789
5568/7200 [======================>.......] - ETA: 0s - loss: 0.2903 - acc: 0.8779
5696/7200 [======================>.......] - ETA: 0s - loss: 0.2886 - acc: 0.8775
5824/7200 [=======================>......] - ETA: 0s - loss: 0.2896 - acc: 0.8774
5952/7200 [=======================>......] - ETA: 0s - loss: 0.2888 - acc: 0.8775
6080/7200 [========================>.....] - ETA: 0s - loss: 0.2887 - acc: 0.8786
6208/7200 [========================>.....] - ETA: 0s - loss: 0.2892 - acc: 0.8781
6336/7200 [=========================>....] - ETA: 0s - loss: 0.2901 - acc: 0.8782
6464/7200 [=========================>....] - ETA: 0s - loss: 0.2896 - acc: 0.8784
6592/7200 [==========================>...] - ETA: 0s - loss: 0.2903 - acc: 0.8782
6720/7200 [===========================>..] - ETA: 0s - loss: 0.2895 - acc: 0.8789
6784/7200 [===========================>..] - ETA: 0s - loss: 0.2896 - acc: 0.8784
6912/7200 [===========================>..] - ETA: 0s - loss: 0.2915 - acc: 0.8773
7040/7200 [============================>.] - ETA: 0s - loss: 0.2908 - acc: 0.8770
7168/7200 [============================>.] - ETA: 0s - loss: 0.2896 - acc: 0.8777
7200/7200 [==============================] - 4s 560us/step - loss: 0.2900 - acc: 0.8775 - val_loss: 0.2673 - val_acc: 0.8911

real	1m12.165s
user	3m30.772s
sys	0m4.319s

ငါဘာသွားတွေ့ရသလဲ ဆိုတော့ epoch က 100 ထိသွားစရာမလိုပဲ ရပ်သွားတာကို တွေ့ရ။

1st time training တုန်းက
7200/7200 [==============================] - 4s 515us/step - loss: 0.3297 - acc: 0.8583 - val_loss: 0.2858 - val_acc: 0.8761

အခု 2nd time training မှာက
7200/7200 [==============================] - 4s 560us/step - loss: 0.2900 - acc: 0.8775 - val_loss: 0.2673 - val_acc: 0.8911

ဆိုတော ... နည်းနည်းတက်လာတာတော့ တွေ့ရ

## Testing2

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ time python ./test-para1.py 
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

2020-12-16 05:15:12.007248: I tensorflow/core/platform/profile_utils/cpu_utils.cc:94] CPU Frequency: 2893330000 Hz
2020-12-16 05:15:12.007873: I tensorflow/compiler/xla/service/service.cc:168] XLA service 0x55babb34c420 initialized for platform Host (this does not guarantee that XLA will be used). Devices:
2020-12-16 05:15:12.007912: I tensorflow/compiler/xla/service/service.cc:176]   StreamExecutor device (0): Host, Default Version
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

10/10 [==============================] - 1s 66ms/step
[('ဝမ်းမြောက် ဝမ်းသာ ဖြစ် မိ ပါ သည်', 'ဝမ်းမြောက် ဝမ်းသာ ရှိ လှ ပေ စွ', 0.9992092), ('တော် တယ် ဆက် ပြီး တော့ ကြိုးစား ပါ', 'တော် တယ် ဆက် ကြိုးစား ပါ', 0.9992092), ('ဦးခိုက်ရှိခိုး ပါ ၏', 'ဦးခိုက် ပါ တယ်', 0.99920917), ('ဆရာတော် ကြီး များ သက်တော် ရာ ကျော် ရှည် ပါ စေ', 'ဆရာတော် ကြီး များ ကျန်းမာ သက် ရှည် ပါ စေ', 0.99920917), ('ကြိုက် သွား ပြီ', 'ကြိုဆို လိုက် ပါ', 0.99920917), ('စောက် လုပ် ကို ရှုပ် တယ်', 'စောက် လုပ် တွေ က ရှုပ် နေ တာ ပဲ', 0.99920917), ('သူ နဲ့ ကင်းကွာ နေ တာ ကြာ ပြီ', 'သူ နဲ့ အနီးဆုံး မှာ ပဲ နေ ပါ တယ်', 0.99920917), ('ထမင်း ကို ဖိတ်စင် အောင် မ စား ပါ နဲ့ ။', 'ရေ ကို ဖိတ်စင် အောင် မ ခပ် ပါ နဲ့ ။', 0.99920917), ('မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း များ သည် ဗွက် ဖြစ် နေ သည် ။', 'မိုး အလွန်အကျွံ ရွာ သောကြောင့် လမ်း မှာ ကောင်းကောင်း သွား မ ရ ပါ ။', 0.99920917), ('ရွဲ့လားစောင်းလား မ လုပ် နဲ့ နော်', 'စောင်း ပြော နေ တာ လား', 0.99920917)]

real	0m8.556s
user	0m8.612s
sys	0m0.872s
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$

## 20K နဲ့ training/validation လုပ်တော့ Error ပေး

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

## Checking fields

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

Ref: https://www.unix.com/shell-programming-and-scripting/172723-checking-csv-files-empty-fields.html

လိုင်းနံပါတ်က Zero က စထားတာမို့ ....

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ sed '$d' < ./2k.test.csv  > tmp.tst
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ mv tmp.tst ./2k.test.csv(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1$ tail ./2k.test.csv 
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

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ sed '$d' < ./line-no.para-no-para.shuf.final > tmp.tst
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ mv tmp.tst ./line-no.para-no-para.shuf.final


(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ sed '$d' < ./line-no.para-no-para.shuf.final.csv > tmp.tst
(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity/para-tst-1/original$ mv tmp.tst line-no.para-no-para.shuf.final.csv 


## Train again

(tensor1.15.4_keras2.2.4) ye@ykt-pro:/media/ye/project1/tool/lstm-siamese-text-similarity$ time python ./train-para1.py 2>&1 | tee ./para-tst-1/original/train-after-last-err-line-removed.log
....
...
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
user	4m9.061s
sys	0m4.584s
