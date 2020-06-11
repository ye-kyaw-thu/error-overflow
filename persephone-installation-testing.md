# Persephone Installation, Errors and Testing Note

## Create New Conda Environment

```
(base) ye@ykt-pro:~/exp/persephone$ conda create --name persephone python=3
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 4.8.3

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/persephone

  added / updated specs:
    - python=3


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2020.4.5.1         |           py38_0         156 KB
    pip-20.0.2                 |           py38_3         1.7 MB
    python-3.8.3               |       hcff3b4d_0        49.1 MB
    setuptools-46.4.0          |           py38_0         515 KB
    wheel-0.34.2               |           py38_0          51 KB
    ------------------------------------------------------------
                                           Total:        51.5 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  ca-certificates    pkgs/main/linux-64::ca-certificates-2020.1.1-0
  certifi            pkgs/main/linux-64::certifi-2020.4.5.1-py38_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.33.1-h53a641e_7
  libedit            pkgs/main/linux-64::libedit-3.1.20181209-hc058e9b_0
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_1
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  openssl            pkgs/main/linux-64::openssl-1.1.1g-h7b6447c_0
  pip                pkgs/main/linux-64::pip-20.0.2-py38_3
  python             pkgs/main/linux-64::python-3.8.3-hcff3b4d_0
  readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
  setuptools         pkgs/main/linux-64::setuptools-46.4.0-py38_0
  sqlite             pkgs/main/linux-64::sqlite-3.31.1-h62c20be_1
  tk                 pkgs/main/linux-64::tk-8.6.8-hbc83047_0
  wheel              pkgs/main/linux-64::wheel-0.34.2-py38_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y


Downloading and Extracting Packages
certifi-2020.4.5.1   | 156 KB    | ######################################################## | 100% 
python-3.8.3         | 49.1 MB   | ######################################################## | 100% 
wheel-0.34.2         | 51 KB     | ######################################################## | 100% 
setuptools-46.4.0    | 515 KB    | ######################################################## | 100% 
pip-20.0.2           | 1.7 MB    | ######################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate persephone
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

## Activate the Environment

```
(base) ye@ykt-pro:~/exp/persephone$ conda activate persephone
(persephone) ye@ykt-pro:~/exp/persephone$
```

## Install persephone

I got tensorflow version not match error.

```
(persephone) ye@ykt-pro:~/exp/persephone$ pip install persephone
Collecting persephone
  Downloading persephone-0.4.2-py3-none-any.whl (66 kB)
     |████████████████████████████████| 66 kB 448 kB/s 
Collecting numpy<2,>=1.14.5
  Downloading numpy-1.18.4-cp38-cp38-manylinux1_x86_64.whl (20.7 MB)
     |████████████████████████████████| 20.7 MB 490 kB/s 
Collecting pint==0.9
  Downloading Pint-0.9-py2.py3-none-any.whl (138 kB)
     |████████████████████████████████| 138 kB 636 kB/s 
Collecting pympi-ling==1.69
  Downloading pympi-ling-1.69.tar.gz (29 kB)
Collecting nltk==3.4.5
  Downloading nltk-3.4.5.zip (1.5 MB)
     |████████████████████████████████| 1.5 MB 334 kB/s 
Collecting python-speech-features==0.6
  Downloading python_speech_features-0.6.tar.gz (5.6 kB)
Collecting pydub==0.20.0
  Downloading pydub-0.20.0-py2.py3-none-any.whl (25 kB)
Collecting scipy<2,>=1.1.0
  Downloading scipy-1.4.1-cp38-cp38-manylinux1_x86_64.whl (26.0 MB)
     |████████████████████████████████| 26.0 MB 448 kB/s 
