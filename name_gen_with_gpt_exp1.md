# Myanmar Name Generation with Simple GPT Model Experiment

Run by Ye, LU Lab., Myanmar.
Last updated: 16 Jan 2025

## Error for 1st Run

(bi_lstm_ner) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/bi_lstm_ner/bin/python ./gpt_lm.py --help
Traceback (most recent call last):
  File "./gpt_lm.py", line 1, in <module>
    import torch
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/torch-2.4.1-py3.8-linux-x86_64.egg/torch/__init__.py", line 31, in <module>
    from ._utils import _import_dotted_name, classproperty
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/torch-2.4.1-py3.8-linux-x86_64.egg/torch/_utils.py", line 11, in <module>
    from typing_extensions import ParamSpec
ImportError: cannot import name 'ParamSpec' from 'typing_extensions' (/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/typing_extensions.py)
(bi_lstm_ner) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Update typing_extensions

(bi_lstm_ner) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/bi_lstm_ner/bin/python -m pip install --upgrade typing_extensions
Requirement already satisfied: typing_extensions in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages (3.7.4.3)
Collecting typing_extensions
  Using cached typing_extensions-4.12.2-py3-none-any.whl.metadata (3.0 kB)
Using cached typing_extensions-4.12.2-py3-none-any.whl (37 kB)
Installing collected packages: typing_extensions
  Attempting uninstall: typing_extensions
    Found existing installation: typing-extensions 3.7.4.3
    Uninstalling typing-extensions-3.7.4.3:
      Successfully uninstalled typing-extensions-3.7.4.3
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
tensorflow-gpu 2.5.0 requires numpy~=1.19.2, but you have numpy 1.23.0 which is incompatible.
tensorflow-gpu 2.5.0 requires typing-extensions~=3.7.4, but you have typing-extensions 4.12.2 which is incompatible.
Successfully installed typing_extensions-4.12.2
(bi_lstm_ner) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Try Again

(bi_lstm_ner) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/bi_lstm_ner/bin/python ./gpt_lm.py --help
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/torch-2.4.1-py3.8-linux-x86_64.egg/torch/__init__.py", line 226, in _load_global_deps
    ctypes.CDLL(global_deps_lib_path, mode=ctypes.RTLD_GLOBAL)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/ctypes/__init__.py", line 373, in __init__
    self._handle = _dlopen(self._name, mode)
OSError: libcudart.so.12: cannot open shared object file: No such file or directory

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "./gpt_lm.py", line 1, in <module>
    import torch
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/torch-2.4.1-py3.8-linux-x86_64.egg/torch/__init__.py", line 289, in <module>
    _load_global_deps()
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/torch-2.4.1-py3.8-linux-x86_64.egg/torch/__init__.py", line 247, in _load_global_deps
    _preload_cuda_deps(lib_folder, lib_name)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/torch-2.4.1-py3.8-linux-x86_64.egg/torch/__init__.py", line 170, in _preload_cuda_deps
    ctypes.CDLL(lib_path)
  File "/home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/ctypes/__init__.py", line 373, in __init__
    self._handle = _dlopen(self._name, mode)
OSError: libnvJitLink.so.12: cannot open shared object file: No such file or directory
(bi_lstm_ner) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$


## Switch Conda Env and Uninstall/Install Pytorch


Switched to hs-fasttext env and uninstall/install pytorch:

/home/ye/anaconda3/envs/bi_lstm_ner/bin/python -m pip uninstall torch
/home/ye/anaconda3/envs/bi_lstm_ner/bin/python -m pip install torch

3.8/site-packages/nvidia_nccl_cu12-2.20.5-py3.8-linux-x86_64.egg (from torch) (2.20.5)
Requirement already satisfied: nvidia-nvtx-cu12==12.1.105 in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/nvidia_nvtx_cu12-12.1.105-py3.8-linux-x86_64.egg (from torch) (12.1.105)
Requirement already satisfied: triton==3.0.0 in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/triton-3.0.0-py3.8-linux-x86_64.egg (from torch) (3.0.0)
Requirement already satisfied: nvidia-nvjitlink-cu12 in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/nvidia_nvjitlink_cu12-12.6.85-py3.8-linux-x86_64.egg (from nvidia-cusolver-cu12==11.4.5.107->torch) (12.6.85)
Requirement already satisfied: MarkupSafe>=2.0 in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages (from jinja2->torch) (2.1.5)
Requirement already satisfied: mpmath<1.4,>=1.1.0 in /home/ye/anaconda3/envs/bi_lstm_ner/lib/python3.8/site-packages/mpmath-1.3.0-py3.8.egg (from sympy->torch) (1.3.0)
Using cached torch-2.4.1-cp38-cp38-manylinux1_x86_64.whl (797.1 MB)
Installing collected packages: torch
Successfully installed torch-2.4.1
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Try Again


Traceback (most recent call last):  File "/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py", line 1, in <module>
    import torch
  File "/home/ye/.local/lib/python3.10/site-packages/torch/__init__.py", line 1471, in <module>
    from .functional import *  # noqa: F403
  File "/home/ye/.local/lib/python3.10/site-packages/torch/functional.py", line 9, in <module>
    import torch.nn.functional as F
  File "/home/ye/.local/lib/python3.10/site-packages/torch/nn/__init__.py", line 1, in <module>
    from .modules import *  # noqa: F403
  File "/home/ye/.local/lib/python3.10/site-packages/torch/nn/modules/__init__.py", line 35, in <module>
    from .transformer import TransformerEncoder, TransformerDecoder, \
  File "/home/ye/.local/lib/python3.10/site-packages/torch/nn/modules/transformer.py", line 20, in <module>
    device: torch.device = torch.device(torch._C._get_default_device()),  # torch.device('cpu'),
/home/ye/.local/lib/python3.10/site-packages/torch/nn/modules/transformer.py:20: UserWarning: Failed to initialize NumPy: _ARRAY_API not found (Triggered internally at ../torch/csrc/utils/tensor_numpy.cpp:84.)
  device: torch.device = torch.device(torch._C._get_default_device()),  # torch.device('cpu'),
usage: gpt_lm.py [-h] [--train] [--generate] [--data DATA] [--model MODEL] [--prompt PROMPT]
                 [--seq_len SEQ_LEN] [--epochs EPOCHS] [--batch_size BATCH_SIZE] [--lr LR]
                 [--embed_dim EMBED_DIM] [--num_heads NUM_HEADS] [--num_layers NUM_LAYERS]
                 [--ff_dim FF_DIM]

Train and generate text using GPT.

