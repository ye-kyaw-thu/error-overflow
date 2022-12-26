# Preparing a Baseline for RL experiments

For this time, I wanna run for 100 epochs baselines ...  

## Preparing to Run

```
#
#     $ conda activate simple-nmt
#
# To deactivate an active environment, use
#
#     $ conda deactivate

root@428d4e81f922:/home/ye/tool# conda activate simple-nmt
(simple-nmt) root@428d4e81f922:/home/ye/tool# ls
cuda_11.7.0_515.43.04_linux.run  gmonitor  multi-bleu.perl  simple-nmt
(simple-nmt) root@428d4e81f922:/home/ye/tool# cd simple-nmt
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# ls
README.md               continue_train.py  lm_train.py  test  train.py
continue_dual_train.py  dual_train.py      simple_nmt   tex   translate.py
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# python ./train.py --help
Traceback (most recent call last):
  File "./train.py", line 4, in <module>
    import torch
ModuleNotFoundError: No module named 'torch'
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# pip install torch
Collecting torch
  Downloading torch-1.10.2-cp36-cp36m-manylinux1_x86_64.whl (881.9 MB)
     |################################| 881.9 MB 82.1 MB/s
Collecting dataclasses
  Downloading dataclasses-0.8-py3-none-any.whl (19 kB)
Collecting typing-extensions
  Downloading typing_extensions-4.1.1-py3-none-any.whl (26 kB)
Installing collected packages: typing-extensions, dataclasses, torch
Successfully installed dataclasses-0.8 torch-1.10.2 typing-extensions-4.1.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt#
```

Try again ...  

```
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# python ./train.py --help
/root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/package/_directory_reader.py:17: UserWarning: Failed to initialize NumPy: numpy.core.multiarray failed to import (Triggered internally at  ../torch/csrc/utils/tensor_numpy.cpp:68.)
  _dtype_to_storage = {data_type(0).dtype: data_type for data_type in _storages}
Traceback (most recent call last):
  File "./train.py", line 8, in <module>
    import torch_optimizer as custom_optim
ModuleNotFoundError: No module named 'torch_optimizer'
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt#
```

Yes, I will install torch_optimizer library ...  

```
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# pip install torch_optimizer
Collecting torch_optimizer
  Using cached torch_optimizer-0.3.0-py3-none-any.whl (61 kB)
Requirement already satisfied: torch>=1.5.0 in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch_optimizer) (1.10.2)
Collecting pytorch-ranger>=0.1.1
  Using cached pytorch_ranger-0.1.1-py3-none-any.whl (14 kB)
Requirement already satisfied: typing-extensions in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch>=1.5.0->torch_optimizer) (4.1.1)
Requirement already satisfied: dataclasses in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch>=1.5.0->torch_optimizer) (0.8)
Installing collected packages: pytorch-ranger, torch-optimizer
Successfully installed pytorch-ranger-0.1.1 torch-optimizer-0.3.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt#
```

run train.py again ...  

```
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# python ./train.py
/root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages/torch/package/_directory_reader.py:17: UserWarning: Failed to initialize NumPy: numpy.core.multiarray failed to import (Triggered internally at  ../torch/csrc/utils/tensor_numpy.cpp:68.)
  _dtype_to_storage = {data_type(0).dtype: data_type for data_type in _storages}
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 3, in <module>
    import torchtext
ModuleNotFoundError: No module named 'torchtext'
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt#
```

OK! I will install torchtext library ...  

```
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# pip install torchtext
...
...
...
Collecting requests
  Downloading requests-2.27.1-py2.py3-none-any.whl (63 kB)
     |################################| 63 kB 4.9 MB/s
Requirement already satisfied: torch==1.10.2 in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torchtext) (1.10.2)
Collecting numpy
  Downloading numpy-1.19.5-cp36-cp36m-manylinux2010_x86_64.whl (14.8 MB)
     |################################| 14.8 MB 99.4 MB/s
Requirement already satisfied: typing-extensions in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch==1.10.2->torchtext) (4.1.1)
Requirement already satisfied: dataclasses in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch==1.10.2->torchtext) (0.8)
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.13-py2.py3-none-any.whl (140 kB)
     |################################| 140 kB 94.5 MB/s
Requirement already satisfied: certifi>=2017.4.17 in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from requests->torchtext) (2021.5.30)
Collecting idna<4,>=2.5
  Downloading idna-3.4-py3-none-any.whl (61 kB)
     |################################| 61 kB 324 kB/s
Collecting charset-normalizer~=2.0.0
  Downloading charset_normalizer-2.0.12-py3-none-any.whl (39 kB)
Collecting importlib-resources
  Downloading importlib_resources-5.4.0-py3-none-any.whl (28 kB)
Collecting zipp>=3.1.0
  Downloading zipp-3.6.0-py3-none-any.whl (5.3 kB)
Installing collected packages: zipp, urllib3, importlib-resources, idna, charset-normalizer, tqdm, requests, numpy, torchtext
Successfully installed charset-normalizer-2.0.12 idna-3.4 importlib-resources-5.4.0 numpy-1.19.5 requests-2.27.1 torchtext-0.11.2 tqdm-4.64.1 urllib3-1.26.13 zipp-3.6.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
```

run train.py again ...  

```
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# python ./train.py
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 92, in <module>
    class TranslationDataset(data.Dataset):
AttributeError: module 'torchtext.data' has no attribute 'Dataset'
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt#
```

Oh! No ...  I install pytorch-ignite  

```
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# pip install pytorch-ignite
Collecting pytorch-ignite
  Downloading pytorch_ignite-0.4.10-py3-none-any.whl (264 kB)
     |################################| 264 kB 2.2 MB/s
Collecting packaging
  Downloading packaging-21.3-py3-none-any.whl (40 kB)
     |################################| 40 kB 14.3 MB/s
Requirement already satisfied: torch<2,>=1.3 in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from pytorch-ignite) (1.10.2)
Requirement already satisfied: dataclasses in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch<2,>=1.3->pytorch-ignite) (0.8)
Requirement already satisfied: typing-extensions in /root/anaconda3/envs/simple-nmt/lib/python3.6/site-packages (from torch<2,>=1.3->pytorch-ignite) (4.1.1)
Collecting pyparsing!=3.0.5,>=2.0.2
  Downloading pyparsing-3.0.9-py3-none-any.whl (98 kB)
     |################################| 98 kB 18.3 MB/s
Installing collected packages: pyparsing, packaging, pytorch-ignite
Successfully installed packaging-21.3 pyparsing-3.0.9 pytorch-ignite-0.4.10
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt#
```

run train.py again ...  and got same error ...  

```
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt# python ./train.py
Traceback (most recent call last):
  File "./train.py", line 10, in <module>
    from simple_nmt.data_loader import DataLoader
  File "/home/ye/tool/simple-nmt/simple_nmt/data_loader.py", line 92, in <module>
    class TranslationDataset(data.Dataset):
AttributeError: module 'torchtext.data' has no attribute 'Dataset'
(simple-nmt) root@428d4e81f922:/home/ye/tool/simple-nmt#
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