ERROR: Could not find a version that satisfies the requirement tensorflow<2,>=1.13.1 (from persephone) (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow<2,>=1.13.1 (from persephone)
(persephone) ye@ykt-pro:~/exp/persephone$ pip install tensorflow=1.15
ERROR: Invalid requirement: 'tensorflow=1.15'
Hint: = is not a valid operator. Did you mean == ?
(persephone) ye@ykt-pro:~/exp/persephone$ pip install tensorflow==1.15
ERROR: Could not find a version that satisfies the requirement tensorflow==1.15 (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow==1.15
(persephone) ye@ykt-pro:~/exp/persephone$ pip install --ignore-installed --upgrade tensorflow==1.14ERROR: Could not find a version that satisfies the requirement tensorflow==1.14 (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow==1.14
(persephone) ye@ykt-pro:~/exp/persephone$ python -m pip install --upgrade pip
Collecting pip
  Downloading pip-20.1.1-py2.py3-none-any.whl (1.5 MB)
     |████████████████████████████████| 1.5 MB 463 kB/s 
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 20.0.2
    Uninstalling pip-20.0.2:
      Successfully uninstalled pip-20.0.2
Successfully installed pip-20.1.1
```

I got following error:  
ERROR: No matching distribution found for tensorflow<2,>=1.13.1 (from persephone)  

And thus, I tried several versions of tensorflow installation ...  

## Try to upgrade tensorflow version 1.15

```
(persephone) ye@ykt-pro:~/exp/persephone$ pip install --ignore-installed --upgrade tensorflow==1.15
ERROR: Could not find a version that satisfies the requirement tensorflow==1.15 (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow==1.15
```

## I tried several times again

```
(persephone) ye@ykt-pro:~/exp/persephone$ python3 -m pip install tensorflow==1.15.0
ERROR: Could not find a version that satisfies the requirement tensorflow==1.15.0 (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow==1.15.0
```

```
(persephone) ye@ykt-pro:~/exp/persephone$ python3 -m pip install tensorflow==1.14.0
ERROR: Could not find a version that satisfies the requirement tensorflow==1.14.0 (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow==1.14.0
```

## Check available tensorflow versions

```
(persephone) ye@ykt-pro:~/exp/persephone$ python -m pip search tensorflow
tensorflow (2.2.0)                                - TensorFlow is an open source machine learning
                                                    framework for everyone.
tensorflow-qndex (0.0.22)                         - tensorflow-qnd x tensorflow-extenteten
tensorflow-plot (0.3.2)                           - TensorFlow Plot
tensorflow-addons (0.10.0)                        - TensorFlow Addons.
tensorflow-estimator (2.2.0)                      - TensorFlow Estimator.
mesh-tensorflow (0.1.13)                          - Mesh TensorFlow
tensorflow-io (0.13.0)                            - TensorFlow IO
tensorflow-ops (0.0.0)                            - tensorflow-ops
tensorflow-datasets (3.1.0)                       - tensorflow/datasets is a library of datasets
                                                    ready to use with TensorFlow.
tensorflow-scientific (0.2.0.dev0)                - Scientific modeling in TensorFlow
emloop-tensorflow (0.6.0)                         - TensorFlow extension for emloop.
tensorflow-k8s (0.0.2)                            - Tensorflow serving extension
daltons-tensorflow (0.0.13)                       - Daltons Tensorflow bindings
cxflow-tensorflow (0.5.0)                         - TensorFlow extension for cxflow.
tensorflow-extenteten (0.0.22)                    - TensorFlow extention library
tensorflow-compression (1.3)                      - Data compression in TensorFlow
Tensorflow-ChatBots (0.0.12)                      - ChatBots supporting TensorFlow
syft-tensorflow (0.1.0)                           - TensorFlow Bindings for PySyft
dask-tensorflow (0.0.2)                           - Interactions between Dask and Tensorflow
tensorflow-tracer (1.1.0)                         - Runtime Tracing Library for TensorFlow
tensorflow-radam (0.15.0)                         - RAdam implemented in Keras & TensorFlow
gmlsnets-tensorflow (0.1)                         - GMLS-Nets Tensorflow implementation
tensorflow-transform (0.22.0)                     - A library for data preprocessing with
                                                    TensorFlow
tensorflow-qnd (0.1.11)                           - Quick and Dirty TensorFlow command framework
tensorflow-probability (0.10.0)                   - Probabilistic modeling and statistical
                                                    inference in TensorFlow
sagemaker-tensorflow (2.2.0.1.0.0)                - Amazon Sagemaker specific TensorFlow
                                                    extensions.
tensorflow-model (0.1.1)                          - Command-line tool to inspect TensorFlow
                                                    models
tensorflow-determinism (0.3.0)                    - Tracking, debugging, and patching non-
                                                    determinism in TensorFlow
tensorflow-utils (0.1.0)                          - Classes and methods to make using TensorFlow
                                                    easier
tensorflow-ranking (0.3.0)                        - Pip package setup file for TensorFlow
                                                    Ranking.
tensorflow-cpu-estimator (1.15.1)                 - TensorFlow Estimator.
tensorflow-io-nightly (0.13.0.dev20200529035009)  - TensorFlow IO
tensorflow-gpu-estimator (2.2.0)                  - TensorFlow Estimator.
tensorflow-lattice-gpu (0.9.8)                    - TensorFlow Lattice provides lattice models in
                                                    TensorFlow
tensorflow-tflex (1.13.1rc3)                      - TensorFlow is an open source machine learning
                                                    framework for everyone.
tensorflow-aarch64 (1.2)                          - Tensorflow r1.2 for aarch64[arm64,pine64] CPU
                                                    only.
tensorflow-gan (2.0.0)                            - TF-GAN: A Generative Adversarial Networks
                                                    library for TensorFlow.
tensorflow-fedora28 (1.9.0rc0)                    - TensorFlow is an open source machine learning
                                                    framework for everyone.
tensorflow-federated (0.14.0)                     - TensorFlow Federated is an open-source
                                                    federated learning framework.
tensorflow-rl (0.2.2)                             - tensorflow-rl: Modular Deep Reinforcement
                                                    Learning Framework.
tensorflow-gpu (2.2.0)                            - TensorFlow is an open source machine learning
                                                    framework for everyone.
tensorflow-cpu (2.2.0)                            - TensorFlow is an open source machine learning
                                                    framework for everyone.
intel-tensorflow (2.1.0)                          - TensorFlow is an open source machine learning
                                                    framework for everyone.
tensorflow-font2char2word2sent2doc (0.0.12)       - TensorFlow implementation of Hierarchical
                                                    Attention Networks for Document
                                                    Classification
tensorflow-template (0.2)                         - A tensorflow template for quick starting a
                                                    deep learning project.
tensorflow-rocm (2.1.1)                           - TensorFlow is an open source machine learning
                                                    framework for everyone.
essentia-tensorflow (2.1b6.dev236)                - Library for audio and music analysis,
                                                    description and synthesis, with TensorFlow
                                                    support
tensorflow-quantum (0.3.0)                        - TensorFlow Quantum is a library for hybrid
                                                    quantum-classical machine learning.
tensorflow-encrypted (0.4.0)                      - Layer on top of TensorFlow for doing machine
                                                    learning on encrypted data.
tensorflow-text (2.2.0)                           - TF.Text is a TensorFlow library of text
                                                    related ops, modules, and subgraphs.
silence-tensorflow (1.1.1)                        - Simple python package to shut up Tensorflow
                                                    warnings and logs.
tensorflow-transform-canary (0.9.0)               - A library for data preprocessing with
                                                    TensorFlow
tensorflow-serving-client (1.0.0)                 - Python client for tensorflow serving
rav-tensorflow-transform (0.7.0.910)              - A library for data preprocessing with
                                                    TensorFlow
tensorflow-serving-api (2.1.0)                    - TensorFlow Serving Python API.
tensorflow-model-analysis (0.22.1)                - A library for analyzing TensorFlow models
tensorflow-onmttok-ops (0.3.0)                    - OpenNMT Tokenizer as TensorFlow Operations
tensorflow-play (0.0.1)                           - The lightweight engineering TensorFlow
                                                    wrapper for AI engineer. Write less, Reuse
                                                    more, Scale easily.
tensorflow-hub (0.8.0)                            - TensorFlow Hub is a library to foster the
                                                    publication, discovery, and consumption of
                                                    reusable parts of machine learning models.
tensorflow-kernels (0.1.2)                        - A package with Tensorflow (both CPU and GPU)
                                                    implementation of most popular Kernels for
                                                    kernels methods (SVM, MKL...).
tensorflow-graphics (2020.5.20)                   - A library that contains well defined,
                                                    reusable and cleanly written graphics related
                                                    ops and utility functions for TensorFlow.
tensorflow-io-2.0-preview (0.7.0.dev1369)         - TensorFlow IO
tensorflow-estimator-2.0-preview (2.0.0)          - TensorFlow Estimator.
tensorflow-constrained-optimization (0.2)         - A library for performing constrained
                                                    optimization in TensorFlow
ngraph-tensorflow-bridge (0.18.0)                 - Intel nGraph compiler and runtime for
                                                    TensorFlow
tensorflow-rocm-enhanced (0.0.1)                  - TensorFlow is an open source machine learning
                                                    framework for everyone.
simple-tensorflow-serving (0.8.1.1)               - The simpler and easy-to-use serving service
                                                    for TensorFlow models
Tensorflow-Telegram-Bot (0.0.2)                   - TensorFlow Telegram Bot which can be used as
                                                    callback
tensorflow-serving-client-grpc (2.1.0)            - A prebuilt tensorflow serving client from the
                                                    tensorflow serving proto files
neuraxle-tensorflow (0.1.1)                       - TensorFlow steps, savers, and utilities for
                                                    Neuraxle. Neuraxle is a Machine Learning (ML)
                                                    library for building neat pipelines,
                                                    providing the right abstractions to both ease
                                                    research, development, and deployment of your
                                                    ML applications.
tensorflow-enterprise-addons (0.0.0)              - Client-side library suites of TensorFlow
                                                    Enteprise on Google Cloud Platform (GCP),
                                                    which implements a special integration with
                                                    GCP behind the TensorFlow APIs.
tensorflow-serving-api-gpu (2.1.0)                - TensorFlow Serving Python API.
spark-tensorflow-distributor (0.0.3)              - This package helps users do distributed
                                                    training with TensorFlow on their Spark
                                                    clusters.
tensorflow-auto-detect (1.11.0)                   - Automatically install CPU or GPU tensorflow
                                                    determined by looking for a CUDA
                                                    installation.
tensorflow-gcs-config (2.1.8)                     - TensorFlow operations for configuring access
                                                    to GCS (Google Compute Storage) resources.
sagemaker-tensorflow-training (20.0.0.post0)      - Open source library for creating TensorFlow
                                                    containers to run on Amazon SageMaker.
tensorflow-object-detection-api (0.1.1)           - Tensorflow Object Detection Library Packaged
tensorflow-serving-api-python3 (1.8.0)            - *UNOFFICIAL* TensorFlow Serving API libraries
                                                    for Python3
tensorflow-graphics-gpu (1.0.0)                   - A library that contains well defined,
                                                    reusable and cleanly written graphics related
                                                    ops and utility functions for TensorFlow.
tensorflow-exercise-hx (1.0.1)                    - tensorflow&#32451;&#20064;&#65306;&#40482;&#2
                                                    3614;&#33457;&#31181;&#31867;&#39044;&#27979;
                                                    &#65292;&#21152;&#24030;&#25151;&#20215;&#390
                                                    44;&#27979;
mlops-tensorflow (0.1.0)                          - 
tensorflow-privacy (0.3.0)                        - 
bert-tensorflow (1.0.1)                           - BERT
tensorflow-tensorboard (1.5.1)                    - TensorBoard lets you watch Tensors Flow
resnet-tensorflow (0.0.1)                         - Deep Residual Neural Network
albert-tensorflow (1.1)                           - ALBERT fork of https://github.com/google-
                                                    research/google-research/tree/master/albert
                                                    with package configuration
tensorflow-cloud (0.1.2)                          - 
tensorflow-metadata (0.22.1)                      - Library and standards for schema and
                                                    statistics.
tensorflow-lattice (2.0.4)                        - A library that implements optionally
                                                    monotonic lattice based models.
xlnet-tensorflow (1.1.2)                          - XLNet fork of
                                                    https://github.com/zihangdai/xlnet with
                                                    package configuration
xl-tensorflow (0.4.3)                             - my tensorflow2.1 Model and useful function
dbnd-tensorflow (0.27.2)                          - Machine Learning Orchestration
tensorflow-gpu-macosx (1.8.1)                     - Unoffcial NVIDIA CUDA GPU support version of
                                                    Google Tensorflow for MAC OSX 10.13. For more
                                                    info, please check out my github page. I
                                                    highly recommend you directly download and
                                                    install it from my github's release. If you
                                                    insist on compiling it, you'd do it on a
                                                    shell to debug.
tensorflow-data-validation (0.22.0)               - A library for exploring and validating
                                                    machine learning data.
tensorflow-model-optimization (0.3.0)             - A suite of tools that users, both novice and
                                                    advanced can use to optimize machine learning
                                                    models for deployment and execution.
dffml-model-tensorflow (0.2.7)                    - 
syntaxnet-with-tensorflow (0.2)                   - SyntaxNet: Neural Models of Syntax
dffml-model-tensorflow-hub (0.0.5)                - 
tensorflow-cpu-2.0-preview (0.0.0)                - 
PSCMRCET-Tensorflow-object-trainer (1.3.0)        - Custom Object training system can be done by
                                                    using single command line
(persephone) ye@ykt-pro:~/exp/persephone$
```

## Tensorflow Installation Success for 1.13.1

```
(persephone) ye@ykt-pro:~/exp/persephone$ pip2 install 'tensorflow==1.13.1' --force-reinstall
Collecting tensorflow==1.13.1
  Cache entry deserialization failed, entry ignored
  Downloading https://files.pythonhosted.org/packages/d2/ea/ab2c8c0e81bd051cc1180b104c75a865ab0fc66c89be992c4b20bbf6d624/tensorflow-1.13.1-cp27-cp27mu-manylinux1_x86_64.whl (92.5MB)
    100% |████████████████████████████████| 92.5MB 9.9kB/s 
Collecting tensorflow-estimator<1.14.0rc0,>=1.13.0 (from tensorflow==1.13.1)
  Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProtocolError('Connection aborted.', error(104, 'Connection reset by peer'))': /simple/tensorflow-estimator/
  Downloading https://files.pythonhosted.org/packages/bb/48/13f49fc3fa0fdf916aa1419013bb8f2ad09674c275b4046d5ee669a46873/tensorflow_estimator-1.13.0-py2.py3-none-any.whl (367kB)
    100% |████████████████████████████████| 368kB 439kB/s 
Collecting grpcio>=1.8.6 (from tensorflow==1.13.1)
  Downloading https://files.pythonhosted.org/packages/f1/23/62d3e82fa4c505f3195315c8a774b2e656b556d174329aa98edb829e48bc/grpcio-1.29.0.tar.gz (19.6MB)
    100% |████████████████████████████████| 19.6MB 36kB/s 
Collecting mock>=2.0.0 (from tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/05/d2/f94e68be6b17f46d2c353564da56e6fb89ef09faeeff3313a046cb810ca9/mock-3.0.5-py2.py3-none-any.whl
Collecting keras-applications>=1.0.6 (from tensorflow==1.13.1)
Collecting enum34>=1.1.6 (from tensorflow==1.13.1)
  Downloading https://files.pythonhosted.org/packages/6f/2c/a9386903ece2ea85e9807e0e062174dc26fdce8b05f216d00491be29fad5/enum34-1.1.10-py2-none-any.whl
Collecting protobuf>=3.6.1 (from tensorflow==1.13.1)
  Downloading https://files.pythonhosted.org/packages/6a/b0/ff5e323618006596743060ad48103853b0351cc79f1b84d7f4b247db1149/protobuf-3.12.2-cp27-cp27mu-manylinux1_x86_64.whl (1.3MB)
    100% |████████████████████████████████| 1.3MB 199kB/s 
Collecting keras-preprocessing>=1.0.5 (from tensorflow==1.13.1)
  Downloading https://files.pythonhosted.org/packages/79/4c/7c3275a01e12ef9368a892926ab932b33bb13d55794881e3573482b378a7/Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42kB)
    100% |████████████████████████████████| 51kB 332kB/s 
Collecting gast>=0.2.0 (from tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/d6/84/759f5dd23fec8ba71952d97bcc7e2c9d7d63bdc582421f3cd4be845f0c98/gast-0.3.3-py2.py3-none-any.whl
Collecting tensorboard<1.14.0,>=1.13.0 (from tensorflow==1.13.1)
  Downloading https://files.pythonhosted.org/packages/89/ac/48dd71c2bdc8d31e367f9b72f25ccb3b89bc6b9d664fee21f9a8efa5714d/tensorboard-1.13.1-py2-none-any.whl (3.2MB)
    100% |████████████████████████████████| 3.2MB 134kB/s 
Collecting wheel (from tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/8c/23/848298cccf8e40f5bbb59009b32848a4c38f4e7f3364297ab3c3e2e2cd14/wheel-0.34.2-py2.py3-none-any.whl
Collecting absl-py>=0.1.6 (from tensorflow==1.13.1)
Collecting backports.weakref>=1.0rc1 (from tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/88/ec/f598b633c3d5ffe267aaada57d961c94fdfa183c5c3ebda2b6d151943db6/backports.weakref-1.0.post1-py2.py3-none-any.whl
Collecting six>=1.10.0 (from tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/ee/ff/48bde5c0f013094d729fe4b0316ba2a24774b3ff1c52d924a8a4cb04078a/six-1.15.0-py2.py3-none-any.whl
Collecting numpy>=1.13.3 (from tensorflow==1.13.1)
  Cache entry deserialization failed, entry ignored
  Using cached https://files.pythonhosted.org/packages/3a/5f/47e578b3ae79e2624e205445ab77a1848acdaa2929a00eeef6b16eaaeb20/numpy-1.16.6-cp27-cp27mu-manylinux1_x86_64.whl
Collecting termcolor>=1.1.0 (from tensorflow==1.13.1)
Collecting astor>=0.6.0 (from tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/c3/88/97eef84f48fa04fbd6750e62dcceafba6c63c81b7ac1420856c8dcc0a3f9/astor-0.8.1-py2.py3-none-any.whl
Collecting futures>=2.2.0 (from grpcio>=1.8.6->tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/d8/a6/f46ae3f1da0cd4361c344888f59ec2f5785e69c872e175a748ef6071cdb5/futures-3.3.0-py2-none-any.whl
Collecting funcsigs>=1; python_version < "3.3" (from mock>=2.0.0->tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/69/cb/f5be453359271714c01b9bd06126eaf2e368f1fddfff30818754b5ac2328/funcsigs-1.0.2-py2.py3-none-any.whl
Collecting h5py (from keras-applications>=1.0.6->tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/12/90/3216b8f6d69905a320352a9ca6802a8e39fdb1cd93133c3d4163db8d5f19/h5py-2.10.0-cp27-cp27mu-manylinux1_x86_64.whl
Collecting setuptools (from protobuf>=3.6.1->tensorflow==1.13.1)
  Downloading https://files.pythonhosted.org/packages/e1/b7/182161210a13158cd3ccc41ee19aadef54496b74f2817cc147006ec932b4/setuptools-44.1.1-py2.py3-none-any.whl (583kB)
    100% |████████████████████████████████| 583kB 140kB/s 
Collecting werkzeug>=0.11.15 (from tensorboard<1.14.0,>=1.13.0->tensorflow==1.13.1)
  Downloading https://files.pythonhosted.org/packages/cc/94/5f7079a0e00bd6863ef8f1da638721e9da21e5bacee597595b318f71d62e/Werkzeug-1.0.1-py2.py3-none-any.whl (298kB)
    100% |████████████████████████████████| 307kB 144kB/s 
Collecting markdown>=2.6.8 (from tensorboard<1.14.0,>=1.13.0->tensorflow==1.13.1)
  Using cached https://files.pythonhosted.org/packages/c0/4e/fd492e91abdc2d2fcb70ef453064d980688762079397f779758e055f6575/Markdown-3.1.1-py2.py3-none-any.whl
Building wheels for collected packages: grpcio
  Running setup.py bdist_wheel for grpcio ... done
  Stored in directory: /home/ye/.cache/pip/wheels/ed/06/79/e559ab3b10134903b88e2df2df1b7cc4d3f1a92a46972a09fb
Successfully built grpcio
Installing collected packages: six, funcsigs, mock, enum34, absl-py, numpy, tensorflow-estimator, futures, grpcio, h5py, keras-applications, setuptools, protobuf, keras-preprocessing, gast, werkzeug, wheel, markdown, tensorboard, backports.weakref, termcolor, astor, tensorflow
Successfully installed absl-py-0.9.0 astor-0.8.1 backports.weakref-1.0.post1 enum34-1.1.10 funcsigs-1.0.2 futures-3.3.0 gast-0.3.3 grpcio-1.29.0 h5py-2.10.0 keras-applications-1.0.8 keras-preprocessing-1.1.2 markdown-3.1.1 mock-3.0.5 numpy-1.16.6 protobuf-3.12.2 setuptools-44.1.1 six-1.15.0 tensorboard-1.14.0 tensorflow-1.14.0 tensorflow-estimator-1.14.0 termcolor-1.1.0 werkzeug-1.0.1 wheel-0.34.2
(persephone) ye@ykt-pro:~/exp/persephone$
```

## Reinstall persephone

Tensorflow framework looks OK and thus, I reinstall persephone again as follows:  

```
(persephone) ye@ykt-pro:~/exp/persephone$ pip uninstall persephone
WARNING: Skipping persephone as it is not installed.
(persephone) ye@ykt-pro:~/exp/persephone$ pip install persephone
Collecting persephone
  Using cached persephone-0.4.2-py3-none-any.whl (66 kB)
Collecting nltk==3.4.5
  Using cached nltk-3.4.5.zip (1.5 MB)
Collecting pympi-ling==1.69
  Using cached pympi-ling-1.69.tar.gz (29 kB)
ERROR: Could not find a version that satisfies the requirement tensorflow<2,>=1.13.1 (from persephone) (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow<2,>=1.13.1 (from persephone)
```

### Used "--force-reinstall" option of pip

```
(persephone) ye@ykt-pro:~/exp/persephone$ pip install persephone --force-reinstall
Collecting persephone
  Using cached persephone-0.4.2-py3-none-any.whl (66 kB)
Collecting python-speech-features==0.6
  Using cached python_speech_features-0.6.tar.gz (5.6 kB)
Collecting scikit-learn==0.21.2
  Downloading scikit-learn-0.21.2.tar.gz (12.2 MB)
     |████████████████████████████████| 12.2 MB 411 kB/s 
Collecting pint==0.9
  Using cached Pint-0.9-py2.py3-none-any.whl (138 kB)
Collecting numpy<2,>=1.14.5
  Using cached numpy-1.18.4-cp38-cp38-manylinux1_x86_64.whl (20.7 MB)
Collecting pydub==0.20.0
  Using cached pydub-0.20.0-py2.py3-none-any.whl (25 kB)
Collecting scipy<2,>=1.1.0
  Using cached scipy-1.4.1-cp38-cp38-manylinux1_x86_64.whl (26.0 MB)
Collecting pympi-ling==1.69
  Using cached pympi-ling-1.69.tar.gz (29 kB)
ERROR: Could not find a version that satisfies the requirement tensorflow<2,>=1.13.1 (from persephone) (from versions: 2.2.0rc1, 2.2.0rc2, 2.2.0rc3, 2.2.0rc4, 2.2.0)
ERROR: No matching distribution found for tensorflow<2,>=1.13.1 (from persephone)
```

Oh!!! No ...

## Downgrade Python Version

Another option is downgrading the Python version ....

```
(persephone) ye@ykt-pro:~/exp/persephone$ python --version
Python 3.8.3
(persephone) ye@ykt-pro:~/exp/persephone$ conda install python=3.7
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 4.8.3

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/persephone

  added / updated specs:
    - python=3.7


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    certifi-2020.4.5.1         |           py37_0         155 KB
    pip-20.0.2                 |           py37_3         1.7 MB
    python-3.7.7               |       hcff3b4d_5        45.1 MB
    setuptools-46.4.0          |           py37_0         514 KB
    wheel-0.34.2               |           py37_0          51 KB
    ------------------------------------------------------------
                                           Total:        47.5 MB

The following packages will be DOWNGRADED:

  certifi                                 2020.4.5.1-py38_0 --> 2020.4.5.1-py37_0
  pip                                         20.0.2-py38_3 --> 20.0.2-py37_3
  python                                   3.8.3-hcff3b4d_0 --> 3.7.7-hcff3b4d_5
  setuptools                                  46.4.0-py38_0 --> 46.4.0-py37_0
  wheel                                       0.34.2-py38_0 --> 0.34.2-py37_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
certifi-2020.4.5.1   | 155 KB    | ######################################################## | 100% 
pip-20.0.2           | 1.7 MB    | ######################################################## | 100% 
python-3.7.7         | 45.1 MB   | ######################################################## | 100% 
wheel-0.34.2         | 51 KB     | ######################################################## | 100% 
setuptools-46.4.0    | 514 KB    | ######################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
```

## Try again installation of persephone

```
(persephone) ye@ykt-pro:~/exp/persephone$ python --version
Python 3.7.7
(persephone) ye@ykt-pro:~/exp/persephone$ pip install persephone --force-reinstall
Collecting persephone
  Using cached persephone-0.4.2-py3-none-any.whl (66 kB)
Collecting scikit-learn==0.21.2
  Downloading scikit_learn-0.21.2-cp37-cp37m-manylinux1_x86_64.whl (6.7 MB)
     |████████████████████████████████| 6.7 MB 410 kB/s 
Collecting scipy<2,>=1.1.0
  Downloading scipy-1.4.1-cp37-cp37m-manylinux1_x86_64.whl (26.1 MB)
     |████████████████████████████████| 26.1 MB 573 kB/s 
Collecting numpy<2,>=1.14.5
  Downloading numpy-1.18.4-cp37-cp37m-manylinux1_x86_64.whl (20.2 MB)
     |████████████████████████████████| 20.2 MB 449 kB/s 
Collecting pympi-ling==1.69
  Using cached pympi-ling-1.69.tar.gz (29 kB)
Collecting tensorflow<2,>=1.13.1
  Downloading tensorflow-1.15.3-cp37-cp37m-manylinux2010_x86_64.whl (110.5 MB)
     |████████████████████████████████| 110.5 MB 27 kB/s 
WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProtocolError('Connection aborted.', ConnectionResetError(104, 'Connection reset by peer'))': /simple/nltk/
Collecting nltk==3.4.5
  Using cached nltk-3.4.5.zip (1.5 MB)
Collecting pydub==0.20.0
  Using cached pydub-0.20.0-py2.py3-none-any.whl (25 kB)
Collecting python-speech-features==0.6
  Using cached python_speech_features-0.6.tar.gz (5.6 kB)
Collecting pint==0.9
  Using cached Pint-0.9-py2.py3-none-any.whl (138 kB)
Collecting joblib>=0.11
  Using cached joblib-0.15.1-py3-none-any.whl (298 kB)
Collecting absl-py>=0.7.0
  Using cached absl-py-0.9.0.tar.gz (104 kB)
Collecting tensorboard<1.16.0,>=1.15.0
  Downloading tensorboard-1.15.0-py3-none-any.whl (3.8 MB)
     |████████████████████████████████| 3.8 MB 643 kB/s 
Collecting keras-preprocessing>=1.0.5
  Using cached Keras_Preprocessing-1.1.2-py2.py3-none-any.whl (42 kB)
Collecting protobuf>=3.6.1
  Downloading protobuf-3.12.2-cp37-cp37m-manylinux1_x86_64.whl (1.3 MB)
     |████████████████████████████████| 1.3 MB 167 kB/s 
Collecting opt-einsum>=2.3.2
  Downloading opt_einsum-3.2.1-py3-none-any.whl (63 kB)
     |████████████████████████████████| 63 kB 263 kB/s 
Collecting gast==0.2.2
  Downloading gast-0.2.2.tar.gz (10 kB)
Collecting keras-applications>=1.0.8
  Downloading Keras_Applications-1.0.8-py3-none-any.whl (50 kB)
     |████████████████████████████████| 50 kB 262 kB/s 
Collecting wrapt>=1.11.1
  Downloading wrapt-1.12.1.tar.gz (27 kB)
Collecting google-pasta>=0.1.6
  Downloading google_pasta-0.2.0-py3-none-any.whl (57 kB)
     |████████████████████████████████| 57 kB 276 kB/s 
Collecting tensorflow-estimator==1.15.1
  Downloading tensorflow_estimator-1.15.1-py2.py3-none-any.whl (503 kB)
     |████████████████████████████████| 503 kB 269 kB/s 
Collecting wheel>=0.26; python_version >= "3"
  Using cached wheel-0.34.2-py2.py3-none-any.whl (26 kB)
Collecting grpcio>=1.8.6
  Downloading grpcio-1.29.0-cp37-cp37m-manylinux2010_x86_64.whl (3.0 MB)
     |████████████████████████████████| 3.0 MB 260 kB/s 
Collecting six>=1.10.0
  Using cached six-1.15.0-py2.py3-none-any.whl (10 kB)
Collecting termcolor>=1.1.0
  Using cached termcolor-1.1.0.tar.gz (3.9 kB)
Collecting astor>=0.6.0
  Using cached astor-0.8.1-py2.py3-none-any.whl (27 kB)
Collecting markdown>=2.6.8
  Downloading Markdown-3.2.2-py3-none-any.whl (88 kB)
     |████████████████████████████████| 88 kB 306 kB/s 
Collecting setuptools>=41.0.0
  Downloading setuptools-47.1.1-py3-none-any.whl (583 kB)
     |████████████████████████████████| 583 kB 192 kB/s 
Collecting werkzeug>=0.11.15
  Using cached Werkzeug-1.0.1-py2.py3-none-any.whl (298 kB)
Collecting h5py
  Downloading h5py-2.10.0-cp37-cp37m-manylinux1_x86_64.whl (2.9 MB)
     |████████████████████████████████| 2.9 MB 322 kB/s 
Collecting importlib-metadata; python_version < "3.8"
  Downloading importlib_metadata-1.6.0-py2.py3-none-any.whl (30 kB)
Collecting zipp>=0.5
  Downloading zipp-3.1.0-py3-none-any.whl (4.9 kB)
Building wheels for collected packages: pympi-ling, nltk, python-speech-features, absl-py, gast, wrapt, termcolor
  Building wheel for pympi-ling (setup.py) ... done
  Created wheel for pympi-ling: filename=pympi_ling-1.69-py3-none-any.whl size=23079 sha256=80022b4b4d3e3e713da7e69dee34ab076dff755bbfe6eea2415b180b73a45ca8
  Stored in directory: /home/ye/.cache/pip/wheels/45/3c/67/db0bc7092b810b2f8558bc5ab0021404087a02e28e80b3675c
  Building wheel for nltk (setup.py) ... done
  Created wheel for nltk: filename=nltk-3.4.5-py3-none-any.whl size=1449905 sha256=1fa680c10457616a954d9c63f398992e70d601000849820b58dd4ddd80f1e17d
  Stored in directory: /home/ye/.cache/pip/wheels/48/8b/7f/473521e0c731c6566d631b281f323842bbda9bd819eb9a3ead
  Building wheel for python-speech-features (setup.py) ... done
  Created wheel for python-speech-features: filename=python_speech_features-0.6-py3-none-any.whl size=5888 sha256=b48d6defc0fd82c5872d8b7c34b42583f2adf47d81b6e2e57996c5d4a2767295
  Stored in directory: /home/ye/.cache/pip/wheels/b0/0e/94/28cd6afa3cd5998a63eef99fe31777acd7d758f59cf24839eb
  Building wheel for absl-py (setup.py) ... done
  Created wheel for absl-py: filename=absl_py-0.9.0-py3-none-any.whl size=121931 sha256=d13271e8169bedc285c37c71a29068a853411972518a9150f4175ee15bfc9fe1
  Stored in directory: /home/ye/.cache/pip/wheels/cc/af/1a/498a24d0730ef484019e007bb9e8cef3ac00311a672c049a3e
  Building wheel for gast (setup.py) ... done
  Created wheel for gast: filename=gast-0.2.2-py3-none-any.whl size=7539 sha256=c3d906203f4f7f9f50c0ec92b5226606ffdd60a4c50c55a25d4858b9430b8f1d
  Stored in directory: /home/ye/.cache/pip/wheels/21/7f/02/420f32a803f7d0967b48dd823da3f558c5166991bfd204eef3
  Building wheel for wrapt (setup.py) ... done
  Created wheel for wrapt: filename=wrapt-1.12.1-cp37-cp37m-linux_x86_64.whl size=70977 sha256=8a613b68b5f3d996d58ef308bdc1a49961edb1395b10ea4c598da92399c8de10
  Stored in directory: /home/ye/.cache/pip/wheels/62/76/4c/aa25851149f3f6d9785f6c869387ad82b3fd37582fa8147ac6
  Building wheel for termcolor (setup.py) ... done
  Created wheel for termcolor: filename=termcolor-1.1.0-py3-none-any.whl size=4830 sha256=2b804b28b1424e2ffe99dbfa31b2511cae4da22152dc42f8c84b41399101c7e0
  Stored in directory: /home/ye/.cache/pip/wheels/3f/e3/ec/8a8336ff196023622fbcb36de0c5a5c218cbb24111d1d4c7f2
Successfully built pympi-ling nltk python-speech-features absl-py gast wrapt termcolor
Installing collected packages: joblib, numpy, scipy, scikit-learn, pympi-ling, six, absl-py, zipp, importlib-metadata, markdown, grpcio, setuptools, wheel, werkzeug, protobuf, tensorboard, keras-preprocessing, opt-einsum, gast, h5py, keras-applications, wrapt, google-pasta, tensorflow-estimator, termcolor, astor, tensorflow, nltk, pydub, python-speech-features, pint, persephone
  Attempting uninstall: setuptools
    Found existing installation: setuptools 46.4.0.post20200518
    Uninstalling setuptools-46.4.0.post20200518:
      Successfully uninstalled setuptools-46.4.0.post20200518
  Attempting uninstall: wheel
    Found existing installation: wheel 0.34.2
    Uninstalling wheel-0.34.2:
      Successfully uninstalled wheel-0.34.2
Successfully installed absl-py-0.9.0 astor-0.8.1 gast-0.2.2 google-pasta-0.2.0 grpcio-1.29.0 h5py-2.10.0 importlib-metadata-1.6.0 joblib-0.15.1 keras-applications-1.0.8 keras-preprocessing-1.1.2 markdown-3.2.2 nltk-3.4.5 numpy-1.18.4 opt-einsum-3.2.1 persephone-0.4.2 pint-0.9 protobuf-3.12.2 pydub-0.20.0 pympi-ling-1.69 python-speech-features-0.6 scikit-learn-0.21.2 scipy-1.4.1 setuptools-47.1.1 six-1.15.0 tensorboard-1.15.0 tensorflow-1.15.3 tensorflow-estimator-1.15.1 termcolor-1.1.0 werkzeug-1.0.1 wheel-0.34.2 wrapt-1.12.1 zipp-3.1.0
(persephone) ye@ykt-pro:~/exp/persephone$ 
```

Finally I can manage to install persephone successfully!!! :)

## download Na data and extracted

I downloaded "Na" data that used for example training with persephone.  
After downloaded, I moved it to the folder under ~/exp/persephone/persephone-tutorial/.  


```
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ tree -L 2
.
├── na_example
│   ├── feat
│   └── label
└── na_example.zip

3 directories, 1 file
```

The example shows running on iPython shell. Currently there is no iPython on my "persephone" conda environment.  

```
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ ipython

Command 'ipython' not found, but can be installed with:

sudo apt install ipython
```

## iPython Installation with sudo apt

I got the error when I installed iPython with "sudo apt".  

```
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ sudo apt install ipython
[sudo] password for ye: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  python-backports-shutil-get-terminal-size python-chardet python-decorator python-ipython
  python-ipython-genutils python-pathlib2 python-pexpect python-pickleshare python-prompt-toolkit
  python-ptyprocess python-pygments python-scandir python-simplegeneric python-traitlets
  python-wcwidth
Suggested packages:
  python-pexpect-doc ttf-bitstream-vera
The following NEW packages will be installed:
  ipython python-backports-shutil-get-terminal-size python-chardet python-decorator
  python-ipython python-ipython-genutils python-pathlib2 python-pexpect python-pickleshare
  python-prompt-toolkit python-ptyprocess python-pygments python-scandir python-simplegeneric
  python-traitlets python-wcwidth
0 upgraded, 16 newly installed, 0 to remove and 75 not upgraded.
Need to get 1,421 kB of archives.
After this operation, 7,607 kB of additional disk space will be used.
Do you want to continue? [Y/n] Y
Get:1 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 python-decorator all 4.1.2-1 [9,300 B]
Get:2 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-ptyprocess all 0.5.2-1 [12.6 kB]
Get:3 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-pexpect all 4.2.1-1 [41.7 kB]
Get:4 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-scandir amd64 1.7-1 [17.7 kB]
Get:5 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-pathlib2 all 2.3.0-1 [15.9 kB]
Get:6 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-pickleshare all 0.7.4-2 [6,832 B]
Get:7 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-wcwidth all 0.1.7+dfsg1-1 [14.7 kB]
Get:8 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-prompt-toolkit all 1.0.15-1 [163 kB]
Get:9 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 python-pygments all 2.2.0+dfsg-1 [577 kB]
Get:10 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 python-simplegeneric all 0.8.1-1 [11.5 kB]
Get:11 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-ipython-genutils all 0.2.0-1 [20.8 kB]
Get:12 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-traitlets all 4.3.2-1 [59.0 kB]
Get:13 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-backports-shutil-get-terminal-size all 1.0.0-5 [5,024 B]
Get:14 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 python-ipython all 5.5.0-1 [381 kB]
Get:15 http://mm.archive.ubuntu.com/ubuntu bionic/universe amd64 ipython all 5.5.0-1 [5,284 B]
Get:16 http://mm.archive.ubuntu.com/ubuntu bionic/main amd64 python-chardet all 3.0.4-1 [80.3 kB]
Fetched 1,421 kB in 4s (344 kB/s)          
Selecting previously unselected package python-decorator.
(Reading database ... 221757 files and directories currently installed.)
Preparing to unpack .../00-python-decorator_4.1.2-1_all.deb ...
Unpacking python-decorator (4.1.2-1) ...
Selecting previously unselected package python-ptyprocess.
Preparing to unpack .../01-python-ptyprocess_0.5.2-1_all.deb ...
Unpacking python-ptyprocess (0.5.2-1) ...
Selecting previously unselected package python-pexpect.
Preparing to unpack .../02-python-pexpect_4.2.1-1_all.deb ...
Unpacking python-pexpect (4.2.1-1) ...
Selecting previously unselected package python-scandir.
Preparing to unpack .../03-python-scandir_1.7-1_amd64.deb ...
Unpacking python-scandir (1.7-1) ...
Selecting previously unselected package python-pathlib2.
Preparing to unpack .../04-python-pathlib2_2.3.0-1_all.deb ...
Unpacking python-pathlib2 (2.3.0-1) ...
Selecting previously unselected package python-pickleshare.
Preparing to unpack .../05-python-pickleshare_0.7.4-2_all.deb ...
Unpacking python-pickleshare (0.7.4-2) ...
Selecting previously unselected package python-wcwidth.
Preparing to unpack .../06-python-wcwidth_0.1.7+dfsg1-1_all.deb ...
Unpacking python-wcwidth (0.1.7+dfsg1-1) ...
Selecting previously unselected package python-prompt-toolkit.
Preparing to unpack .../07-python-prompt-toolkit_1.0.15-1_all.deb ...
Unpacking python-prompt-toolkit (1.0.15-1) ...
Selecting previously unselected package python-pygments.
Preparing to unpack .../08-python-pygments_2.2.0+dfsg-1_all.deb ...
Unpacking python-pygments (2.2.0+dfsg-1) ...
Selecting previously unselected package python-simplegeneric.
Preparing to unpack .../09-python-simplegeneric_0.8.1-1_all.deb ...
Unpacking python-simplegeneric (0.8.1-1) ...
Selecting previously unselected package python-ipython-genutils.
Preparing to unpack .../10-python-ipython-genutils_0.2.0-1_all.deb ...
Unpacking python-ipython-genutils (0.2.0-1) ...
Selecting previously unselected package python-traitlets.
Preparing to unpack .../11-python-traitlets_4.3.2-1_all.deb ...
Unpacking python-traitlets (4.3.2-1) ...
Selecting previously unselected package python-backports-shutil-get-terminal-size.
Preparing to unpack .../12-python-backports-shutil-get-terminal-size_1.0.0-5_all.deb ...
Unpacking python-backports-shutil-get-terminal-size (1.0.0-5) ...
Selecting previously unselected package python-ipython.
Preparing to unpack .../13-python-ipython_5.5.0-1_all.deb ...
Unpacking python-ipython (5.5.0-1) ...
Selecting previously unselected package ipython.
Preparing to unpack .../14-ipython_5.5.0-1_all.deb ...
Unpacking ipython (5.5.0-1) ...
Selecting previously unselected package python-chardet.
Preparing to unpack .../15-python-chardet_3.0.4-1_all.deb ...
Unpacking python-chardet (3.0.4-1) ...
Setting up python-simplegeneric (0.8.1-1) ...
Setting up python-chardet (3.0.4-1) ...
Setting up python-scandir (1.7-1) ...
Setting up python-backports-shutil-get-terminal-size (1.0.0-5) ...
Setting up python-ipython-genutils (0.2.0-1) ...
Setting up python-wcwidth (0.1.7+dfsg1-1) ...
Setting up python-pygments (2.2.0+dfsg-1) ...
Setting up python-ptyprocess (0.5.2-1) ...
Setting up python-decorator (4.1.2-1) ...
Setting up python-pathlib2 (2.3.0-1) ...
Setting up python-traitlets (4.3.2-1) ...
Setting up python-prompt-toolkit (1.0.15-1) ...
Setting up python-pexpect (4.2.1-1) ...
Setting up python-pickleshare (0.7.4-2) ...
Setting up python-ipython (5.5.0-1) ...
Setting up ipython (5.5.0-1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$

(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ ipython
Traceback (most recent call last):
  File "<string>", line 1, in <module>
ModuleNotFoundError: No module named 'IPython'
```

## iPython installation with pip


```
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ pip install ipython
Collecting ipython
  Downloading ipython-7.15.0-py3-none-any.whl (783 kB)
     |████████████████████████████████| 783 kB 541 kB/s 
Collecting pexpect; sys_platform != "win32"
  Downloading pexpect-4.8.0-py2.py3-none-any.whl (59 kB)
     |████████████████████████████████| 59 kB 637 kB/s 
Collecting jedi>=0.10
  Downloading jedi-0.17.0-py2.py3-none-any.whl (1.1 MB)
     |████████████████████████████████| 1.1 MB 400 kB/s 
Collecting prompt-toolkit!=3.0.0,!=3.0.1,<3.1.0,>=2.0.0
  Downloading prompt_toolkit-3.0.5-py3-none-any.whl (351 kB)
     |████████████████████████████████| 351 kB 546 kB/s 
Collecting traitlets>=4.2
  Downloading traitlets-4.3.3-py2.py3-none-any.whl (75 kB)
     |████████████████████████████████| 75 kB 280 kB/s 
Collecting decorator
  Downloading decorator-4.4.2-py2.py3-none-any.whl (9.2 kB)
Collecting pickleshare
  Downloading pickleshare-0.7.5-py2.py3-none-any.whl (6.9 kB)
Requirement already satisfied: setuptools>=18.5 in /home/ye/tool/anaconda3/envs/persephone/lib/python3.7/site-packages (from ipython) (47.1.1)
Collecting pygments
  Downloading Pygments-2.6.1-py3-none-any.whl (914 kB)
     |████████████████████████████████| 914 kB 309 kB/s 
Collecting backcall
  Downloading backcall-0.1.0.tar.gz (9.7 kB)
Collecting ptyprocess>=0.5
  Downloading ptyprocess-0.6.0-py2.py3-none-any.whl (39 kB)
Collecting parso>=0.7.0
  Downloading parso-0.7.0-py2.py3-none-any.whl (100 kB)
     |████████████████████████████████| 100 kB 704 kB/s 
Collecting wcwidth
  Downloading wcwidth-0.1.9-py2.py3-none-any.whl (19 kB)
Collecting ipython-genutils
  Downloading ipython_genutils-0.2.0-py2.py3-none-any.whl (26 kB)
Requirement already satisfied: six in /home/ye/tool/anaconda3/envs/persephone/lib/python3.7/site-packages (from traitlets>=4.2->ipython) (1.15.0)
Building wheels for collected packages: backcall
  Building wheel for backcall (setup.py) ... done
  Created wheel for backcall: filename=backcall-0.1.0-py3-none-any.whl size=10413 sha256=2e3f3ee846e25b0ad8ca519ec21dffca428f7ffe4c5b55975830d88b0d403e98
  Stored in directory: /home/ye/.cache/pip/wheels/9e/56/4f/da13e448a8a5b8671b2954600d5355cf36e557c7aa5020139b
Successfully built backcall
Installing collected packages: ptyprocess, pexpect, parso, jedi, wcwidth, prompt-toolkit, decorator, ipython-genutils, traitlets, pickleshare, pygments, backcall, ipython
Successfully installed backcall-0.1.0 decorator-4.4.2 ipython-7.15.0 ipython-genutils-0.2.0 jedi-0.17.0 parso-0.7.0 pexpect-4.8.0 pickleshare-0.7.5 prompt-toolkit-3.0.5 ptyprocess-0.6.0 pygments-2.6.1 traitlets-4.3.3 wcwidth-0.1.9
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$
```

## Error Relating to ffmpeg, avconv

When I train with example data ... I found that I need to install "ffmpeg or avconv" as follows:  

```
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ ipython
Python 3.7.7 (default, May  7 2020, 21:25:33) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.15.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: from persephone import corpus                                                              
/home/ye/tool/anaconda3/envs/persephone/lib/python3.7/site-packages/pydub/utils.py:165: RuntimeWarning: Couldn't find ffmpeg or avconv - defaulting to ffmpeg, but may not work
  warn("Couldn't find ffmpeg or avconv - defaulting to ffmpeg, but may not work", RuntimeWarning)

In [2]:   

```

## Installing ffmpeg

```
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ sudo apt install ffmpeg

(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ ffmpeg --help
ffmpeg version 3.4.6-0ubuntu0.18.04.1 Copyright (c) 2000-2019 the FFmpeg developers
  built with gcc 7 (Ubuntu 7.3.0-16ubuntu3)
  configuration: --prefix=/usr --extra-version=0ubuntu0.18.04.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --enable-gpl --disable-stripping --enable-avresample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librubberband --enable-librsvg --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-omx --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libopencv --enable-libx264 --enable-shared
  libavutil      55. 78.100 / 55. 78.100
  libavcodec     57.107.100 / 57.107.100
  libavformat    57. 83.100 / 57. 83.100
  libavdevice    57. 10.100 / 57. 10.100
  libavfilter     6.107.100 /  6.107.100
  libavresample   3.  7.  0 /  3.  7.  0
  libswscale      4.  8.100 /  4.  8.100
  libswresample   2.  9.100 /  2.  9.100
  libpostproc    54.  7.100 / 54.  7.100
Hyper fast Audio and Video encoder
usage: ffmpeg [options] [[infile options] -i infile]... {[outfile options] outfile}...

Getting help:
    -h      -- print basic options
    -h long -- print more options
    -h full -- print all options (including all format and codec specific options, very long)
    -h type=name -- print all options for the named decoder/encoder/demuxer/muxer/filter
    See man ffmpeg for detailed description of the options.

Print help / information / capabilities:
-L                  show license
-h topic            show help
-? topic            show help
-help topic         show help
--help topic        show help
-version            show version
-buildconf          show build configuration
-formats            show available formats
-muxers             show available muxers
-demuxers           show available demuxers
-devices            show available devices
-codecs             show available codecs
-decoders           show available decoders
-encoders           show available encoders
-bsfs               show available bit stream filters
-protocols          show available protocols
-filters            show available filters
-pix_fmts           show available pixel formats
-layouts            show standard channel layouts
-sample_fmts        show available audio sample formats
-colors             show available color names
-sources device     list sources of the input device
-sinks device       list sinks of the output device
-hwaccels           show available HW acceleration methods

Global options (affect whole program instead of just one file:
-loglevel loglevel  set logging level
-v loglevel         set logging level
-report             generate a report
-max_alloc bytes    set maximum size of a single allocated block
-y                  overwrite output files
-n                  never overwrite output files
-ignore_unknown     Ignore unknown stream types
-filter_threads     number of non-complex filter threads
-filter_complex_threads  number of threads for -filter_complex
-stats              print progress report during encoding
-max_error_rate ratio of errors (0.0: no errors, 1.0: 100% error  maximum error rate
-bits_per_raw_sample number  set the number of bits per raw sample
-vol volume         change audio volume (256=normal)

Per-file main options:
-f fmt              force format
-c codec            codec name
-codec codec        codec name
-pre preset         preset name
-map_metadata outfile[,metadata]:infile[,metadata]  set metadata information of outfile from infile
-t duration         record or transcode "duration" seconds of audio/video
-to time_stop       record or transcode stop time
-fs limit_size      set the limit file size in bytes
-ss time_off        set the start time offset
-sseof time_off     set the start time offset relative to EOF
-seek_timestamp     enable/disable seeking by timestamp with -ss
-timestamp time     set the recording timestamp ('now' to set the current time)
-metadata string=string  add metadata
-program title=string:st=number...  add program with specified streams
-target type        specify target file type ("vcd", "svcd", "dvd", "dv" or "dv50" with optional prefixes "pal-", "ntsc-" or "film-")
-apad               audio pad
-frames number      set the number of frames to output
-filter filter_graph  set stream filtergraph
-filter_script filename  read stream filtergraph description from a file
-reinit_filter      reinit filtergraph on input parameter changes
-discard            discard
-disposition        disposition

Video options:
-vframes number     set the number of video frames to output
-r rate             set frame rate (Hz value, fraction or abbreviation)
-s size             set frame size (WxH or abbreviation)
-aspect aspect      set aspect ratio (4:3, 16:9 or 1.3333, 1.7777)
-bits_per_raw_sample number  set the number of bits per raw sample
-vn                 disable video
-vcodec codec       force video codec ('copy' to copy stream)
-timecode hh:mm:ss[:;.]ff  set initial TimeCode value.
-pass n             select the pass number (1 to 3)
-vf filter_graph    set video filters
-ab bitrate         audio bitrate (please use -b:a)
-b bitrate          video bitrate (please use -b:v)
-dn                 disable data

Audio options:
-aframes number     set the number of audio frames to output
-aq quality         set audio quality (codec-specific)
-ar rate            set audio sampling rate (in Hz)
-ac channels        set number of audio channels
-an                 disable audio
-acodec codec       force audio codec ('copy' to copy stream)
-vol volume         change audio volume (256=normal)
-af filter_graph    set audio filters

Subtitle options:
-s size             set frame size (WxH or abbreviation)
-sn                 disable subtitle
-scodec codec       force subtitle codec ('copy' to copy stream)
-stag fourcc/tag    force subtitle tag/fourcc
-fix_sub_duration   fix subtitles duration
-canvas_size size   set canvas size (WxH or abbreviation)
-spre preset        set the subtitle options to the indicated preset
```

## Start Training with "Na" Data

I got error message as follows:  

```
(persephone) ye@ykt-pro:~/exp/persephone/persephone-tutorial$ ipython
Python 3.7.7 (default, May  7 2020, 21:25:33) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.15.0 -- An enhanced Interactive Python. Type '?' for help.

In [1]: from persephone import corpus                                                              

In [2]: corp = corpus.Corpus("fbank", "phonemes", "./data/na_example")                             
---------------------------------------------------------------------------
PersephoneException                       Traceback (most recent call last)
<ipython-input-2-2ffc636d6333> in <module>
----> 1 corp = corpus.Corpus("fbank", "phonemes", "./data/na_example")

~/tool/anaconda3/envs/persephone/lib/python3.7/site-packages/persephone/corpus.py in __init__(self, feat_type, label_type, tgt_dir, labels, max_samples, speakers)
    179 
    180         logger.debug("Setting up directories for this Corpus object at %s", self.tgt_dir)
--> 181         self.set_and_check_directories(self.tgt_dir)
    182 
    183         # Label-related stuff

~/tool/anaconda3/envs/persephone/lib/python3.7/site-packages/persephone/corpus.py in set_and_check_directories(self, tgt_dir)
    352         if not self.wav_dir.is_dir():
    353             raise PersephoneException(
--> 354                 "The supplied path requires a 'wav' subdirectory.")
    355         self.feat_dir.mkdir(parents=True, exist_ok=True)
    356         if not self.label_dir.is_dir():

PersephoneException: The supplied path requires a 'wav' subdirectory.

Got ERROR!!!
```

## Change Folder

```
(base) ye@ykt-pro:~/exp/persephone/persephone-tutorial/data/na_example$ ls
feat  label
(base) ye@ykt-pro:~/exp/persephone/persephone-tutorial/data/na_example$ mv feat/ wav
(base) ye@ykt-pro:~/exp/persephone/persephone-tutorial/data/na_example$ ls
label  wav
```

## Training with "Na" Data Again.

Finally training success as follows:  

```
$ ipython
> from persephone import corpus
> corp = corpus.Corpus("fbank", "phonemes", "data/na_example")
```

You have to wait for several minutes ...

```
...
...
...
Input #0, wav, from 'data/na_example/wav/crdo-NRU_NUMPLUSCL_M1_HEAP_1TO100_F4_24SEPT2011_AUDIOPLUSEGG.10.wav':
  Metadata:
    encoder         : Lavf57.71.100
  Duration: 00:00:01.50, bitrate: 256 kb/s
    Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 16000 Hz, mono, s16, 256 kb/s
Stream mapping:
  Stream #0:0 -> #0:0 (pcm_s16le (native) -> pcm_s16le (native))
Press [q] to stop, [?] for help
Output #0, wav, to 'data/na_example/feat/crdo-NRU_NUMPLUSCL_M1_HEAP_1TO100_F4_24SEPT2011_AUDIOPLUSEGG.10.wav':
  Metadata:
    ISFT            : Lavf57.83.100
    Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 16000 Hz, mono, s16, 256 kb/s
    Metadata:
      encoder         : Lavc57.107.100 pcm_s16le
size=      47kB time=00:00:01.49 bitrate= 256.4kbits/s speed=1.86e+03x    
video:0kB audio:47kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.162717%
ffmpeg version 3.4.6-0ubuntu0.18.04.1 Copyright (c) 2000-2019 the FFmpeg developers
  built with gcc 7 (Ubuntu 7.3.0-16ubuntu3)
  configuration: --prefix=/usr --extra-version=0ubuntu0.18.04.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --enable-gpl --disable-stripping --enable-avresample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librubberband --enable-librsvg --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-omx --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libopencv --enable-libx264 --enable-shared
  libavutil      55. 78.100 / 55. 78.100
  libavcodec     57.107.100 / 57.107.100
  libavformat    57. 83.100 / 57. 83.100
  libavdevice    57. 10.100 / 57. 10.100
  libavfilter     6.107.100 /  6.107.100
  libavresample   3.  7.  0 /  3.  7.  0
  libswscale      4.  8.100 /  4.  8.100
  libswresample   2.  9.100 /  2.  9.100
  libpostproc    54.  7.100 / 54.  7.100
Guessed Channel Layout for Input Stream #0.0 : mono
Input #0, wav, from 'data/na_example/wav/crdo-NRU_NUMPLUSCL_M2_ROUNDOBJECTS_1TO100_F4_3OCT2011_AUDIOPLUSEGG.61.wav':
  Metadata:
    encoder         : Lavf57.71.100
  Duration: 00:00:01.59, bitrate: 256 kb/s
    Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 16000 Hz, mono, s16, 256 kb/s
Stream mapping:
  Stream #0:0 -> #0:0 (pcm_s16le (native) -> pcm_s16le (native))
Press [q] to stop, [?] for help
Output #0, wav, to 'data/na_example/feat/crdo-NRU_NUMPLUSCL_M2_ROUNDOBJECTS_1TO100_F4_3OCT2011_AUDIOPLUSEGG.61.wav':
  Metadata:
    ISFT            : Lavf57.83.100
    Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 16000 Hz, mono, s16, 256 kb/s
    Metadata:
      encoder         : Lavc57.107.100 pcm_s16le
size=      50kB time=00:00:01.58 bitrate= 256.4kbits/s speed=1.75e+03x    
video:0kB audio:50kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.153785%
ffmpeg version 3.4.6-0ubuntu0.18.04.1 Copyright (c) 2000-2019 the FFmpeg developers
  built with gcc 7 (Ubuntu 7.3.0-16ubuntu3)
  configuration: --prefix=/usr --extra-version=0ubuntu0.18.04.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --enable-gpl --disable-stripping --enable-avresample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librubberband --enable-librsvg --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-omx --enable-openal --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-chromaprint --enable-frei0r --enable-libopencv --enable-libx264 --enable-shared
  libavutil      55. 78.100 / 55. 78.100
  libavcodec     57.107.100 / 57.107.100
  libavformat    57. 83.100 / 57. 83.100
  libavdevice    57. 10.100 / 57. 10.100
  libavfilter     6.107.100 /  6.107.100
  libavresample   3.  7.  0 /  3.  7.  0
  libswscale      4.  8.100 /  4.  8.100
  libswresample   2.  9.100 /  2.  9.100
  libpostproc    54.  7.100 / 54.  7.100
Guessed Channel Layout for Input Stream #0.0 : mono
Input #0, wav, from 'data/na_example/wav/crdo-NRU_NUMPLUSCL_MH1_YEAR_1TO30_F4_11MARCH2009.20.wav':
  Metadata:
    encoder         : Lavf57.71.100
  Duration: 00:00:01.46, bitrate: 256 kb/s
    Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 16000 Hz, mono, s16, 256 kb/s
Stream mapping:
  Stream #0:0 -> #0:0 (pcm_s16le (native) -> pcm_s16le (native))
Press [q] to stop, [?] for help
Output #0, wav, to 'data/na_example/feat/crdo-NRU_NUMPLUSCL_MH1_YEAR_1TO30_F4_11MARCH2009.20.wav':
  Metadata:
    ISFT            : Lavf57.83.100
    Stream #0:0: Audio: pcm_s16le ([1][0][0][0] / 0x0001), 16000 Hz, mono, s16, 256 kb/s
    Metadata:
      encoder         : Lavc57.107.100 pcm_s16le
size=      46kB time=00:00:01.46 bitrate= 256.4kbits/s speed=1.81e+03x    
video:0kB audio:46kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: 0.166610%

In [4]: from persephone import experiment                                                          
WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/persephone/lib/python3.7/site-packages/persephone/model.py:22: The name tf.ConfigProto is deprecated. Please use tf.compat.v1.ConfigProto instead.

WARNING:tensorflow:From /home/ye/tool/anaconda3/envs/persephone/lib/python3.7/site-packages/persephone/model.py:27: The name tf.train.Saver is deprecated. Please use tf.compat.v1.train.Saver instead.


In [5]:  experiment.train_ready(corp)
```

Training was started at 23:01 ...  
(23:01 မှာ training ... လုပ်ခဲ့)  

```
exp_dir ./exp/0, epoch 21
	Batch...0...1...2...3...4...5...6...7...8...9...10...11...12...13...14...15...16...17...18...19...20...21...22...23...24...25...26...27...28...29...30...31...32...33...34...35...36...37...38...39...40...41...42...43...44...45...46...47...48...49...50...51...52...53...54...55...56...57...58...59...60...61...62...63...64...65...66...67...68...69...70...71...72...73...74...75...76...77...78...79...80...81...82...83...84...85...86...87...88...89...90...91...92...93...94...95...96...97...98...99...100...101...102...103...104...105...106...107...108...109...110...111...112...113...114...115...116...117...118...119...120...121...122...123...124...125...126...127...128...129...130...131...132...133...134...135...136...137...138...139...140...141...142...143...144...145...146...147...148...149...150...151...152...153...154...155...156...157...158...159...160...161...162...163...164...165...166...167...168...169...170...171...172...173...174...175...176...177...178...179...180...181...182...183...184...185...186...187...188...189...190...191...192...193...194...195...196...197...198...199...200...201...202...203...204...205...206...207...208...209...210...211...212...213...214...215...216...217...218...219...220...221...222...223...224...225...226...227...228...229...230...
exp_dir ./exp/0, epoch 22
	Batch...0...1...2...3...4...5...6...7...8...9...10...11...12...13...14...15...16...17...18...19...20...21...22...23...24...25...26...27...28...29...30...31...32...33...34...35...36...37...38...39...40...41...42...43...44...45...46...47...48...49...50...51...52...53...54...55...56...57...58...59...60...61...62...63...64...65...66...67...68...69...70...71...72...73...74...75...76...77...78...79...80...81...82...83...84...85...86...87...88...89...90...91...92...93...94...95...96...97...98...99...100...101...102...103...104...105...106...107...108...109...110...111...112...113...114...115...116...117...118...119...120...121...122...123...124...125...126...127...128...129...130...131...132...133...134...135...136...137...138...139...140...141...142...143...144...145...146...147...148...149...150...151...152...153...154...155...156...157...158...159...160...161...162...163...164...165...166...167...168...169...170...171...172...173...174...175...176...177...178...179...180...181...182...183...184...185...186...187...188...189...190...191...192...193...194...195...196...197...198...199...200...201...202...203...204...205...206...207...208...209...210...211...212...213...214...215...216...217...218...219...220...221...222...223...224...225...226...227...228...229...230...
exp_dir ./exp/0, epoch 23
	Batch...0...1...2...3...4...5...6...7...8...9...10...11...12...13...14...15...16...17...18...19...20...21...22...23...24...25...26...27...28...29...30...31...32...33...34...35...36...37...38...39...40...41...42...43...44...45...46...47...48...49...50...51...52...53...54...55...56...57...58...59...60...61...62...63...64...65...66...67...68...69...70...71...72...73...74...75...76...77...78...79...80...81...82...83...84...85...86...87...88...89...90...91...92...93...94...95...96...97...98...99...100...101...102...103...104...105...106...107...108...109...110...111...112...113...114...115...116...117...118...119...120...121...122...123...124...125...126...127...128...129...130...131...132...133...134...135...136...137...138...139...140...141...142...143...144...145...146...147...148...149...150...151...152...153...154...155...156...157...158...159...160...161...162...163...164...165...166...167...168...169...170...171...172...173...174...175...176...177...178...179...180...181...182...183...184...185...186...187...188...189...190...191...192...193...194...195...196...197...198...199...200...201...202...203...204...205...206...207...208...209...210...211...212...213...214...215...216...217...218...219...220...221...222...223...224...225...226...227...228...229...230...INFO:tensorflow:Restoring parameters from ./exp/0/model/model_best.ckpt
Out[5]: './exp/0'

In [6]:        
```

Training လုပ်လို့ ပြီးတာက နောက်နေ့ မနက်မှ ပြီးတယ်။  


## Reference:

https://stackoverflow.com/questions/52584907/how-to-downgrade-python-from-3-7-to-3-6
https://github.com/tensorflow/tensorflow/issues/34302
https://stackoverflow.com/questions/41937915/how-to-pip-install-old-version-of-librarytensorflow
https://stackoverflow.com/questions/45179915/importerror-no-module-named-ipython