options:
  -h, --help            show this help message and exit
  --train               Train the GPT model.
  --generate            Generate text.
  --data DATA           Path to the dataset.
  --model MODEL         Path to save/load the model.
  --prompt PROMPT       Prompt for text generation.
  --seq_len SEQ_LEN     Sequence length.
  --epochs EPOCHS       Number of training epochs.
  --batch_size BATCH_SIZE
                        Batch size.
  --lr LR               Learning rate.
  --embed_dim EMBED_DIM
                        Embedding dimension.
  --num_heads NUM_HEADS
                        Number of attention heads.
  --num_layers NUM_LAYERS
                        Number of transformer layers.
  --ff_dim FF_DIM       Feedforward dimension.
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Uninstall/Install Numpy

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/hs-fasttext/bin/python
-m pip uninstall numpy
Found existing installation: numpy 2.2.1
Uninstalling numpy-2.2.1:
  Would remove:
    /home/ye/.local/bin/f2py
    /home/ye/.local/bin/numpy-config
    /home/ye/.local/lib/python3.10/site-packages/numpy-2.2.1.dist-info/*
    /home/ye/.local/lib/python3.10/site-packages/numpy.libs/libgfortran-040039e1-0352e75f.so.5.0.0
    /home/ye/.local/lib/python3.10/site-packages/numpy.libs/libquadmath-96973f99-934c22de.so.0.0.0
    /home/ye/.local/lib/python3.10/site-packages/numpy.libs/libscipy_openblas64_-6bb31eeb.so
    /home/ye/.local/lib/python3.10/site-packages/numpy/*
Proceed (Y/n)? Y
  Successfully uninstalled numpy-2.2.1
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/hs-fasttext/bin/python -m pip install numpy --force-reinstall
Collecting numpy
  Using cached numpy-2.2.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (62 kB)
Using cached numpy-2.2.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.4 MB)
Installing collected packages: numpy
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
music21 9.1.0 requires chardet, which is not installed.
sacrebleu 2.4.0 requires colorama, which is not installed.
contourpy 1.2.0 requires numpy<2.0,>=1.20, but you have numpy 2.2.1 which is incompatible.
matplotlib 3.8.3 requires numpy<2,>=1.21, but you have numpy 2.2.1 which is incompatible.
mytokenize 0.1.1 requires tensorflow==2.13, but you have tensorflow 2.18.0 which is incompatible.
numba 0.60.0 requires numpy<2.1,>=1.22, but you have numpy 2.2.1 which is incompatible.
pandas 2.2.0 requires numpy<2,>=1.22.4; python_version < "3.11", but you have numpy 2.2.1 which is incompatible.
pyarrow 15.0.0 requires numpy<2,>=1.16.6, but you have numpy 2.2.1 which is incompatible.
scikit-learn 1.4.1.post1 requires numpy<2.0,>=1.19.5, but you have numpy 2.2.1 which is incompatible.
scipy 1.12.0 requires numpy<1.29.0,>=1.22.4, but you have numpy 2.2.1 which is incompatible.
tensorflow 2.18.0 requires numpy<2.1.0,>=1.26.0, but you have numpy 2.2.1 which is incompatible.
transformer-smaller-training-vocab 0.4.0 requires numpy<2.0.0,>=1.21.0; python_version >= "3.9", but you have numpy 2.2.1 which is incompatible.
Successfully installed numpy-2.2.1
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Try Again

Still facing error and decided to uninstall/install torch.
What I mean I wanna use new numpy.  

## Uninstall/Install Torch


(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/hs-fasttext/bin/python -m pip install torch
...
...
      Successfully uninstalled nvidia-cuda-cupti-cu12-12.1.105
  Attempting uninstall: nvidia-cublas-cu12
    Found existing installation: nvidia-cublas-cu12 12.1.3.1
    Uninstalling nvidia-cublas-cu12-12.1.3.1:
      Successfully uninstalled nvidia-cublas-cu12-12.1.3.1
  Attempting uninstall: nvidia-cusparse-cu12
    Found existing installation: nvidia-cusparse-cu12 12.1.0.106
    Uninstalling nvidia-cusparse-cu12-12.1.0.106:
      Successfully uninstalled nvidia-cusparse-cu12-12.1.0.106
  Attempting uninstall: nvidia-cudnn-cu12
    Found existing installation: nvidia-cudnn-cu12 8.9.2.26
    Uninstalling nvidia-cudnn-cu12-8.9.2.26:
      Successfully uninstalled nvidia-cudnn-cu12-8.9.2.26
  Attempting uninstall: nvidia-cusolver-cu12
    Found existing installation: nvidia-cusolver-cu12 11.4.5.107
    Uninstalling nvidia-cusolver-cu12-11.4.5.107:
      Successfully uninstalled nvidia-cusolver-cu12-11.4.5.107
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
transformer-smaller-training-vocab 0.4.0 requires numpy<2.0.0,>=1.21.0; python_version >= "3.9", but you have numpy 2.2.1 which is incompatible.
Successfully installed nvidia-cublas-cu12-12.4.5.8 nvidia-cuda-cupti-cu12-12.4.127 nvidia-cuda-nvrtc-cu12-12.4.127 nvidia-cuda-runtime-cu12-12.4.127 nvidia-cudnn-cu12-9.1.0.70 nvidia-cufft-cu12-11.2.1.3 nvidia-curand-cu12-10.3.5.147 nvidia-cusolver-cu12-11.6.1.9 nvidia-cusparse-cu12-12.3.1.170 nvidia-nccl-cu12-2.21.5 nvidia-nvjitlink-cu12-12.4.127 nvidia-nvtx-cu12-12.4.127 sympy-1.13.1 torch-2.5.1 triton-3.1.0
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$


## Check Installed numpy and torch

Finally, I got it!

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/hs-fasttext/bin/python  -c "import numpy; print(numpy.__version__)"
2.2.1
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ /home/ye/anaconda3/envs/hs-fasttext/bin/python  -c "import torch; print(torch.__version__)"
2.5.1+cu124
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Run Again

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ python ./gpt_lm.py --help
usage: gpt_lm.py [-h] [--train] [--generate] [--data DATA] [--model MODEL] [--prompt PROMPT]
                 [--seq_len SEQ_LEN] [--epochs EPOCHS] [--batch_size BATCH_SIZE] [--lr LR]
                 [--embed_dim EMBED_DIM] [--num_heads NUM_HEADS] [--num_layers NUM_LAYERS]
                 [--ff_dim FF_DIM]

Train and generate text using GPT.

options:
  -h, --help            show this help message and exit
  --train               Train the GPT model.
  --generate            Generate text.
  --data DATA           Path to the dataset.
  --model MODEL         Path to save/load the model.
  --prompt PROMPT       Prompt for text generation.
  --seq_len SEQ_LEN     Sequence length.
  --epochs EPOCHS       Number of training epochs.
  --batch_size BATCH_SIZE
                        Batch size.
  --lr LR               Learning rate.
  --embed_dim EMBED_DIM
                        Embedding dimension.
  --num_heads NUM_HEADS
                        Number of attention heads.
  --num_layers NUM_LAYERS
                        Number of transformer layers.
  --ff_dim FF_DIM       Feedforward dimension.
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$


## Training

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --train --data ../data/train/train.txt --model ./model/gpt.model
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
Epoch 1/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:10<00:00, 12.04it/s]
Epoch 1, Loss: 0.3045
Epoch 2/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:11<00:00, 11.98it/s]
Epoch 2, Loss: 0.2053
Epoch 3/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:10<00:00, 12.08it/s]
Epoch 3, Loss: 0.1919
Epoch 4/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:10<00:00, 12.07it/s]
Epoch 4, Loss: 0.1852
Epoch 5/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:10<00:00, 12.13it/s]
Epoch 5, Loss: 0.1808
Epoch 6/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:09<00:00, 12.33it/s]
Epoch 6, Loss: 0.1773
Epoch 7/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:10<00:00, 12.15it/s]
Epoch 7, Loss: 0.1745
Epoch 8/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:08<00:00, 12.41it/s]
Epoch 8, Loss: 0.1720
Epoch 9/10: 100%|██████████████████████████████████████████████████████| 852/852 [01:10<00:00, 12.08it/s]
Epoch 9, Loss: 0.1699
Epoch 10/10: 100%|█████████████████████████████████████████████████████| 852/852 [01:08<00:00, 12.36it/s]
Epoch 10, Loss: 0.1680

real    11m44.086s
user    183m38.505s
sys     2m15.577s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

Check the output model and vocab files:  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ ls ./model/ -lh
total 11M
-rw-rw-r-- 1 ye ye 11M Jan 15 14:56 gpt.model
-rw-rw-r-- 1 ye ye 25K Jan 15 14:45 gpt.model.vocab
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ file ./model/*
./model/gpt.model:       Zip archive data, at least v0.0 to extract, compression method=store
./model/gpt.model.vocab: Unicode text, UTF-8 text
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ head ./model/gpt.model.vocab
ထိပ်    0
ခေတ်    1
မှုံ    2
ကြော့   3
ရင်     4
မိန်း   5
ဂူ      6
ဖုန်    7
ဘွား    8
ဒေါ်    9
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ tail ./model/gpt.model.vocab
ဒုလ်    1441
သဉ္ဇူ   1442
နွန်း   1443
ကိန္န   1444
ဆွန်    1445
ကော်    1446
မို     1447
ဂျာလ်   1448
ကျိန်း  1449
ဖော်    1450
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ wc ./model/gpt.model.vocab
 1451  2902 24737 ./model/gpt.model.vocab
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Debugging on Generation

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 2 --prompt မောင်
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:227: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: မောင် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ် ထိပ်

real    0m2.319s
user    0m7.350s
sys     0m0.240s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 2 --prompt "မောင်"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:221: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: မောင် ထိပ် ထိပ်

real    0m2.219s
user    0m5.695s
sys     0m0.208s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "မောင်"

time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "လှ"

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "လှ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:221: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: လှ နိုင် ဝေ ရီ လှိုင် ထိပ်

real    0m2.223s
user    0m5.799s
sys     0m0.232s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ဆွေ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:221: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: ဆွေ ထိပ် ထိပ် ထိပ် ထိပ် ထိပ်

real    0m2.227s
user    0m5.831s
sys     0m0.205s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "အေး"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:221: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: အေး ထိပ် ထိပ် ထိပ် ထိပ် ထိပ်

real    0m2.242s
user    0m5.822s
sys     0m0.225s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ဆွေ ဆွေ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:221: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: ဆွေ ဆွေ ထိပ် ထိပ် ထိပ် ထိပ် ထိပ်

real    0m2.217s
user    0m5.787s
sys     0m0.245s

time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ဆွေ"

===========

အထက်ပါ ကိစ္စမှာ debugging လုပ်ရတာ တော်တော် အချိန်ပေးလိုက်ရတယ်။  

ရလဒ်က မကောင်းလို့ model ရဲ့ checkpoint သိမ်းတဲ့ parameter တွေကို ပြင်၊ tokenization အပိုင်းကိုလည်း generation လုပ်တဲ့အပိုင်းမှာပါ ညီအောင်ညှိ၊ generation မလုပ်ခင်လည်း မော်ဒယ် loading အပိုင်းကိုလည်း ပြင်တာတွေလုပ်ပြီးမှ နောက်ဆုံး ရလဒ်ကောင်းလာတယ်။ အောက်ပါအတိုင်း...  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ဆွေ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:251: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
dict_keys(['model_state_dict', 'token_to_id', 'id_to_token', 'embed_dim', 'num_heads', 'num_layers', 'ff_dim', 'seq_len'])
Generated Text: ဆွေ ဆွန်း ဘို နည် ဘက် မာ့

real    0m2.245s
user    0m6.100s
sys     0m0.243s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ဆွေ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:251: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
dict_keys(['model_state_dict', 'token_to_id', 'id_to_token', 'embed_dim', 'num_heads', 'num_layers', 'ff_dim', 'seq_len'])
Generated Text: ဆွေ ဘန့် ချမ်း မဲန် အာဖ် လှေး

real    0m2.259s
user    0m6.135s
sys     0m0.215s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ရဲ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:251: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
dict_keys(['model_state_dict', 'token_to_id', 'id_to_token', 'embed_dim', 'num_heads', 'num_layers', 'ff_dim', 'seq_len'])
Generated Text: ရဲ နီ ကာ ဖြိုး မိုး ဘုတ်

real    0m2.262s
user    0m6.082s
sys     0m0.255s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 1 3 --prompt "ရဲ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:251: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
dict_keys(['model_state_dict', 'token_to_id', 'id_to_token', 'embed_dim', 'num_heads', 'num_layers', 'ff_dim', 'seq_len'])
Generated Text: ရဲ ငိုက် ငြိမ့် ရိုင်

real    0m2.235s
user    0m5.984s
sys     0m0.220s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 1 --prompt "ရဲ ကျော်"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:251: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
dict_keys(['model_state_dict', 'token_to_id', 'id_to_token', 'embed_dim', 'num_heads', 'num_layers', 'ff_dim', 'seq_len'])
Generated Text: ရဲ ကျော် ကျုံး

real    0m2.227s
user    0m5.718s
sys     0m0.221s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 31 --prompt "ရဲ ကျော်"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:251: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
dict_keys(['model_state_dict', 'token_to_id', 'id_to_token', 'embed_dim', 'num_heads', 'num_layers', 'ff_dim', 'seq_len'])
Generated Text: ရဲ ကျော် ပူး

real    0m2.197s
user    0m5.619s
sys     0m0.201s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

## Current Version 

the 1st version for working both gpt model building and text generation:  

import torch
import torch.nn as nn
from torch.utils.data import DataLoader, Dataset
import argparse
import numpy as np
import os
from tqdm import tqdm

# Tokenizer for the Burmese language
class Tokenizer:
    def __init__(self):
        self.token_to_id = {}
        self.id_to_token = {}

    def fit(self, texts):
        tokens = set()
        for text in texts:
            tokens.update(text.split())
        self.token_to_id = {token: idx for idx, token in enumerate(tokens)}
        self.id_to_token = {idx: token for token, idx in self.token_to_id.items()}

    def encode(self, text, return_tensors=None):
        ids = [self.token_to_id.get(token, -1) for token in text.split()]
        if -1 in ids:
            raise ValueError("Some tokens are not in the vocabulary.")
        if return_tensors == "pt":
            return torch.tensor(ids, dtype=torch.long).unsqueeze(0)
        return ids

    def decode(self, ids):
        return ' '.join([self.id_to_token[i] for i in ids])

# Dataset class
class BurmeseDataset(Dataset):
    def __init__(self, texts, tokenizer, seq_len):
        self.tokenizer = tokenizer
        self.seq_len = seq_len
        self.texts = [tokenizer.encode(text) for text in texts]

    def __len__(self):
        return len(self.texts)

    def __getitem__(self, idx):
        text = self.texts[idx]
        input_ids = text[:-1]
        target_ids = text[1:]
        if len(input_ids) < self.seq_len:
            pad_len = self.seq_len - len(input_ids)
            input_ids = [0] * pad_len + input_ids
            target_ids = [0] * pad_len + target_ids
        return torch.tensor(input_ids), torch.tensor(target_ids)

# Transformer Block
class TransformerBlock(nn.Module):
    def __init__(self, embed_dim, num_heads, ff_dim, dropout=0.1):
        super(TransformerBlock, self).__init__()
        self.attention = nn.MultiheadAttention(embed_dim, num_heads, dropout=dropout)
        self.norm1 = nn.LayerNorm(embed_dim)
        self.ff = nn.Sequential(
            nn.Linear(embed_dim, ff_dim),
            nn.ReLU(),
            nn.Linear(ff_dim, embed_dim)
        )
        self.norm2 = nn.LayerNorm(embed_dim)
        self.dropout = nn.Dropout(dropout)

    def forward(self, x):
        # Multi-head self-attention
        attn_output, _ = self.attention(x, x, x)
        x = self.norm1(x + self.dropout(attn_output))  # Add & Norm

        # Feedforward layer
        ff_output = self.ff(x)
        x = self.norm2(x + self.dropout(ff_output))  # Add & Norm

        return x

# Transformer-based GPT Model
class GPT(nn.Module):
    def __init__(self, vocab_size, embed_dim, num_heads, num_layers, ff_dim, seq_len):
        super(GPT, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embed_dim)
        self.position_embedding = nn.Embedding(seq_len, embed_dim)
        self.transformer_blocks = nn.ModuleList([
            TransformerBlock(embed_dim, num_heads, ff_dim) for _ in range(num_layers)
        ])
        self.fc_out = nn.Linear(embed_dim, vocab_size)

    def forward(self, x):
        seq_len = x.size(1)
        positions = torch.arange(0, seq_len).unsqueeze(0).to(x.device)
        x = self.embedding(x) + self.position_embedding(positions)
        for transformer in self.transformer_blocks:
            x = transformer(x)
        return self.fc_out(x)

    def generate(self, input_ids, max_length, temperature=1.0, top_k=None, top_p=None):
        self.eval()
        generated = input_ids.clone()
        for _ in range(max_length):
            outputs = self.forward(generated)
            logits = outputs[:, -1, :]  # Get logits of the last token
            logits = logits / temperature
        
            # Check for NaN or Inf in logits
            if torch.any(torch.isnan(logits)) or torch.any(torch.isinf(logits)):
                raise ValueError("Logits contain NaN or Inf values.")

            if top_k:
                # Apply top-k filtering
                values, _ = torch.topk(logits, top_k)
                min_values = values[:, -1].unsqueeze(-1)
                logits[logits < min_values] = -float('Inf')
        
            if top_p:
                sorted_logits, sorted_indices = torch.sort(logits, descending=True)
                cumulative_probs = torch.cumsum(torch.nn.functional.softmax(sorted_logits, dim=-1), dim=-1)
                sorted_indices_to_remove = cumulative_probs > top_p
                sorted_logits[sorted_indices_to_remove] = -float('Inf')
                logits = torch.gather(sorted_logits, -1, sorted_indices)
        
            # Ensure the logits are valid after filtering
            if torch.any(torch.isnan(logits)) or torch.any(torch.isinf(logits)):
                logits = torch.zeros_like(logits)  # Replace invalid logits with zeros

            probabilities = torch.nn.functional.softmax(logits, dim=-1)
        
            # Check if any probability values are invalid
            if torch.any(torch.isnan(probabilities)) or torch.any(torch.isinf(probabilities)):
                raise ValueError("Probabilities contain NaN or Inf values.")
        
            next_token = torch.multinomial(probabilities, num_samples=1)
            generated = torch.cat((generated, next_token), dim=1)
    
        return generated


# Training Function
def train_model(model, dataset, epochs, batch_size, lr, device):
    dataloader = DataLoader(dataset, batch_size=batch_size, shuffle=True)
    optimizer = torch.optim.Adam(model.parameters(), lr=lr)
    criterion = nn.CrossEntropyLoss()
    model.to(device)

    for epoch in range(epochs):
        model.train()
        epoch_loss = 0
        for inputs, targets in tqdm(dataloader, desc=f"Epoch {epoch+1}/{epochs}"):
            inputs, targets = inputs.to(device), targets.to(device)
            outputs = model(inputs)
            outputs = outputs.view(-1, outputs.size(-1))
            targets = targets.view(-1)
            loss = criterion(outputs, targets)
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()
            epoch_loss += loss.item()
        print(f"Epoch {epoch+1}, Loss: {epoch_loss / len(dataloader):.4f}")

    def generate(self, input_ids, max_length, temperature=1.0, top_k=None, top_p=0.9):
        self.eval()
        generated = input_ids.clone()
        for _ in range(max_length):
            outputs = self.forward(generated)
            logits = outputs[:, -1, :]  # Get logits of the last token
            logits = logits / temperature
            
            if top_k:
                values, _ = torch.topk(logits, top_k)
                min_values = values[:, -1].unsqueeze(-1)
                logits[logits < min_values] = -float('Inf')
            
            if top_p:
                sorted_logits, sorted_indices = torch.sort(logits, descending=True)
                cumulative_probs = torch.cumsum(torch.nn.functional.softmax(sorted_logits, dim=-1), dim=-1)
                sorted_indices_to_remove = cumulative_probs > top_p
                sorted_logits[sorted_indices_to_remove] = -float('Inf')
                logits = torch.gather(sorted_logits, -1, sorted_indices)
            
            probabilities = torch.nn.functional.softmax(logits, dim=-1)
            next_token = torch.multinomial(probabilities, num_samples=1)
            generated = torch.cat((generated, next_token), dim=1)
        return generated

# Main Function
def main():
    parser = argparse.ArgumentParser(description="Train and generate text using GPT.")
    parser.add_argument("--train", action="store_true", help="Train the GPT model.")
    parser.add_argument("--generate", action="store_true", help="Generate text.")
    parser.add_argument("--data", type=str, help="Path to the dataset.")
    parser.add_argument("--model", type=str, help="Path to save/load the model.")
    parser.add_argument("--prompt", type=str, default="", help="Prompt for text generation.")
    parser.add_argument("--seq_len", type=int, default=50, help="Sequence length.")
    parser.add_argument("--epochs", type=int, default=10, help="Number of training epochs.")
    parser.add_argument("--batch_size", type=int, default=32, help="Batch size.")
    parser.add_argument("--lr", type=float, default=1e-4, help="Learning rate.")
    parser.add_argument("--embed_dim", type=int, default=256, help="Embedding dimension.")
    parser.add_argument("--num_heads", type=int, default=4, help="Number of attention heads.")
    parser.add_argument("--num_layers", type=int, default=4, help="Number of transformer layers.")
    parser.add_argument("--ff_dim", type=int, default=512, help="Feedforward dimension.")
    ## following arguments are for --generate mode
    parser.add_argument("--temperature", type=float, default=1.0, help="Sampling temperature (higher = more random).")
    parser.add_argument("--top_k", type=int, default=30, help="Top-k sampling.")
    parser.add_argument("--top_p", type=float, default=0.9, help="Top-p (nucleus) sampling.")

    args = parser.parse_args()

    device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

    if args.train:
        # Load dataset
        with open(args.data, "r", encoding="utf-8") as f:
            texts = f.read().splitlines()

        tokenizer = Tokenizer()
        tokenizer.fit(texts)

        dataset = BurmeseDataset(texts, tokenizer, args.seq_len)

        # Save tokenizer information
        with open(args.model + ".vocab", "w", encoding="utf-8") as vocab_file:
            for token, idx in tokenizer.token_to_id.items():
                vocab_file.write(f"{token}\t{idx}\n")

        # Initialize model
        model = GPT(len(tokenizer.token_to_id), args.embed_dim, args.num_heads, args.num_layers, args.ff_dim, args.seq_len)

        train_model(model, dataset, args.epochs, args.batch_size, args.lr, device)
        # Save the model and tokenizer
        checkpoint = {
            "model_state_dict": model.state_dict(),
            "token_to_id": tokenizer.token_to_id,
            "id_to_token": tokenizer.id_to_token,
            "embed_dim": args.embed_dim,
            "num_heads": args.num_heads,
            "num_layers": args.num_layers,
            "ff_dim": args.ff_dim,
            "seq_len": args.seq_len,
        }

        torch.save(checkpoint, args.model)

    if args.generate:
        if not args.model:
            raise ValueError("Model path must be specified for generation mode.")

        if not args.prompt:
            raise ValueError("Prompt must be specified for generation mode.")

        # Load the model
        checkpoint = torch.load(args.model)
        print(checkpoint.keys()) 
        tokenizer = Tokenizer()
        tokenizer.token_to_id = checkpoint["token_to_id"]
        tokenizer.id_to_token = checkpoint["id_to_token"]
        model = GPT(
            vocab_size=len(tokenizer.token_to_id),
            embed_dim=checkpoint["embed_dim"],
            num_heads=checkpoint["num_heads"],
            num_layers=checkpoint["num_layers"],
            ff_dim=checkpoint["ff_dim"],
            seq_len=checkpoint["seq_len"],
        )
        model.load_state_dict(checkpoint["model_state_dict"])
        model.to(device)

        # Restore tokenizer state
        tokenizer = Tokenizer()
        tokenizer.token_to_id = checkpoint["token_to_id"]
        tokenizer.id_to_token = checkpoint["id_to_token"]

        # Encode the prompt
        try:
            input_ids = tokenizer.encode(args.prompt, return_tensors="pt").to(device)
            output_ids = model.generate(input_ids, max_length=args.seq_len, temperature=args.temperature, top_k=args.top_k)
        except ValueError as e:
            raise ValueError(f"Error in encoding prompt: {e}")

        # Generate text
        generated_ids = model.generate(
            input_ids,
            max_length=args.seq_len,
            temperature=args.temperature,
            top_k=args.top_k,
            top_p=args.top_p,
        )
        generated_text = tokenizer.decode(generated_ids.squeeze().tolist())
        print(f"Generated Text: {generated_text}")


if __name__ == "__main__":
    main()

## --help of Current Code

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ python ./gpt_lm.py --help
usage: gpt_lm.py [-h] [--train] [--generate] [--data DATA] [--model MODEL] [--prompt PROMPT]
                 [--seq_len SEQ_LEN] [--epochs EPOCHS] [--batch_size BATCH_SIZE] [--lr LR]
                 [--embed_dim EMBED_DIM] [--num_heads NUM_HEADS] [--num_layers NUM_LAYERS]
                 [--ff_dim FF_DIM] [--temperature TEMPERATURE] [--top_k TOP_K] [--top_p TOP_P]

Train and generate text using GPT.

options:
  -h, --help            show this help message and exit
  --train               Train the GPT model.
  --generate            Generate text.
  --data DATA           Path to the dataset.
  --model MODEL         Path to save/load the model.
  --prompt PROMPT       Prompt for text generation.
  --seq_len SEQ_LEN     Sequence length.
  --epochs EPOCHS       Number of training epochs.
  --batch_size BATCH_SIZE
                        Batch size.
  --lr LR               Learning rate.
  --embed_dim EMBED_DIM
                        Embedding dimension.
  --num_heads NUM_HEADS
                        Number of attention heads.
  --num_layers NUM_LAYERS
                        Number of transformer layers.
  --ff_dim FF_DIM       Feedforward dimension.
  --temperature TEMPERATURE
                        Sampling temperature (higher = more random).
  --top_k TOP_K         Top-k sampling.
  --top_p TOP_P         Top-p (nucleus) sampling.

## Code Updating

I updated the code for running without --prompt (i.e. random) 
and --output (for saving generated text into a file)

import torch
import torch.nn as nn
from torch.utils.data import DataLoader, Dataset
import argparse
import numpy as np
import os
from tqdm import tqdm
import random

# Tokenizer for the Burmese language
class Tokenizer:
    def __init__(self):
        self.token_to_id = {}
        self.id_to_token = {}

    def fit(self, texts):
        tokens = set()
        for text in texts:
            tokens.update(text.split())
        tokens.add("[UNK]")  # Add unknown token
        self.token_to_id = {token: idx for idx, token in enumerate(tokens)}
        self.id_to_token = {idx: token for token, idx in self.token_to_id.items()}

    def encode(self, text, return_tensors=None):
        ids = [self.token_to_id.get(token, self.token_to_id["[UNK]"]) for token in text.split()]
        if return_tensors == "pt":
            return torch.tensor(ids, dtype=torch.long).unsqueeze(0)
        return ids

    def decode(self, ids):
        return ' '.join([self.id_to_token[i] for i in ids])

# Dataset class
class BurmeseDataset(Dataset):
    def __init__(self, texts, tokenizer, seq_len):
        self.tokenizer = tokenizer
        self.seq_len = seq_len
        self.texts = [tokenizer.encode(text) for text in texts]

    def __len__(self):
        return len(self.texts)

    def __getitem__(self, idx):
        text = self.texts[idx]
        input_ids = text[:-1]
        target_ids = text[1:]
        if len(input_ids) < self.seq_len:
            pad_len = self.seq_len - len(input_ids)
            input_ids = [0] * pad_len + input_ids
            target_ids = [0] * pad_len + target_ids
        return torch.tensor(input_ids), torch.tensor(target_ids)

# Transformer Block
class TransformerBlock(nn.Module):
    def __init__(self, embed_dim, num_heads, ff_dim, dropout=0.1):
        super(TransformerBlock, self).__init__()
        self.attention = nn.MultiheadAttention(embed_dim, num_heads, dropout=dropout)
        self.norm1 = nn.LayerNorm(embed_dim)
        self.ff = nn.Sequential(
            nn.Linear(embed_dim, ff_dim),
            nn.ReLU(),
            nn.Linear(ff_dim, embed_dim)
        )
        self.norm2 = nn.LayerNorm(embed_dim)
        self.dropout = nn.Dropout(dropout)

    def forward(self, x):
        # Multi-head self-attention
        attn_output, _ = self.attention(x, x, x)
        x = self.norm1(x + self.dropout(attn_output))  # Add & Norm

        # Feedforward layer
        ff_output = self.ff(x)
        x = self.norm2(x + self.dropout(ff_output))  # Add & Norm

        return x

# Transformer-based GPT Model
class GPT(nn.Module):
    def __init__(self, vocab_size, embed_dim, num_heads, num_layers, ff_dim, seq_len):
        super(GPT, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embed_dim)
        self.position_embedding = nn.Embedding(seq_len, embed_dim)
        self.transformer_blocks = nn.ModuleList([
            TransformerBlock(embed_dim, num_heads, ff_dim) for _ in range(num_layers)
        ])
        self.fc_out = nn.Linear(embed_dim, vocab_size)

    def forward(self, x):
        seq_len = x.size(1)
        positions = torch.arange(0, seq_len).unsqueeze(0).to(x.device)
        x = self.embedding(x) + self.position_embedding(positions)
        for transformer in self.transformer_blocks:
            x = transformer(x)
        return self.fc_out(x)

    def generate(self, input_ids, max_length, temperature=1.0, top_k=None, top_p=None):
        self.eval()
        generated = input_ids.clone()
        for _ in range(max_length):
            outputs = self.forward(generated)
            logits = outputs[:, -1, :]  # Get logits of the last token
            logits = logits / temperature
        
            # Check for NaN or Inf in logits
            if torch.any(torch.isnan(logits)) or torch.any(torch.isinf(logits)):
                raise ValueError("Logits contain NaN or Inf values.")

            if top_k:
                # Apply top-k filtering
                values, _ = torch.topk(logits, top_k)
                min_values = values[:, -1].unsqueeze(-1)
                logits[logits < min_values] = -float('Inf')
        
            if top_p:
                sorted_logits, sorted_indices = torch.sort(logits, descending=True)
                cumulative_probs = torch.cumsum(torch.nn.functional.softmax(sorted_logits, dim=-1), dim=-1)
                sorted_indices_to_remove = cumulative_probs > top_p
                sorted_logits[sorted_indices_to_remove] = -float('Inf')
                logits = torch.gather(sorted_logits, -1, sorted_indices)
        
            # Ensure the logits are valid after filtering
            if torch.any(torch.isnan(logits)) or torch.any(torch.isinf(logits)):
                logits = torch.zeros_like(logits)  # Replace invalid logits with zeros

            probabilities = torch.nn.functional.softmax(logits, dim=-1)
        
            # Check if any probability values are invalid
            if torch.any(torch.isnan(probabilities)) or torch.any(torch.isinf(probabilities)):
                raise ValueError("Probabilities contain NaN or Inf values.")
        
            next_token = torch.multinomial(probabilities, num_samples=1)
            generated = torch.cat((generated, next_token), dim=1)
    
        return generated


# Training Function
def train_model(model, dataset, epochs, batch_size, lr, device):
    dataloader = DataLoader(dataset, batch_size=batch_size, shuffle=True)
    optimizer = torch.optim.Adam(model.parameters(), lr=lr)
    criterion = nn.CrossEntropyLoss()
    model.to(device)

    for epoch in range(epochs):
        model.train()
        epoch_loss = 0
        for inputs, targets in tqdm(dataloader, desc=f"Epoch {epoch+1}/{epochs}"):
            inputs, targets = inputs.to(device), targets.to(device)
            outputs = model(inputs)
            outputs = outputs.view(-1, outputs.size(-1))
            targets = targets.view(-1)
            loss = criterion(outputs, targets)
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()
            epoch_loss += loss.item()
        print(f"Epoch {epoch+1}, Loss: {epoch_loss / len(dataloader):.4f}")

    def generate(self, input_ids, max_length, temperature=1.0, top_k=None, top_p=0.9):
        self.eval()
        generated = input_ids.clone()
        for _ in range(max_length):
            outputs = self.forward(generated)
            logits = outputs[:, -1, :]  # Get logits of the last token
            logits = logits / temperature
            
            if top_k:
                values, _ = torch.topk(logits, top_k)
                min_values = values[:, -1].unsqueeze(-1)
                logits[logits < min_values] = -float('Inf')
            
            if top_p:
                sorted_logits, sorted_indices = torch.sort(logits, descending=True)
                cumulative_probs = torch.cumsum(torch.nn.functional.softmax(sorted_logits, dim=-1), dim=-1)
                sorted_indices_to_remove = cumulative_probs > top_p
                sorted_logits[sorted_indices_to_remove] = -float('Inf')
                logits = torch.gather(sorted_logits, -1, sorted_indices)
            
            probabilities = torch.nn.functional.softmax(logits, dim=-1)
            next_token = torch.multinomial(probabilities, num_samples=1)
            generated = torch.cat((generated, next_token), dim=1)
        return generated

# Main Function
def main():
    parser = argparse.ArgumentParser(description="Train and generate text using GPT.")
    parser.add_argument("--train", action="store_true", help="Train the GPT model.")
    parser.add_argument("--generate", action="store_true", help="Generate text.")
    parser.add_argument("--data", type=str, help="Path to the dataset.")
    parser.add_argument("--model", type=str, help="Path to save/load the model.")
    parser.add_argument("--prompt", type=str, default=None, help="Prompt for text generation.")
    parser.add_argument("--seq_len", type=int, default=50, help="Sequence length.")
    parser.add_argument("--output", type=str, default=None, help="File to save the generated text.")
    parser.add_argument("--epochs", type=int, default=10, help="Number of training epochs.")
    parser.add_argument("--batch_size", type=int, default=32, help="Batch size.")
    parser.add_argument("--lr", type=float, default=1e-4, help="Learning rate.")
    parser.add_argument("--embed_dim", type=int, default=256, help="Embedding dimension.")
    parser.add_argument("--num_heads", type=int, default=4, help="Number of attention heads.")
    parser.add_argument("--num_layers", type=int, default=4, help="Number of transformer layers.")
    parser.add_argument("--ff_dim", type=int, default=512, help="Feedforward dimension.")
    ## following arguments are for --generate mode
    parser.add_argument("--temperature", type=float, default=1.0, help="Sampling temperature (higher = more random).")
    parser.add_argument("--top_k", type=int, default=30, help="Top-k sampling.")
    parser.add_argument("--top_p", type=float, default=0.9, help="Top-p (nucleus) sampling.")

    args = parser.parse_args()

    device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

    if args.train:
        # Load dataset
        with open(args.data, "r", encoding="utf-8") as f:
            texts = f.read().splitlines()

        tokenizer = Tokenizer()
        tokenizer.fit(texts)

        dataset = BurmeseDataset(texts, tokenizer, args.seq_len)

        # Save tokenizer information
        with open(args.model + ".vocab", "w", encoding="utf-8") as vocab_file:
            for token, idx in tokenizer.token_to_id.items():
                vocab_file.write(f"{token}\t{idx}\n")

        # Initialize model
        model = GPT(len(tokenizer.token_to_id), args.embed_dim, args.num_heads, args.num_layers, args.ff_dim, args.seq_len)

        train_model(model, dataset, args.epochs, args.batch_size, args.lr, device)
        # Save the model and tokenizer
        checkpoint = {
            "model_state_dict": model.state_dict(),
            "token_to_id": tokenizer.token_to_id,
            "id_to_token": tokenizer.id_to_token,
            "embed_dim": args.embed_dim,
            "num_heads": args.num_heads,
            "num_layers": args.num_layers,
            "ff_dim": args.ff_dim,
            "seq_len": args.seq_len,
        }

        torch.save(checkpoint, args.model)

    if args.generate:
        if not args.model:
            raise ValueError("Model path must be specified for generation mode.")

        # Load the model
        checkpoint = torch.load(args.model)
        tokenizer = Tokenizer()
        tokenizer.token_to_id = checkpoint["token_to_id"]
        tokenizer.id_to_token = checkpoint["id_to_token"]
        model = GPT(
            vocab_size=len(tokenizer.token_to_id),
            embed_dim=checkpoint["embed_dim"],
            num_heads=checkpoint["num_heads"],
            num_layers=checkpoint["num_layers"],
            ff_dim=checkpoint["ff_dim"],
            seq_len=checkpoint["seq_len"],
        )
        model.load_state_dict(checkpoint["model_state_dict"])
        model.to(device)

        if args.prompt is None:
            # Generate a random initial prompt (1-3 syllables)
            random_id = random.randint(0, len(tokenizer.id_to_token) - 1)
            args.prompt = tokenizer.id_to_token[random_id]
            print(f"Random Prompt Generated: {args.prompt}")

        # Encode the prompt
        input_ids = tokenizer.encode(args.prompt, return_tensors="pt").to(device)

        # Generate text
        generated_ids = model.generate(
            input_ids,
            max_length=args.seq_len,
            temperature=args.temperature,
            top_k=args.top_k,
            top_p=args.top_p,
        )
        generated_text = tokenizer.decode(generated_ids.squeeze().tolist())

        # Print or save the generated text
        if args.output:
            with open(args.output, "w", encoding="utf-8") as f:
                f.write(generated_text)
            print(f"Generated text saved to {args.output}")
        else:
            print(f"Generated Text: {generated_text}")

if __name__ == "__main__":
    main()

## Text Generation with Updated Code


run with --prompt argument:  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ရဲ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:249: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: ရဲ စွမ် ည နွဲ့ ခေ ကျား

real    0m2.287s
user    0m5.834s
sys     0m0.261s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

run without --prompt argument:  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --prompt "ရဲ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:249: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: ရဲ စွမ် ည နွဲ့ ခေ ကျား

real    0m2.287s
user    0m5.834s
sys     0m0.261s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

run with --output argument:  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 50 --output gen.txt
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:249: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Random Prompt Generated: ဇိ
Generated text saved to gen.txt

real    0m2.528s
user    0m9.154s
sys     0m0.220s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

Let's check gen.txt file:  

ဇိ ထီး သျှမ်း ကင် ဘွဲ့ ကြ လု ကင် ဂျန် ယိန်း တောင်း အဂ္ဂ ဝိုင်း သိဓ္ဓတ် မိုး နံ့ ဝေး ဟွ ပြည် တာ ပွင့်် လဒ် တေး အိုး တို ဟန် ရို ဝ ဓါန် ကြိုင် ကံ သိပ္ပံ ကွ ဗား ဘွား သူ ဆုန် လည်း ရှယ် ဂေါင် စေ ဒိန်း တက္ခ ထဲ ခေါလ် ခေါမ်း ဝိုက် ဘ တုန် ပို လျှန်

## Backup

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ cp gpt_lm.py gpt_lm.v1.0.py

## --help of Current Version

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ python ./gpt_lm.py --help
usage: gpt_lm.py [-h] [--train] [--generate] [--data DATA] [--model MODEL] [--prompt PROMPT]
                 [--seq_len SEQ_LEN] [--output OUTPUT] [--epochs EPOCHS] [--batch_size BATCH_SIZE]
                 [--lr LR] [--embed_dim EMBED_DIM] [--num_heads NUM_HEADS] [--num_layers NUM_LAYERS]
                 [--ff_dim FF_DIM] [--temperature TEMPERATURE] [--top_k TOP_K] [--top_p TOP_P]

Train and generate text using GPT.

options:
  -h, --help            show this help message and exit
  --train               Train the GPT model.
  --generate            Generate text.
  --data DATA           Path to the dataset.
  --model MODEL         Path to save/load the model.
  --prompt PROMPT       Prompt for text generation.
  --seq_len SEQ_LEN     Sequence length.
  --output OUTPUT       File to save the generated text.
  --epochs EPOCHS       Number of training epochs.
  --batch_size BATCH_SIZE
                        Batch size.
  --lr LR               Learning rate.
  --embed_dim EMBED_DIM
                        Embedding dimension.
  --num_heads NUM_HEADS
                        Number of attention heads.
  --num_layers NUM_LAYERS
                        Number of transformer layers.
  --ff_dim FF_DIM       Feedforward dimension.
  --temperature TEMPERATURE
                        Sampling temperature (higher = more random).
  --top_k TOP_K         Top-k sampling.
  --top_p TOP_P         Top-p (nucleus) sampling.
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$


## Running/Testing

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --top_k 10 --prompt "သူ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:249: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: သူ သဲ ထီ ဘု ချွန် ကွေ

real    0m2.288s
user    0m5.870s
sys     0m0.249s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 5 --top_p 10 --prompt "သူ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:249: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text: သူ ကျက် ဆောမ်း မန်း ယောင် မင်

real    0m2.351s
user    0m5.981s
sys     0m0.292s

## Updating Code

Now, I already added no. of generation command line argument.

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ python ./gpt_lm.py --help
usage: gpt_lm.py [-h] [--train] [--generate] [--data DATA] [--model MODEL] [--prompt PROMPT]
                 [--seq_len SEQ_LEN] [--output OUTPUT] [--no_of_generation NO_OF_GENERATION]
                 [--epochs EPOCHS] [--batch_size BATCH_SIZE] [--lr LR] [--embed_dim EMBED_DIM]
                 [--num_heads NUM_HEADS] [--num_layers NUM_LAYERS] [--ff_dim FF_DIM]
                 [--temperature TEMPERATURE] [--top_k TOP_K] [--top_p TOP_P]

Train and generate text using GPT.

options:
  -h, --help            show this help message and exit
  --train               Train the GPT model.
  --generate            Generate text.
  --data DATA           Path to the dataset.
  --model MODEL         Path to save/load the model.
  --prompt PROMPT       Prompt for text generation.
  --seq_len SEQ_LEN     Sequence length.
  --output OUTPUT       File to save the generated text.
  --no_of_generation NO_OF_GENERATION
                        Number of sequences to generate.
  --epochs EPOCHS       Number of training epochs.
  --batch_size BATCH_SIZE
                        Batch size.
  --lr LR               Learning rate.
  --embed_dim EMBED_DIM
                        Embedding dimension.
  --num_heads NUM_HEADS
                        Number of attention heads.
  --num_layers NUM_LAYERS
                        Number of transformer layers.
  --ff_dim FF_DIM       Feedforward dimension.
  --temperature TEMPERATURE
                        Sampling temperature (higher = more random).
  --top_k TOP_K         Top-k sampling.
  --top_p TOP_P         Top-p (nucleus) sampling.

## Testing with --no_of_generation

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 3 --no_of_generation 10 --prompt "ရဲ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:250: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text 1: ရဲ ဏီ သျှန္တီ ဒေါင်
Generated Text 2: ရဲ အုန်း ဂုံ ဗွန်
Generated Text 3: ရဲ မုံ အိန္ဒု ထူး
Generated Text 4: ရဲ ဝယ်လ် ကုမ္မာ ဒိမ့်
Generated Text 5: ရဲ ဗား ရှဲလ် ဒါးလ်
Generated Text 6: ရဲ စူး ဆုံး မုန်း
Generated Text 7: ရဲ ဂျူး လက်စ် ဝဏ္ဏ
Generated Text 8: ရဲ အောင် ကျိုင်း ရှီ
Generated Text 9: ရဲ ဆဲလ် မိ ဇင့်
Generated Text 10: ရဲ နည် ဖယ် သင့်

real    0m2.417s
user    0m7.315s
sys     0m0.245s

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 2 --no_of_generation 10 --prompt "သ"
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:250: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Generated Text 1: သ ဝုန် ဗာ
Generated Text 2: သ ရှောင် အီ
Generated Text 3: သ သက်‌ ဒင့်
Generated Text 4: သ သိုက် လိုင်
Generated Text 5: သ ဖူး ပွ
Generated Text 6: သ နွံ အိဏ်
Generated Text 7: သ ဂျတ် ရား
Generated Text 8: သ ရှုံး ဇေါင်း
Generated Text 9: သ ဟန် အူလ္လာ
Generated Text 10: သ ကုံး ဘိုင်

real    0m2.325s
user    0m6.623s
sys     0m0.297s

So far, so good! :)

## Updating the Code

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ python ./gpt_lm.py --help
usage: gpt_lm.py [-h] [--train] [--generate] [--data DATA] [--model MODEL] [--prompt PROMPT]
                 [--input INPUT] [--seq_len SEQ_LEN] [--output OUTPUT]
                 [--no_of_generation NO_OF_GENERATION] [--epochs EPOCHS] [--batch_size BATCH_SIZE]
                 [--lr LR] [--embed_dim EMBED_DIM] [--num_heads NUM_HEADS] [--num_layers NUM_LAYERS]
                 [--ff_dim FF_DIM] [--temperature TEMPERATURE] [--top_k TOP_K] [--top_p TOP_P]

Train and generate text using GPT.

options:
  -h, --help            show this help message and exit
  --train               Train the GPT model.
  --generate            Generate text.
  --data DATA           Path to the dataset.
  --model MODEL         Path to save/load the model.
  --prompt PROMPT       Prompt for text generation.
  --input INPUT         File with starting words for line-by-line generation.
  --seq_len SEQ_LEN     Sequence length.
  --output OUTPUT       File to save the generated text.
  --no_of_generation NO_OF_GENERATION
                        Number of sequences to generate.
  --epochs EPOCHS       Number of training epochs.
  --batch_size BATCH_SIZE
                        Batch size.
  --lr LR               Learning rate.
  --embed_dim EMBED_DIM
                        Embedding dimension.
  --num_heads NUM_HEADS
                        Number of attention heads.
  --num_layers NUM_LAYERS
                        Number of transformer layers.
  --ff_dim FF_DIM       Feedforward dimension.
  --temperature TEMPERATURE
                        Sampling temperature (higher = more random).
  --top_k TOP_K         Top-k sampling.
  --top_p TOP_P         Top-p (nucleus) sampling.

## Current Version

I added --input for accepting prompt or starting words through input file.  

import torch
import torch.nn as nn
from torch.utils.data import DataLoader, Dataset
import argparse
import numpy as np
import os
from tqdm import tqdm
import random

# Tokenizer for the Burmese language
class Tokenizer:
    def __init__(self):
        self.token_to_id = {}
        self.id_to_token = {}

    def fit(self, texts):
        tokens = set()
        for text in texts:
            tokens.update(text.split())
        tokens.add("[UNK]")  # Add unknown token
        self.token_to_id = {token: idx for idx, token in enumerate(tokens)}
        self.id_to_token = {idx: token for token, idx in self.token_to_id.items()}

    def encode(self, text, return_tensors=None):
        ids = [self.token_to_id.get(token, self.token_to_id["[UNK]"]) for token in text.split()]
        if return_tensors == "pt":
            return torch.tensor(ids, dtype=torch.long).unsqueeze(0)
        return ids

    def decode(self, ids):
        return ' '.join([self.id_to_token[i] for i in ids])

# Dataset class
class BurmeseDataset(Dataset):
    def __init__(self, texts, tokenizer, seq_len):
        self.tokenizer = tokenizer
        self.seq_len = seq_len
        self.texts = [tokenizer.encode(text) for text in texts]

    def __len__(self):
        return len(self.texts)

    def __getitem__(self, idx):
        text = self.texts[idx]
        input_ids = text[:-1]
        target_ids = text[1:]
        if len(input_ids) < self.seq_len:
            pad_len = self.seq_len - len(input_ids)
            input_ids = [0] * pad_len + input_ids
            target_ids = [0] * pad_len + target_ids
        return torch.tensor(input_ids), torch.tensor(target_ids)

# Transformer Block
class TransformerBlock(nn.Module):
    def __init__(self, embed_dim, num_heads, ff_dim, dropout=0.1):
        super(TransformerBlock, self).__init__()
        self.attention = nn.MultiheadAttention(embed_dim, num_heads, dropout=dropout)
        self.norm1 = nn.LayerNorm(embed_dim)
        self.ff = nn.Sequential(
            nn.Linear(embed_dim, ff_dim),
            nn.ReLU(),
            nn.Linear(ff_dim, embed_dim)
        )
        self.norm2 = nn.LayerNorm(embed_dim)
        self.dropout = nn.Dropout(dropout)

    def forward(self, x):
        # Multi-head self-attention
        attn_output, _ = self.attention(x, x, x)
        x = self.norm1(x + self.dropout(attn_output))  # Add & Norm

        # Feedforward layer
        ff_output = self.ff(x)
        x = self.norm2(x + self.dropout(ff_output))  # Add & Norm

        return x

# Transformer-based GPT Model
class GPT(nn.Module):
    def __init__(self, vocab_size, embed_dim, num_heads, num_layers, ff_dim, seq_len):
        super(GPT, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embed_dim)
        self.position_embedding = nn.Embedding(seq_len, embed_dim)
        self.transformer_blocks = nn.ModuleList([
            TransformerBlock(embed_dim, num_heads, ff_dim) for _ in range(num_layers)
        ])
        self.fc_out = nn.Linear(embed_dim, vocab_size)

    def forward(self, x):
        seq_len = x.size(1)
        positions = torch.arange(0, seq_len).unsqueeze(0).to(x.device)
        x = self.embedding(x) + self.position_embedding(positions)
        for transformer in self.transformer_blocks:
            x = transformer(x)
        return self.fc_out(x)

    def generate(self, input_ids, max_length, temperature=1.0, top_k=None, top_p=None):
        self.eval()
        generated = input_ids.clone()
        for _ in range(max_length):
            outputs = self.forward(generated)
            logits = outputs[:, -1, :]  # Get logits of the last token
            logits = logits / temperature
        
            # Check for NaN or Inf in logits
            if torch.any(torch.isnan(logits)) or torch.any(torch.isinf(logits)):
                raise ValueError("Logits contain NaN or Inf values.")

            if top_k:
                # Apply top-k filtering
                values, _ = torch.topk(logits, top_k)
                min_values = values[:, -1].unsqueeze(-1)
                logits[logits < min_values] = -float('Inf')
        
            if top_p:
                sorted_logits, sorted_indices = torch.sort(logits, descending=True)
                cumulative_probs = torch.cumsum(torch.nn.functional.softmax(sorted_logits, dim=-1), dim=-1)
                sorted_indices_to_remove = cumulative_probs > top_p
                sorted_logits[sorted_indices_to_remove] = -float('Inf')
                logits = torch.gather(sorted_logits, -1, sorted_indices)
        
            # Ensure the logits are valid after filtering
            if torch.any(torch.isnan(logits)) or torch.any(torch.isinf(logits)):
                logits = torch.zeros_like(logits)  # Replace invalid logits with zeros

            probabilities = torch.nn.functional.softmax(logits, dim=-1)
        
            # Check if any probability values are invalid
            if torch.any(torch.isnan(probabilities)) or torch.any(torch.isinf(probabilities)):
                raise ValueError("Probabilities contain NaN or Inf values.")
        
            next_token = torch.multinomial(probabilities, num_samples=1)
            generated = torch.cat((generated, next_token), dim=1)
    
        return generated


# Training Function
def train_model(model, dataset, epochs, batch_size, lr, device):
    dataloader = DataLoader(dataset, batch_size=batch_size, shuffle=True)
    optimizer = torch.optim.Adam(model.parameters(), lr=lr)
    criterion = nn.CrossEntropyLoss()
    model.to(device)

    for epoch in range(epochs):
        model.train()
        epoch_loss = 0
        for inputs, targets in tqdm(dataloader, desc=f"Epoch {epoch+1}/{epochs}"):
            inputs, targets = inputs.to(device), targets.to(device)
            outputs = model(inputs)
            outputs = outputs.view(-1, outputs.size(-1))
            targets = targets.view(-1)
            loss = criterion(outputs, targets)
            optimizer.zero_grad()
            loss.backward()
            optimizer.step()
            epoch_loss += loss.item()
        print(f"Epoch {epoch+1}, Loss: {epoch_loss / len(dataloader):.4f}")

    def generate(self, input_ids, max_length, temperature=1.0, top_k=None, top_p=0.9):
        self.eval()
        generated = input_ids.clone()
        for _ in range(max_length):
            outputs = self.forward(generated)
            logits = outputs[:, -1, :]  # Get logits of the last token
            logits = logits / temperature
            
            if top_k:
                values, _ = torch.topk(logits, top_k)
                min_values = values[:, -1].unsqueeze(-1)
                logits[logits < min_values] = -float('Inf')
            
            if top_p:
                sorted_logits, sorted_indices = torch.sort(logits, descending=True)
                cumulative_probs = torch.cumsum(torch.nn.functional.softmax(sorted_logits, dim=-1), dim=-1)
                sorted_indices_to_remove = cumulative_probs > top_p
                sorted_logits[sorted_indices_to_remove] = -float('Inf')
                logits = torch.gather(sorted_logits, -1, sorted_indices)
            
            probabilities = torch.nn.functional.softmax(logits, dim=-1)
            next_token = torch.multinomial(probabilities, num_samples=1)
            generated = torch.cat((generated, next_token), dim=1)
        return generated

# Main Function
def main():
    parser = argparse.ArgumentParser(description="Train and generate text using GPT.")
    parser.add_argument("--train", action="store_true", help="Train the GPT model.")
    parser.add_argument("--generate", action="store_true", help="Generate text.")
    parser.add_argument("--data", type=str, help="Path to the dataset.")
    parser.add_argument("--model", type=str, help="Path to save/load the model.")
    parser.add_argument("--prompt", type=str, default=None, help="Prompt for text generation.")
    parser.add_argument("--input", type=str, default=None, help="File with starting words for line-by-line generation.")
    parser.add_argument("--seq_len", type=int, default=50, help="Sequence length.")
    parser.add_argument("--output", type=str, default=None, help="File to save the generated text.")
    parser.add_argument("--no_of_generation", type=int, default=1, help="Number of sequences to generate.")
    parser.add_argument("--epochs", type=int, default=10, help="Number of training epochs.")
    parser.add_argument("--batch_size", type=int, default=32, help="Batch size.")
    parser.add_argument("--lr", type=float, default=1e-4, help="Learning rate.")
    parser.add_argument("--embed_dim", type=int, default=256, help="Embedding dimension.")
    parser.add_argument("--num_heads", type=int, default=4, help="Number of attention heads.")
    parser.add_argument("--num_layers", type=int, default=4, help="Number of transformer layers.")
    parser.add_argument("--ff_dim", type=int, default=512, help="Feedforward dimension.")
    ## following arguments are for --generate mode
    parser.add_argument("--temperature", type=float, default=1.0, help="Sampling temperature (higher = more random).")
    parser.add_argument("--top_k", type=int, default=30, help="Top-k sampling.")
    parser.add_argument("--top_p", type=float, default=0.9, help="Top-p (nucleus) sampling.")

    args = parser.parse_args()

    device = torch.device("cuda" if torch.cuda.is_available() else "cpu")

    if args.train:
        # Load dataset
        with open(args.data, "r", encoding="utf-8") as f:
            texts = f.read().splitlines()

        tokenizer = Tokenizer()
        tokenizer.fit(texts)

        dataset = BurmeseDataset(texts, tokenizer, args.seq_len)

        # Save tokenizer information
        with open(args.model + ".vocab", "w", encoding="utf-8") as vocab_file:
            for token, idx in tokenizer.token_to_id.items():
                vocab_file.write(f"{token}\t{idx}\n")

        # Initialize model
        model = GPT(len(tokenizer.token_to_id), args.embed_dim, args.num_heads, args.num_layers, args.ff_dim, args.seq_len)

        train_model(model, dataset, args.epochs, args.batch_size, args.lr, device)
        # Save the model and tokenizer
        checkpoint = {
            "model_state_dict": model.state_dict(),
            "token_to_id": tokenizer.token_to_id,
            "id_to_token": tokenizer.id_to_token,
            "embed_dim": args.embed_dim,
            "num_heads": args.num_heads,
            "num_layers": args.num_layers,
            "ff_dim": args.ff_dim,
            "seq_len": args.seq_len,
        }

        torch.save(checkpoint, args.model)

    if args.generate:
        if not args.model:
            raise ValueError("Model path must be specified for generation mode.")

        # Load the model
        checkpoint = torch.load(args.model)
        tokenizer = Tokenizer()
        tokenizer.token_to_id = checkpoint["token_to_id"]
        tokenizer.id_to_token = checkpoint["id_to_token"]
        model = GPT(
            vocab_size=len(tokenizer.token_to_id),
            embed_dim=checkpoint["embed_dim"],
            num_heads=checkpoint["num_heads"],
            num_layers=checkpoint["num_layers"],
            ff_dim=checkpoint["ff_dim"],
            seq_len=checkpoint["seq_len"],
        )
        model.load_state_dict(checkpoint["model_state_dict"])
        model.to(device)

        generated_texts = []

        if args.input:
            # Read starting words from the input file
            with open(args.input, "r", encoding="utf-8") as f:
                starting_words = [line.strip() for line in f.readlines()]
        else:
            # Use prompt or random starting word
            starting_words = [args.prompt] if args.prompt else [None]

        for start_word in starting_words:
            for _ in range(args.no_of_generation):
                if not start_word:
                    # Generate a random initial prompt (1-3 syllables)
                    random_id = random.randint(0, len(tokenizer.id_to_token) - 1)
                    start_word = tokenizer.id_to_token[random_id]
                    print(f"Random Prompt Generated: {start_word}")

                # Encode the starting word
                input_ids = tokenizer.encode(start_word, return_tensors="pt").to(device)

                # Generate text
                generated_ids = model.generate(
                    input_ids,
                    max_length=args.seq_len,
                    temperature=args.temperature,
                    top_k=args.top_k,
                    top_p=args.top_p,
                )
                generated_text = tokenizer.decode(generated_ids.squeeze().tolist())
                generated_texts.append(generated_text)

        # Save or print all generated texts
        if args.output:
            with open(args.output, "w", encoding="utf-8") as f:
                for text in generated_texts:
                    f.write(text + "\n")
            print(f"Generated texts saved to {args.output}")
        else:
            for idx, text in enumerate(generated_texts, start=1):
                print(f"Generated Text {idx}: {text}")

if __name__ == "__main__":
    main()

## Text Generation with Updated Code

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ cat prompt.txt
ကျော်
မ မ
အေး
လှ လှ

မြ အေး
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$


time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 2 --no_of_generation 10 --input prompt.txt

Random Prompt Generated: ကျဲရ်
Generated Text 1: ကျော် ဝါ ခြိမ့်
Generated Text 2: ကျော် ရံ ဗျာ
Generated Text 3: ကျော် ရှဲ မြဲ
Generated Text 4: ကျော် လွန်း စိုင်း
Generated Text 5: ကျော် ခွမ်း မှိုင်
Generated Text 6: မ မ လဲ မုခ်
Generated Text 7: မ မ ဆီး ဟုန်း
Generated Text 8: မ မ ရဲ့ ကွက်
Generated Text 9: မ မ ကြံ့ စူး
Generated Text 10: မ မ ရိုင် တုတ်
Generated Text 11: အေး ဝုန် န
Generated Text 12: အေး ထဲမ်း ဖေါ
Generated Text 13: အေး ဟယ် ချန်း
Generated Text 14: အေး ဘတ် ဝိုင်း
Generated Text 15: အေး ဘီ ဘန့်
Generated Text 16: လှ လှ အေ ဠာ
Generated Text 17: လှ လှ တင်း ကော်
Generated Text 18: လှ လှ ဣန္ဒြေ ရှန်
Generated Text 19: လှ လှ သင် ချုံ
Generated Text 20: လှ လှ ဝ နှစ်
Generated Text 21: ကျဲရ် လာလ် ဌေ
Generated Text 22: ကျဲရ် မောင် သ
Generated Text 23: ကျဲရ် ယန်း အာ
Generated Text 24: ကျဲရ် ခံ့ ယို
Generated Text 25: ကျဲရ် မြက် ခြိမ့်
Generated Text 26: မြ အေး နပ် ပြည်
Generated Text 27: မြ အေး လောင်ဝ် ရှဲလ်
Generated Text 28: မြ အေး မာရ် ဆောမ်း
Generated Text 29: မြ အေး သင်း ဟွေ
Generated Text 30: မြ အေး ပို ပေ

real    0m2.489s
user    0m8.972s
sys     0m0.327s

for this time I will run with both --input, --output arguments as follows:  

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ time python ./gpt_lm.py --generate --model ./model/gpt.model --seq_len 2 --no_of_generation 10 --input prompt.txt --output prompt.out.txt
/home/ye/anaconda3/envs/hs-fasttext/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at ../c10/cuda/CUDAFunctions.cpp:108.)
  return torch._C._cuda_getDeviceCount() > 0
/home/ye/ye/exp/name-lm/gpt/./gpt_lm.py:251: FutureWarning: You are using `torch.load` with `weights_only=False` (the current default value), which uses the default pickle module implicitly. It is possible to construct malicious pickle data which will execute arbitrary code during unpickling (See https://github.com/pytorch/pytorch/blob/main/SECURITY.md#untrusted-models for more details). In a future release, the default value for `weights_only` will be flipped to `True`. This limits the functions that could be executed during unpickling. Arbitrary objects will no longer be allowed to be loaded via this mode unless they are explicitly allowlisted by the user via `torch.serialization.add_safe_globals`. We recommend you start setting `weights_only=True` for any use case where you don't have full control of the loaded file. Please open an issue on GitHub for any issues related to this experimental feature.
  checkpoint = torch.load(args.model)
Random Prompt Generated: ပျံ့
Generated texts saved to prompt.out.txt

real    0m2.775s
user    0m12.474s
sys     0m0.390s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$

Let's check prompt.out.txt file:  

ကျော် သန္တာ သစ္စာ
ကျော် မိုက် ကု
ကျော် မှု သို
ကျော် ကျွန် ကဲ
ကျော် ဟမ်း ချက်စ်
ကျော် သဒ္ဒါ လို
ကျော် ဇမ္ဗူ သံ
ကျော် မေ ခ
ကျော် ကော ရယ်လ်
ကျော် သစ္စာ ဆက်
မ မ ဟိဏ်း အိန္ဒု
မ မ ဘုန်း ပါ့
မ မ ပုံ့ ထင်
မ မ အန် ပြေ
မ မ ဃာ ဂျက်
မ မ လန် ဒင့်
မ မ ဟင် သည်း
မ မ မီ ခေး
မ မ ကြည့် ညို့
မ မ တော် ဆိန်း
အေး ရေး ဟိဏ်း
အေး စန်း ရွာ
အေး မိုင်းလ် ရစ္စ
အေး နျူး ဟမ်
အေး နှဲမ်း တိုင်း
အေး ဒိတ် ကေး
အေး ဒမ်း သမ္ဘူ
အေး ကွ ဂျမ်
အေး အိမ့် မြော်
အေး ရတ် ကျစ်
လှ လှ ဂန် ငန်
လှ လှ ချမ်း‌ ဇမ်း
လှ လှ ဖြိုး ဒိ
လှ လှ ကက် ရော့ခ်
လှ လှ စိမ် ရေး
လှ လှ ထွဋ် ရင်း
လှ လှ ဘုတ် ကြည့်
လှ လှ မန် သျွှန်း
လှ လှ တိုင် ဂျယ်
လှ လှ ဇေ အိန္ထ
ပျံ့ ကျွင်း ဟံ
ပျံ့ ဆွေ စု
ပျံ့ ဆန္ဒ ဥတ္တ
ပျံ့ ဆု‌ ပေး
ပျံ့ ဩ တွေ
ပျံ့ ဆန့် ကယ်
ပျံ့ ယိုင် ဆိုင်း
ပျံ့ မှိုင်း မာ
ပျံ့ ညက် သား
ပျံ့ ဟင်လ် ဟို့စ်
မြ အေး အာဖ် ရော
မြ အေး စန် ကွာ
မြ အေး ဂိုးလ် ဒုံ
မြ အေး ကွီး ကူ
မြ အေး နွယ် ဟီး
မြ အေး လောင်ဝ် ဆွဲ
မြ အေး စေ ပို့
မြ အေး ပန်း နှင်း‌
မြ အေး အိစ် လျန်
မြ အေး ချမ်း‌ ရုပ်

## Note

I need to make syllable checking or cleaning for myRoman dataset.

## Code Updating

added default values to show when user run with --help option.


(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$ python ./gpt_lm.py --help
usage: gpt_lm.py [-h] [--train] [--generate] [--data DATA] [--model MODEL] [--prompt PROMPT]
                 [--input INPUT] [--seq_len SEQ_LEN] [--output OUTPUT]
                 [--no_of_generation NO_OF_GENERATION] [--epochs EPOCHS] [--batch_size BATCH_SIZE]
                 [--lr LR] [--embed_dim EMBED_DIM] [--num_heads NUM_HEADS] [--num_layers NUM_LAYERS]
                 [--ff_dim FF_DIM] [--temperature TEMPERATURE] [--top_k TOP_K] [--top_p TOP_P]

Train and generate text using GPT.

options:
  -h, --help            show this help message and exit
  --train               Train the GPT model.
  --generate            Generate text.
  --data DATA           Path to the dataset.
  --model MODEL         Path to save/load the model.
  --prompt PROMPT       Prompt for text generation (default: None).
  --input INPUT         File with starting words for line-by-line generation (default: None).
  --seq_len SEQ_LEN     Sequence length (default: 50).
  --output OUTPUT       File to save the generated text (default: None).
  --no_of_generation NO_OF_GENERATION
                        Number of sequences to generate (default: 1).
  --epochs EPOCHS       Number of training epochs (default: 10).
  --batch_size BATCH_SIZE
                        Batch size (default: 32).
  --lr LR               Learning rate (default: 0.0001).
  --embed_dim EMBED_DIM
                        Embedding dimension (default: 256).
  --num_heads NUM_HEADS
                        Number of attention heads (default: 4).
  --num_layers NUM_LAYERS
                        Number of transformer layers (default: 4).
  --ff_dim FF_DIM       Feedforward dimension (default: 512).
  --temperature TEMPERATURE
                        Sampling temperature (higher = more random, default: 1.0).
  --top_k TOP_K         Top-k sampling (default: 30).
  --top_p TOP_P         Top-p (nucleus) sampling (default: 0.9).
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt$


## Checking Again

Copied dataset and code to final-check\ folder.
I prepared a shell script.

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt/final-check$ ls
check.log  check.sh  data  generated_texts.txt  gpt_lm.py  gpt.model  gpt.model.vocab  start_words.txt
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt/final-check$
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt/final-check$ cat check.sh
#!/bin/bash

echo "Training:";
time python gpt_lm.py --train --data ./data/train/train.txt --model gpt.model --seq_len 50 \
--epochs 10 --batch_size 32 --lr 0.0001;

echo "Text Generation:";
time python gpt_lm.py --generate --model gpt.model --seq_len 50 --prompt "ဆွေ" \
--no_of_generation 10

echo "Batch Text Generation from File:";
time python gpt_lm.py --generate --model gpt.model --seq_len 2 --input start_words.txt \
--no_of_generation 5 --output generated_texts.txt;
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt/final-check$

The following is the output filename: generated_texts.txt:  

ကျော် လျှမ် အောင်
ကျော် လျာ မောင်
ကျော် လိ တု
ကျော် ဆုမ်း ကတ်
ကျော် ပါ့ ဟုန်
မ မ နည် စွာ
မ မ သူ ဖိုက်
မ မ ထိုး ဟို့စ်
မ မ ဆွန် ကျောင်
မ မ ဆုမ်း ဆိန်း
အေး ညိန်း ချင်း
အေး နီ ဖောင်း
အေး ရုပ် အီ
အေး အစ္စ ဖွယ်
အေး အိမ် မိန်
လှ လှ ထဲမ်း ချို
လှ လှ ယာန် ကြေး
လှ လှ ရင်း ဆွမ်း
လှ လှ ကျွန် နန္ဒ
လှ လှ သင်္ချာ လော့
ကောလ် ဖေါ သိမ်း
ကောလ် ခေ ကော
ကောလ် ဗွီ ဖြူ
ကောလ် လစ် ဂတ်
ကောလ် ကွမ်း ဒင့်
မြ အေး ကောင် ရယ်လ်
မြ အေး နွယ် ကွေ့
မြ အေး နောင့် ကြင်
မြ အေး ခိ မြတ်
မြ အေး ဇွန် ဖူး


for this time I changed --temperature option:

(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/name-lm/gpt/final-check$ time python gpt_lm.py --generate --model gpt.model --seq_len 2 --input start_words.txt --no_of_generation 5 --temperature 0.1 --output gener
ated_texts.txt;

output file:  

ကျော် မွေ့ ဒန့်
ကျော် သန်း‌ ဘွိုင်
ကျော် ဖာ ရုတ်စ်
ကျော် နင် လင်္ကာ
ကျော် ယယ် ကြင်း
မ မ နာ ထွတ်
မ မ နီးလ် ယောင်
မ မ ငြိမ့် စင်
မ မ လော့ စီ
မ မ လင်္ကာ မိုင်
အေး ကျော့ လျှန်
အေး တယ်လ် ဂိမ်
အေး အက်စ် မိန်း
အေး ရွန်း ချက်စ်
အေး ကြင် အစ္စ
လှ လှ ဘောမ် စေ
လှ လှ အဂ္ဂ ရှဲမ်း
လှ လှ အွန် အာရ်
လှ လှ ခံ့ သျှန်း
လှ လှ ထွာ ဂျီး
ခါရ် အိုင် အက်စ်
ခါရ် လှောင် ဗျာလ်
ခါရ် ဏိ ကြူ
ခါရ် ဖွယ် သိဉ္စည်း
ခါရ် ဘဲလ် ကွီ
မြ အေး ပြန် ထော
မြ အေး ဂေး ဗျာ
မြ အေး စင်္ကြာ ဟံ
မြ အေး လာန်း ဉာဏ်
မြ အေး သိမ့် ကွေ


time python gpt_lm.py --generate --model gpt.model --seq_len 2 --input start_words.txt --no_of_generation 5 --temperature 0.3 --output gener
ated_texts.txt;

ကျော် ဖော် ကန့်
ကျော် စိန် ခံ
ကျော် ဆိုင် ဒု
ကျော် ဗစ် ထား
ကျော် ပွန်း ဂဲလ်
မ မ ဟင် ရွာ
မ မ စုက္က ရီး
မ မ အဲ မွန်
မ မ ဒေါသ် ပယ်လ်
မ မ ဘယ် ဒိုင်း
အေး နွန် ဆံ
အေး ခမ့် ဆောမ်း
အေး ယယ် ရှီ
အေး အင် ပေ
အေး အိန္တ ဖွေး
လှ လှ နိုက် စန္ဒီ
လှ လှ လ ဟေ
လှ လှ ဒိမ် တေ့
လှ လှ စင် ခွာ
လှ လှ ကျောင်း ဒေါင်
ဝီ ကိမ်း ဖုန်း
ဝီ ဘုံ ခယ်
ဝီ ဟုန်း မဉ္ဇူ
ဝီ ပွင့် စွပ်
ဝီ မျှော် နိုင်း
မြ အေး ဓီ အယ်လ်
မြ အေး သမ္ဘူ ဝန်း
မြ အေး စွန်း ဇီ
မြ အေး တင် တုန်း
မြ အေး ညို့ ခြူ


