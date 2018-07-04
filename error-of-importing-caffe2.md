# Error of "from caffe2.python import core"

I installed caffe2 based on the instructions supported by the following link:  
(https://caffe2.ai/docs/getting-started.html?platform=ubuntu&configuration=compile)[https://caffe2.ai/docs/getting-started.html?platform=ubuntu&configuration=compile]  

## Installation steps in details

Installation for dependencies:  

```
$ sudo apt-get update
$ sudo apt-get install -y --no-install-recommends \
      build-essential \
      cmake \
      git \
      libgoogle-glog-dev \
      libgtest-dev \
      libiomp-dev \
      libleveldb-dev \
      liblmdb-dev \
      libopencv-dev \
      libopenmpi-dev \
      libsnappy-dev \
      libprotobuf-dev \
      openmpi-bin \
      openmpi-doc \
      protobuf-compiler \
      python-dev \
      python-pip                          
$ sudo pip install \
      future \
      numpy \
      protobuf
      
$ sudo apt-get install -y --no-install-recommends libgflags-dev
```

Clone source code of Caffe2 from Github repository:  

```
$ git clone --recursive https://github.com/pytorch/pytorch.git && cd pytorch
$ git submodule update --init
```

Building, configuring, Compiling:  

```
$ mkdir build && cd build

$ cmake ..

$ sudo make install
```
Testing Caffe2 installation:  

```
cd ~ && python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"
```

# Problem:  

I failed the final testing step of Caffe2 installation:  

```
$ python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"
Failure
```

# How to solve:  

The followings are the log of how I solved:  

```
# Make confirmation of import error:

(py3.6.5) lar@lar-air:~$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from caffe2.python import core
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'caffe2'
>>> 

# ==============

# Check python and pip are in the same place or not:

(py3.6.5) lar@lar-air:~$ which python
/home/lar/anaconda3/envs/py3.6.5/bin/python
(py3.6.5) lar@lar-air:~$ which pip
/home/lar/anaconda3/envs/py3.6.5/bin/pip

# ==============

# Exporting PYTHONPATH

(py3.6.5) lar@lar-air:~$ export PYTHONPATH="${PYTHONPATH}:$(which python)/../.."

(py3.6.5) lar@lar-air:~$ cd ~ && python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"
Failure

==============

# After I updated $PYTHONPATH as follows:

(py3.6.5) lar@lar-air:~$ export PYTHONPATH=/usr/local/lib/python3.6/site-packages:$PYTHONPATH

# Now I can import caffe2 but ...

lar@lar-air:/usr/local/lib/python3.6/site-packages$ source activate py3.6.5

(py3.6.5) lar@lar-air:/usr/local/lib/python3.6/site-packages$ echo $PYTHONPATH 
/usr/local/lib/python3.6/site-packages:/home/lar/anaconda3/bin/python

(py3.6.5) lar@lar-air:/usr/local/lib/python3.6/site-packages$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import caffe2
>>> exit()

# Still got "Failure"

(py3.6.5) lar@lar-air:/usr/local/lib/python3.6/site-packages$ python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"
Failure

# =============

# I can also "import caffe2.python" but ...

(py3.6.5) lar@lar-air:~$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from caffe2.python import core
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/lib/python3.6/site-packages/caffe2/python/core.py", line 9, in <module>
    from past.builtins import basestring
ModuleNotFoundError: No module named 'past'
>>> 

# ===============

(py3.6.5) lar@lar-air:~$ pip install past
Collecting past
  Could not find a version that satisfies the requirement past (from versions: )
No matching distribution found for past

# ===============

(py3.6.5) lar@lar-air:~$ pip install future
Collecting future
  Downloading https://files.pythonhosted.org/packages/00/2b/8d082ddfed935f3608cc61140df6dcbf0edea1bc3ab52fb6c29ae3e81e85/future-0.16.0.tar.gz (824kB)
    100% |████████████████████████████████| 829kB 256kB/s 
Building wheels for collected packages: future
  Running setup.py bdist_wheel for future ... done
  Stored in directory: /home/lar/.cache/pip/wheels/bf/c9/a3/c538d90ef17cf7823fa51fc701a7a7a910a80f6a405bf15b1a
Successfully built future
Installing collected packages: future
Successfully installed future-0.16.0

# And then tried again ...

(py3.6.5) lar@lar-air:~$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from caffe2.python import core
WARNING:root:This caffe2 python run does not have GPU support. Will run in CPU only mode.
WARNING:root:Debug message: No module named 'caffe2.python.caffe2_pybind11_state_hip'
CRITICAL:root:Cannot load caffe2.python. Error: libcaffe2.so: cannot open shared object file: No such file or directory

# ===========

(py3.6.5) lar@lar-air:~$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from caffe2.python import *
>>> 

# Above is OK! WHY "from caffe2.python import core" is not OK???

===========

# Check $LD_LIBRARY_PATH

(py3.6.5) lar@lar-air:~$ echo $LD_LIBRARY_PATH 
:/lib:/lib64:/usr/lib:/usr/lib64:/lib:/lib64:/usr/lib:/usr/lib64

# ============

lar@lar-air:~/tool/pytorch/build/lib$ source ~/.bashrc

# I updated the LD_LIBRARY_PATH to include caffe2 build directory:
# For my case: /home/lar/tool/pytorch/build/lib
# export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/lib:/lib64:/usr/lib:/usr/lib64:/home/lar/tool/pytorch/build/lib

lar@lar-air:~/tool/pytorch/build/lib$ echo $LD_LIBRARY_PATH 
:/lib:/lib64:/usr/lib:/usr/lib64:/lib:/lib64:/usr/lib:/usr/lib64:/lib:/lib64:/usr/lib:/usr/lib64:/home/lar/tool/pytorch/build/lib
lar@lar-air:~/tool/pytorch/build/lib$ source activate py3.6.5
(py3.6.5) lar@lar-air:~/tool/pytorch/build/lib$ python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"
Success

# Confirmation again:

(py3.6.5) lar@lar-air:~/tool/pytorch/build/lib$ python
Python 3.6.5 | packaged by conda-forge | (default, Apr  6 2018, 13:39:56) 
[GCC 4.8.2 20140120 (Red Hat 4.8.2-15)] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from caffe2.python import core
WARNING:root:This caffe2 python run does not have GPU support. Will run in CPU only mode.
WARNING:root:Debug message: No module named 'caffe2.python.caffe2_pybind11_state_hip'
>>> 

```

What I learned from this installation:
