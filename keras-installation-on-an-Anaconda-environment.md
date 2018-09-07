
keras.datasets က လက်ရှိသုံးနေတဲ့ notebook မှာ မရှိသေးလို့ import လုပ်လို့မရ

(py3.6.5) lar@lar-air:~/experiment/cnn/exe1$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import keras
>>> import keras.datasets
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'keras.datasets'
>>> exit()

==========

အဲဒါကြောင့် pip နဲ့ keras.datasets ကို install လုပ်ပြီး
import လုပ်ကြည့်လဲ အောက်ပါအတိုင်း error message ရခဲ့။

(py3.6.5) lar@lar-air:~/experiment/cnn/exe1$ pip install keras.datasets
Collecting keras.datasets
  Downloading https://files.pythonhosted.org/packages/07/20/9ed10cd3247cc29c362c77c52d820928ab4f955b7e1ba9e77a288b4c5f3c/keras_datasets-0.1.0-py2.py3-none-any.whl
Installing collected packages: keras.datasets
Successfully installed keras.datasets

(py3.6.5) lar@lar-air:~/experiment/cnn/exe1$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import keras.datasets
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'keras.datasets'
>>> import keras
>>> import keras.datasets
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'keras.datasets'
>>> from keras.datasets import mnist
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'keras.datasets'

==========

အဲဒါကြောင့် conda ကိုသုံးပြီး အောက်ပါအတိုင်း install လုပ်ခဲ့

(py3.6.5) lar@lar-air:~/experiment/cnn/exe1$ conda install keras
Fetching package metadata ...........
Solving package specifications: .

Package plan for installation in environment /home/lar/anaconda3/envs/py3.6.5:

The following NEW packages will be INSTALLED:

    h5py:                2.8.0-py36h470a237_0                  conda-forge
    keras:               2.2.2-py36_0                          conda-forge
    keras-applications:  1.0.4-py_1                            conda-forge
    keras-preprocessing: 1.0.2-py_1                            conda-forge
    libgcc-ng:           7.2.0-hdf63c60_3                      conda-forge
    mkl:                 2017.0.3-0                                       
    pygpu:               0.7.6-py36_0                          conda-forge
    scipy:               0.19.1-np113py36_0                               
    theano:              1.0.2-py36_0                          conda-forge

The following packages will be DOWNGRADED:

    blas:                1.1-openblas                          conda-forge --> 1.0-mkl      
    numpy:               1.14.5-py36_blas_openblash24bf2e0_200 conda-forge [blas_openblas] --> 1.13.1-py36_0

Proceed ([y]/n)? y

blas-1.0-mkl.t 100% |#######################################################################################################| Time: 0:00:00   1.87 MB/s
libgcc-ng-7.2. 100% |#######################################################################################################| Time: 0:00:20 318.20 kB/s
mkl-2017.0.3-0 100% |#######################################################################################################| Time: 0:06:54 327.57 kB/s
numpy-1.13.1-p 100% |#######################################################################################################| Time: 0:00:23 328.83 kB/s
h5py-2.8.0-py3 100% |#######################################################################################################| Time: 0:00:12 305.91 kB/s
scipy-0.19.1-n 100% |#######################################################################################################| Time: 0:01:53 336.58 kB/s
keras-applicat 100% |#######################################################################################################| Time: 0:00:01  15.33 kB/s
keras-2.2.2-py 100% |#######################################################################################################| Time: 0:00:05  77.69 kB/s
keras-preproce 100% |#######################################################################################################| Time: 0:00:00   6.30 MB/s

CondaError: OSError(28, 'No space left on device')
CondaError: OSError(28, 'No space left on device')
CondaError: OSError(28, 'No space left on device')

အထက်ပါ Error က notebook မှာ disk space မရှိတော့လို့ပေးတာ။
အဲဒါကြောင့် disk space ကို clean လုပ်ပြီးတော့
အောက်ပါအတိုင်း keras ကို ပြန် install လုပ်ခဲ့

(py3.6.5) lar@lar-air:~/experiment/cnn/exe1$ conda install keras
Fetching package metadata ...........
Solving package specifications: .

Package plan for installation in environment /home/lar/anaconda3/envs/py3.6.5:

The following NEW packages will be INSTALLED:

    h5py:                2.8.0-py36h470a237_0                  conda-forge
    keras:               2.2.2-py36_0                          conda-forge
    keras-applications:  1.0.4-py_1                            conda-forge
    keras-preprocessing: 1.0.2-py_1                            conda-forge
    libgcc-ng:           7.2.0-hdf63c60_3                      conda-forge
    mkl:                 2017.0.3-0                                       
    pygpu:               0.7.6-py36_0                          conda-forge
    scipy:               0.19.1-np113py36_0                               
    theano:              1.0.2-py36_0                          conda-forge

The following packages will be DOWNGRADED:

    blas:                1.1-openblas                          conda-forge --> 1.0-mkl      
    numpy:               1.14.5-py36_blas_openblash24bf2e0_200 conda-forge [blas_openblas] --> 1.13.1-py36_0

Proceed ([y]/n)? y

Installation ပြီးတဲ့အခါမှာတော့ import လုပ်လို့ ရသွားပါတယ်။

(py3.6.5) lar@lar-air:~/experiment/cnn/exe1$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import keras
Using TensorFlow backend.
>>> from keras.datasets import mnist
>>> 
