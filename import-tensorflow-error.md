Python ကို run ပြီး၊ tensorflow ကို import လုပ်တော့ အောက်ပါအတိုင်း error ပေးတယ်။  

```bash
lar@lar-air:~/ss2018$ source activate py3.6.2
(py3.6.2) lar@lar-air:~/ss2018$ python
Python 3.6.2 |Continuum Analytics, Inc.| (default, Jul 20 2017, 13:51:32) 
[GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tensorflow
RuntimeError: module compiled against API version 0xc but this version of numpy is 0xb
ImportError: numpy.core.multiarray failed to import
ImportError: numpy.core.umath failed to import
ImportError: numpy.core.umath failed to import
2018-06-08 09:14:00.458580: F tensorflow/python/lib/core/bfloat16.cc:664] Check failed: PyBfloat16_Type.tp_base != nullptr 
Aborted (core dumped)
```
ပြဿနာက numpy version ကြောင့်ဆိုတာကို သိလို့၊ numpy ကို ပြန် install လုပ်ခဲ့တယ်။  

```bash
(py3.6.2) lar@lar-air:~/ss2018$ pip install numpy
Requirement already satisfied: numpy in /home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages (1.14.0)
(py3.6.2) lar@lar-air:~/ss2018$ pip install numpy --upgrade
Collecting numpy
  Downloading https://files.pythonhosted.org/packages/4b/3d/9c0a34ad8544abef864714840fb8954d630b04433f00881bc8fde7b2ab27/numpy-1.14.4-cp36-cp36m-manylinux1_x86_64.whl (12.2MB)
    100% |████████████████████████████████| 12.2MB 2.0MB/s 
Installing collected packages: numpy
  Found existing installation: numpy 1.14.0
    Uninstalling numpy-1.14.0:
      Successfully uninstalled numpy-1.14.0
Successfully installed numpy-1.14.4
```
numpy ကို install လုပ်ပြီးတော့ import numpy, import tensorflow လုပ်တော့
အောက်ပါအတိုင်း အိုကေသွားတယ်။  

```bash
(py3.6.2) lar@lar-air:~/ss2018$ python
Python 3.6.2 |Continuum Analytics, Inc.| (default, Jul 20 2017, 13:51:32) 
[GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy as np
>>> import tensorflow as tf
/home/lar/anaconda3/envs/py3.6.2/lib/python3.6/site-packages/h5py/__init__.py:36: FutureWarning: Conversion of the second argument of issubdtype from `float` to `np.floating` is deprecated. In future, it will be treated as `np.float64 == np.dtype(float).type`.
  from ._conv import register_converters as _register_converters
>>> 
```
