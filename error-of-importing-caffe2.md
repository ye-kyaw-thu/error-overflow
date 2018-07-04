# Error of "from caffe2.python import core"

I installed caffe2 based on the instructions supported by the following link:  
(https://caffe2.ai/docs/getting-started.html?platform=ubuntu&configuration=compile)[https://caffe2.ai/docs/getting-started.html?platform=ubuntu&configuration=compile]  

## Installation steps in details

Installation for Dependencies:  

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
