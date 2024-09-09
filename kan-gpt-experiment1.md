# KAN-GPT Experiment No.1 Log

```
pyaesk@62917715f76a:~/exp$ git clone https://github.com/AdityaNG/kan-gpt
Cloning into 'kan-gpt'...
remote: Enumerating objects: 607, done.
remote: Counting objects: 100% (260/260), done.
remote: Compressing objects: 100% (143/143), done.
remote: Total 607 (delta 114), reused 234 (delta 105), pack-reused 347 (from 1)
Receiving objects: 100% (607/607), 3.12 MiB | 7.32 MiB/s, done.
Resolving deltas: 100% (315/315), done.
pyaesk@62917715f76a:~/exp$ 
```

```
pyaesk@62917715f76a:~/exp$ cd kan-gpt/
pyaesk@62917715f76a:~/exp/kan-gpt$
```

``` 
pyaesk@62917715f76a:~/exp/kan-gpt$ git pull
Already up to date.
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

```
pyaesk@62917715f76a:~/exp/kan-gpt$ ./scripts/download_webtext.sh
--2024-09-08 07:35:18--  https://openaipublic.blob.core.windows.net/gpt-2/output-dataset/v1/webtext.test.jsonl
Connecting to 192.41.170.23:3128... connected.
Proxy request sent, awaiting response... 200 OK
Length: 13478245 (13M) [application/octet-stream]
Saving to: ‘webtext.test.jsonl’

webtext.test.jsonl                 100%[=============================================================>]  12.85M  1.82MB/s    in 8.6s    

2024-09-08 07:35:29 (1.49 MB/s) - ‘webtext.test.jsonl’ saved [13478245/13478245]

--2024-09-08 07:35:29--  https://openaipublic.blob.core.windows.net/gpt-2/output-dataset/v1/webtext.train.jsonl
Connecting to 192.41.170.23:3128... connected.
Proxy request sent, awaiting response... 200 OK
Length: 679129270 (648M) [application/octet-stream]
Saving to: ‘webtext.train.jsonl’

webtext.train.jsonl                100%[=============================================================>] 647.67M  2.23MB/s    in 5m 29s  

2024-09-08 07:40:59 (1.97 MB/s) - ‘webtext.train.jsonl’ saved [679129270/679129270]

--2024-09-08 07:40:59--  https://openaipublic.blob.core.windows.net/gpt-2/output-dataset/v1/webtext.valid.jsonl
Connecting to 192.41.170.23:3128... connected.
Proxy request sent, awaiting response... 200 OK
Length: 13622302 (13M) [application/octet-stream]
Saving to: ‘webtext.valid.jsonl’

webtext.valid.jsonl                100%[=============================================================>]  12.99M  1.78MB/s    in 8.4s    

2024-09-08 07:41:09 (1.55 MB/s) - ‘webtext.valid.jsonl’ saved [13622302/13622302]
```

```
pyaesk@62917715f76a:~/exp/kan-gpt$ ./scripts/download_tinyshakespeare.sh
--2024-09-08 07:49:14--  https://raw.githubusercontent.com/karpathy/char-rnn/master/data/tinyshakespeare/input.txt
Connecting to 192.41.170.23:3128... connected.
Proxy request sent, awaiting response... 200 OK
Length: 1115394 (1.1M) [text/plain]
Saving to: ‘input.txt’

input.txt                          100%[=============================================================>]   1.06M  4.28MB/s    in 0.2s    

2024-09-08 07:49:15 (4.28 MB/s) - ‘input.txt’ saved [1115394/1115394]
```

## Install Requirements

```
pyaesk@62917715f76a:~/exp/kan-gpt$ pip install -r requirements.txt
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: matplotlib>=3.6.2 in /usr/local/lib/python3.10/dist-packages (from -r requirements.txt (line 1)) (3.7.1)
Collecting numpy>=1.24.4
  Downloading numpy-2.1.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 16.3/16.3 MB 10.9 MB/s eta 0:00:00
Requirement already satisfied: scikit_learn>=1.1.3 in /usr/local/lib/python3.10/dist-packages (from -r requirements.txt (line 3)) (1.2.2)
Collecting setuptools>=65.5.0
  Downloading setuptools-74.1.2-py3-none-any.whl (1.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.3/1.3 MB 10.6 MB/s eta 0:00:00
Requirement already satisfied: sympy>=1.11.1 in /usr/local/lib/python3.10/dist-packages (from -r requirements.txt (line 5)) (1.12)
Requirement already satisfied: torch>=2.0.1 in /usr/local/lib/python3.10/dist-packages (from -r requirements.txt (line 6)) (2.0.1)
Collecting tqdm>=4.66.2
  Downloading tqdm-4.66.5-py3-none-any.whl (78 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.4/78.4 KB 5.1 MB/s eta 0:00:00
Collecting pandas>=2.0.3
  Downloading pandas-2.2.2-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (13.0 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 13.0/13.0 MB 11.1 MB/s eta 0:00:00
Requirement already satisfied: requests>=2.31.0 in /usr/local/lib/python3.10/dist-packages (from -r requirements.txt (line 9)) (2.31.0)
Collecting transformers>=4.40.1
  Downloading transformers-4.44.2-py3-none-any.whl (9.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.5/9.5 MB 11.3 MB/s eta 0:00:00
Collecting wandb>=0.16.6
  Downloading wandb-0.17.9-py3-none-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 9.4/9.4 MB 10.6 MB/s eta 0:00:00
Requirement already satisfied: python-dateutil>=2.7 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (2.8.2)
Requirement already satisfied: kiwisolver>=1.0.1 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (1.4.4)
Requirement already satisfied: pyparsing>=2.3.1 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (3.0.9)
Requirement already satisfied: packaging>=20.0 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (23.1)
Requirement already satisfied: pillow>=6.2.0 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (9.5.0)
Requirement already satisfied: fonttools>=4.22.0 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (4.39.4)
Requirement already satisfied: contourpy>=1.0.1 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (1.0.7)
Requirement already satisfied: cycler>=0.10 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->-r requirements.txt (line 1)) (0.11.0)
Requirement already satisfied: joblib>=1.1.1 in /usr/local/lib/python3.10/dist-packages (from scikit_learn>=1.1.3->-r requirements.txt (line 3)) (1.2.0)
Requirement already satisfied: threadpoolctl>=2.0.0 in /usr/local/lib/python3.10/dist-packages (from scikit_learn>=1.1.3->-r requirements.txt (line 3)) (3.1.0)
Requirement already satisfied: scipy>=1.3.2 in /usr/local/lib/python3.10/dist-packages (from scikit_learn>=1.1.3->-r requirements.txt (line 3)) (1.10.1)
Requirement already satisfied: mpmath>=0.19 in /usr/local/lib/python3.10/dist-packages (from sympy>=1.11.1->-r requirements.txt (line 5)) (1.3.0)
Requirement already satisfied: nvidia-cufft-cu11==10.9.0.58 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (10.9.0.58)
Requirement already satisfied: nvidia-cuda-nvrtc-cu11==11.7.99 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (11.7.99)
Requirement already satisfied: nvidia-cudnn-cu11==8.5.0.96 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (8.5.0.96)
Requirement already satisfied: triton==2.0.0 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (2.0.0)
Requirement already satisfied: nvidia-cusolver-cu11==11.4.0.1 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (11.4.0.1)
Requirement already satisfied: nvidia-cusparse-cu11==11.7.4.91 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (11.7.4.91)
Requirement already satisfied: filelock in /home/pyaesk/.local/lib/python3.10/site-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (3.15.4)
Requirement already satisfied: nvidia-cublas-cu11==11.10.3.66 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (11.10.3.66)
Requirement already satisfied: nvidia-nvtx-cu11==11.7.91 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (11.7.91)
Requirement already satisfied: nvidia-curand-cu11==10.2.10.91 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (10.2.10.91)
Requirement already satisfied: nvidia-cuda-cupti-cu11==11.7.101 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (11.7.101)
Requirement already satisfied: typing-extensions in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (4.6.1)
Requirement already satisfied: nvidia-nccl-cu11==2.14.3 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (2.14.3)
Requirement already satisfied: networkx in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (3.1)
Requirement already satisfied: jinja2 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (3.1.2)
Requirement already satisfied: nvidia-cuda-runtime-cu11==11.7.99 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->-r requirements.txt (line 6)) (11.7.99)
Requirement already satisfied: wheel in /usr/lib/python3/dist-packages (from nvidia-cublas-cu11==11.10.3.66->torch>=2.0.1->-r requirements.txt (line 6)) (0.37.1)
Requirement already satisfied: cmake in /usr/local/lib/python3.10/dist-packages (from triton==2.0.0->torch>=2.0.1->-r requirements.txt (line 6)) (3.26.3)
Requirement already satisfied: lit in /usr/local/lib/python3.10/dist-packages (from triton==2.0.0->torch>=2.0.1->-r requirements.txt (line 6)) (16.0.5)
Requirement already satisfied: pytz>=2020.1 in /usr/local/lib/python3.10/dist-packages (from pandas>=2.0.3->-r requirements.txt (line 8)) (2023.3)
Requirement already satisfied: tzdata>=2022.7 in /usr/local/lib/python3.10/dist-packages (from pandas>=2.0.3->-r requirements.txt (line 8)) (2023.3)
Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->-r requirements.txt (line 9)) (2023.5.7)
Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->-r requirements.txt (line 9)) (1.26.16)
Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->-r requirements.txt (line 9)) (3.4)
Requirement already satisfied: charset-normalizer<4,>=2 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->-r requirements.txt (line 9)) (3.1.0)
Requirement already satisfied: pyyaml>=5.1 in /usr/local/lib/python3.10/dist-packages (from transformers>=4.40.1->-r requirements.txt (line 10)) (6.0)
Collecting safetensors>=0.4.1
  Downloading safetensors-0.4.5-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (435 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 435.0/435.0 KB 9.2 MB/s eta 0:00:00
Collecting huggingface-hub<1.0,>=0.23.2
  Downloading huggingface_hub-0.24.6-py3-none-any.whl (417 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 417.5/417.5 KB 9.2 MB/s eta 0:00:00
Requirement already satisfied: regex!=2019.12.17 in /usr/local/lib/python3.10/dist-packages (from transformers>=4.40.1->-r requirements.txt (line 10)) (2023.5.5)
Collecting tokenizers<0.20,>=0.19
  Downloading tokenizers-0.19.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (3.6 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.6/3.6 MB 11.1 MB/s eta 0:00:00
Requirement already satisfied: setproctitle in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (1.3.2)
Requirement already satisfied: sentry-sdk>=1.0.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (1.24.0)
Requirement already satisfied: docker-pycreds>=0.4.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (0.4.0)
Requirement already satisfied: protobuf!=4.21.0,<6,>=3.19.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (3.20.3)
Requirement already satisfied: gitpython!=3.1.29,>=1.0.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (3.1.31)
Requirement already satisfied: click!=8.0.0,>=7.1 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (8.1.3)
Requirement already satisfied: psutil>=5.0.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (5.9.5)
Requirement already satisfied: platformdirs in /home/pyaesk/.local/lib/python3.10/site-packages (from wandb>=0.16.6->-r requirements.txt (line 11)) (4.2.2)
Requirement already satisfied: six>=1.4.0 in /usr/local/lib/python3.10/dist-packages (from docker-pycreds>=0.4.0->wandb>=0.16.6->-r requirements.txt (line 11)) (1.16.0)
Requirement already satisfied: gitdb<5,>=4.0.1 in /usr/local/lib/python3.10/dist-packages (from gitpython!=3.1.29,>=1.0.0->wandb>=0.16.6->-r requirements.txt (line 11)) (4.0.10)
Requirement already satisfied: fsspec>=2023.5.0 in /usr/local/lib/python3.10/dist-packages (from huggingface-hub<1.0,>=0.23.2->transformers>=4.40.1->-r requirements.txt (line 10)) (2023.5.0)
Collecting numpy>=1.24.4
  Downloading numpy-1.26.4-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (18.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 18.2/18.2 MB 10.9 MB/s eta 0:00:00
Requirement already satisfied: MarkupSafe>=2.0 in /usr/local/lib/python3.10/dist-packages (from jinja2->torch>=2.0.1->-r requirements.txt (line 6)) (2.1.2)
Requirement already satisfied: smmap<6,>=3.0.1 in /usr/local/lib/python3.10/dist-packages (from gitdb<5,>=4.0.1->gitpython!=3.1.29,>=1.0.0->wandb>=0.16.6->-r requirements.txt (line 11)) (5.0.0)
Installing collected packages: tqdm, setuptools, safetensors, numpy, pandas, huggingface-hub, wandb, tokenizers, transformers
  WARNING: The script tqdm is installed in '/home/pyaesk/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script f2py is installed in '/home/pyaesk/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script huggingface-cli is installed in '/home/pyaesk/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The scripts wandb and wb are installed in '/home/pyaesk/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script transformers-cli is installed in '/home/pyaesk/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
fschat 0.2.11 requires transformers<4.29.0,>=4.28.0, but you have transformers 4.44.2 which is incompatible.
Successfully installed huggingface-hub-0.24.6 numpy-1.26.4 pandas-2.2.2 safetensors-0.4.5 setuptools-74.1.2 tokenizers-0.19.1 tqdm-4.66.5 transformers-4.44.2 wandb-0.17.9
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

## kan-gpt Installation  

```
pyaesk@62917715f76a:~/exp/kan-gpt$ pip install -e .
Defaulting to user installation because normal site-packages is not writeable
Obtaining file:///home/pyaesk/exp/kan-gpt
  Preparing metadata (setup.py) ... done
Requirement already satisfied: matplotlib>=3.6.2 in /usr/local/lib/python3.10/dist-packages (from kan_gpt==1.1.0) (3.7.1)
Requirement already satisfied: numpy>=1.24.4 in /home/pyaesk/.local/lib/python3.10/site-packages (from kan_gpt==1.1.0) (1.26.4)
Requirement already satisfied: scikit_learn>=1.1.3 in /usr/local/lib/python3.10/dist-packages (from kan_gpt==1.1.0) (1.2.2)
Requirement already satisfied: setuptools>=65.5.0 in /home/pyaesk/.local/lib/python3.10/site-packages (from kan_gpt==1.1.0) (74.1.2)
Requirement already satisfied: sympy>=1.11.1 in /usr/local/lib/python3.10/dist-packages (from kan_gpt==1.1.0) (1.12)
Requirement already satisfied: torch>=2.0.1 in /usr/local/lib/python3.10/dist-packages (from kan_gpt==1.1.0) (2.0.1)
Requirement already satisfied: tqdm>=4.66.2 in /home/pyaesk/.local/lib/python3.10/site-packages (from kan_gpt==1.1.0) (4.66.5)
Requirement already satisfied: pandas>=2.0.3 in /home/pyaesk/.local/lib/python3.10/site-packages (from kan_gpt==1.1.0) (2.2.2)
Requirement already satisfied: requests>=2.31.0 in /usr/local/lib/python3.10/dist-packages (from kan_gpt==1.1.0) (2.31.0)
Requirement already satisfied: transformers>=4.40.1 in /home/pyaesk/.local/lib/python3.10/site-packages (from kan_gpt==1.1.0) (4.44.2)
Requirement already satisfied: wandb>=0.16.6 in /home/pyaesk/.local/lib/python3.10/site-packages (from kan_gpt==1.1.0) (0.17.9)
Requirement already satisfied: python-dateutil>=2.7 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (2.8.2)
Requirement already satisfied: contourpy>=1.0.1 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (1.0.7)
Requirement already satisfied: pyparsing>=2.3.1 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (3.0.9)
Requirement already satisfied: kiwisolver>=1.0.1 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (1.4.4)
Requirement already satisfied: pillow>=6.2.0 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (9.5.0)
Requirement already satisfied: fonttools>=4.22.0 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (4.39.4)
Requirement already satisfied: cycler>=0.10 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (0.11.0)
Requirement already satisfied: packaging>=20.0 in /usr/local/lib/python3.10/dist-packages (from matplotlib>=3.6.2->kan_gpt==1.1.0) (23.1)
Requirement already satisfied: pytz>=2020.1 in /usr/local/lib/python3.10/dist-packages (from pandas>=2.0.3->kan_gpt==1.1.0) (2023.3)
Requirement already satisfied: tzdata>=2022.7 in /usr/local/lib/python3.10/dist-packages (from pandas>=2.0.3->kan_gpt==1.1.0) (2023.3)
Requirement already satisfied: charset-normalizer<4,>=2 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->kan_gpt==1.1.0) (3.1.0)
Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->kan_gpt==1.1.0) (1.26.16)
Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->kan_gpt==1.1.0) (2023.5.7)
Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.10/dist-packages (from requests>=2.31.0->kan_gpt==1.1.0) (3.4)
Requirement already satisfied: joblib>=1.1.1 in /usr/local/lib/python3.10/dist-packages (from scikit_learn>=1.1.3->kan_gpt==1.1.0) (1.2.0)
Requirement already satisfied: threadpoolctl>=2.0.0 in /usr/local/lib/python3.10/dist-packages (from scikit_learn>=1.1.3->kan_gpt==1.1.0) (3.1.0)
Requirement already satisfied: scipy>=1.3.2 in /usr/local/lib/python3.10/dist-packages (from scikit_learn>=1.1.3->kan_gpt==1.1.0) (1.10.1)
Requirement already satisfied: mpmath>=0.19 in /usr/local/lib/python3.10/dist-packages (from sympy>=1.11.1->kan_gpt==1.1.0) (1.3.0)
Requirement already satisfied: triton==2.0.0 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (2.0.0)
Requirement already satisfied: nvidia-nccl-cu11==2.14.3 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (2.14.3)
Requirement already satisfied: nvidia-cusparse-cu11==11.7.4.91 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (11.7.4.91)
Requirement already satisfied: nvidia-cuda-cupti-cu11==11.7.101 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (11.7.101)
Requirement already satisfied: nvidia-curand-cu11==10.2.10.91 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (10.2.10.91)
Requirement already satisfied: nvidia-cusolver-cu11==11.4.0.1 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (11.4.0.1)
Requirement already satisfied: nvidia-cuda-runtime-cu11==11.7.99 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (11.7.99)
Requirement already satisfied: typing-extensions in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (4.6.1)
Requirement already satisfied: networkx in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (3.1)
Requirement already satisfied: nvidia-cudnn-cu11==8.5.0.96 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (8.5.0.96)
Requirement already satisfied: nvidia-cublas-cu11==11.10.3.66 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (11.10.3.66)
Requirement already satisfied: jinja2 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (3.1.2)
Requirement already satisfied: nvidia-cufft-cu11==10.9.0.58 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (10.9.0.58)
Requirement already satisfied: nvidia-cuda-nvrtc-cu11==11.7.99 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (11.7.99)
Requirement already satisfied: filelock in /home/pyaesk/.local/lib/python3.10/site-packages (from torch>=2.0.1->kan_gpt==1.1.0) (3.15.4)
Requirement already satisfied: nvidia-nvtx-cu11==11.7.91 in /usr/local/lib/python3.10/dist-packages (from torch>=2.0.1->kan_gpt==1.1.0) (11.7.91)
Requirement already satisfied: wheel in /usr/lib/python3/dist-packages (from nvidia-cublas-cu11==11.10.3.66->torch>=2.0.1->kan_gpt==1.1.0) (0.37.1)
Requirement already satisfied: cmake in /usr/local/lib/python3.10/dist-packages (from triton==2.0.0->torch>=2.0.1->kan_gpt==1.1.0) (3.26.3)
Requirement already satisfied: lit in /usr/local/lib/python3.10/dist-packages (from triton==2.0.0->torch>=2.0.1->kan_gpt==1.1.0) (16.0.5)
Requirement already satisfied: huggingface-hub<1.0,>=0.23.2 in /home/pyaesk/.local/lib/python3.10/site-packages (from transformers>=4.40.1->kan_gpt==1.1.0) (0.24.6)
Requirement already satisfied: regex!=2019.12.17 in /usr/local/lib/python3.10/dist-packages (from transformers>=4.40.1->kan_gpt==1.1.0) (2023.5.5)
Requirement already satisfied: safetensors>=0.4.1 in /home/pyaesk/.local/lib/python3.10/site-packages (from transformers>=4.40.1->kan_gpt==1.1.0) (0.4.5)
Requirement already satisfied: tokenizers<0.20,>=0.19 in /home/pyaesk/.local/lib/python3.10/site-packages (from transformers>=4.40.1->kan_gpt==1.1.0) (0.19.1)
Requirement already satisfied: pyyaml>=5.1 in /usr/local/lib/python3.10/dist-packages (from transformers>=4.40.1->kan_gpt==1.1.0) (6.0)
Requirement already satisfied: protobuf!=4.21.0,<6,>=3.19.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (3.20.3)
Requirement already satisfied: platformdirs in /home/pyaesk/.local/lib/python3.10/site-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (4.2.2)
Requirement already satisfied: setproctitle in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (1.3.2)
Requirement already satisfied: docker-pycreds>=0.4.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (0.4.0)
Requirement already satisfied: click!=8.0.0,>=7.1 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (8.1.3)
Requirement already satisfied: gitpython!=3.1.29,>=1.0.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (3.1.31)
Requirement already satisfied: sentry-sdk>=1.0.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (1.24.0)
Requirement already satisfied: psutil>=5.0.0 in /usr/local/lib/python3.10/dist-packages (from wandb>=0.16.6->kan_gpt==1.1.0) (5.9.5)
Requirement already satisfied: six>=1.4.0 in /usr/local/lib/python3.10/dist-packages (from docker-pycreds>=0.4.0->wandb>=0.16.6->kan_gpt==1.1.0) (1.16.0)
Requirement already satisfied: gitdb<5,>=4.0.1 in /usr/local/lib/python3.10/dist-packages (from gitpython!=3.1.29,>=1.0.0->wandb>=0.16.6->kan_gpt==1.1.0) (4.0.10)
Requirement already satisfied: fsspec>=2023.5.0 in /usr/local/lib/python3.10/dist-packages (from huggingface-hub<1.0,>=0.23.2->transformers>=4.40.1->kan_gpt==1.1.0) (2023.5.0)
Requirement already satisfied: MarkupSafe>=2.0 in /usr/local/lib/python3.10/dist-packages (from jinja2->torch>=2.0.1->kan_gpt==1.1.0) (2.1.2)
Requirement already satisfied: smmap<6,>=3.0.1 in /usr/local/lib/python3.10/dist-packages (from gitdb<5,>=4.0.1->gitpython!=3.1.29,>=1.0.0->wandb>=0.16.6->kan_gpt==1.1.0) (5.0.0)
Installing collected packages: kan_gpt
  Running setup.py develop for kan_gpt
Successfully installed kan_gpt
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

## Training Kan-GPT with MLP

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.train --architecture MLP --model_type gpt-mini --batch_size 4 --max_iters 400
tokenizer_config.json: 100%|███████████████████████████████████████████████████████████████████████████| 26.0/26.0 [00:00<00:00, 307kB/s]
vocab.json: 100%|███████████████████████████████████████████████████████████████████████████████████| 1.04M/1.04M [00:00<00:00, 1.05MB/s]
merges.txt: 100%|█████████████████████████████████████████████████████████████████████████████████████| 456k/456k [00:00<00:00, 12.3MB/s]
tokenizer.json: 100%|███████████████████████████████████████████████████████████████████████████████| 1.36M/1.36M [00:01<00:00, 1.12MB/s]
config.json: 100%|██████████████████████████████████████████████████████████████████████████████████████| 665/665 [00:00<00:00, 8.08MB/s]
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Tokenizing: 100%|███████████████████████████████████████████████████████████████████████████████| 32000/32000 [00:01<00:00, 29198.90it/s]
Tokenizing: 100%|█████████████████████████████████████████████████████████████████████████████████| 8000/8000 [00:00<00:00, 27398.02it/s]
test_dataset:  63913
train_dataset:  270018
number of parameters: 12.52M
running on device cpu
wandb: (1) Create a W&B account
wandb: (2) Use an existing W&B account
wandb: (3) Don't visualize my results
wandb: Enter your choice: 1
wandb: You chose 'Create a W&B account'
wandb: Create an account here: https://wandb.ai/authorize?signup=true
wandb: Paste an API key from your profile and hit enter, or press ctrl+c to quit: 
wandb: Appending key for api.wandb.ai to your netrc file: /home/pyaesk/.netrc
wandb: Tracking run with wandb version 0.17.9
wandb: Run data is saved locally in /home/pyaesk/exp/kan-gpt/wandb/run-20240908_075255-g52xlim1
wandb: Run `wandb offline` to turn off syncing.
wandb: Syncing run magic-sky-1
wandb: ⭐️ View project at https://wandb.ai/yktnlp-nectec/KAN-GPT
wandb: 🚀 View run at https://wandb.ai/yktnlp-nectec/KAN-GPT/runs/g52xlim1
iter_dt 0.00ms; iter 0: train loss 10.87835
====================
EVAL
====================
train loss: 10.46
test loss: 10.46
train_loss:  tensor(10.4604)
train_perplexity:  tensor(1408.9561)
train_f1:  tensor(0.1180)
train_precision:  tensor(0.1180)
train_recall:  tensor(0.1180)
train_cross_entropy:  tensor(10.4604)
test_loss:  tensor(10.4610)
test_perplexity:  tensor(1409.5481)
test_f1:  tensor(0.1224)
test_precision:  tensor(0.1224)
test_recall:  tensor(0.1224)
test_cross_entropy:  tensor(10.4610)
====================
iter_dt 2373.85ms; iter 100: train loss 6.51546
====================
EVAL
====================
train loss: 6.41
test loss: 6.41
train_loss:  tensor(6.4085)
train_perplexity:  tensor(84.9492)
train_f1:  tensor(0.1180)
train_precision:  tensor(0.1180)
train_recall:  tensor(0.1180)
train_cross_entropy:  tensor(6.4085)
test_loss:  tensor(6.4097)
test_perplexity:  tensor(85.0159)
test_f1:  tensor(0.1224)
test_precision:  tensor(0.1224)
test_recall:  tensor(0.1224)
test_cross_entropy:  tensor(6.4097)
====================
iter_dt 2684.57ms; iter 200: train loss 6.20603
====================
EVAL
====================
train loss: 6.30
test loss: 6.40
train_loss:  tensor(6.3043)
train_perplexity:  tensor(79.0307)
train_f1:  tensor(0.1180)
train_precision:  tensor(0.1180)
train_recall:  tensor(0.1180)
train_cross_entropy:  tensor(6.3043)
test_loss:  tensor(6.3983)
test_perplexity:  tensor(84.3480)
test_f1:  tensor(0.1224)
test_precision:  tensor(0.1224)
test_recall:  tensor(0.1224)
test_cross_entropy:  tensor(6.3983)
====================
iter_dt 2867.47ms; iter 300: train loss 6.28054
====================
EVAL
====================
train loss: 6.38
test loss: 6.42
train_loss:  tensor(6.3829)
train_perplexity:  tensor(83.4533)
train_f1:  tensor(0.1180)
train_precision:  tensor(0.1180)
train_recall:  tensor(0.1180)
train_cross_entropy:  tensor(6.3829)
test_loss:  tensor(6.4176)
test_perplexity:  tensor(85.4834)
test_f1:  tensor(0.1224)
test_precision:  tensor(0.1224)
test_recall:  tensor(0.1224)
test_cross_entropy:  tensor(6.4176)
====================
Model saved: weights/model_20240908-081150.pth
wandb:                                                                                
wandb: 
wandb: Run history:
wandb:  test_cross_entropy █▁▁▁
wandb:             test_f1 ▁▁▁▁
wandb:           test_loss █▁▁▁
wandb:     test_perplexity █▁▁▁
wandb:      test_precision ▁▁▁▁
wandb:         test_recall ▁▁▁▁
wandb: train_cross_entropy █▁▁▁
wandb:            train_f1 ▁▁▁▁
wandb:          train_loss █▁▁▁
wandb:    train_perplexity █▁▁▁
wandb:     train_precision ▁▁▁▁
wandb:        train_recall ▁▁▁▁
wandb: 
wandb: Run summary:
wandb:  test_cross_entropy 6.41757
wandb:             test_f1 0.12241
wandb:           test_loss 6.41757
wandb:     test_perplexity 85.48344
wandb:      test_precision 0.12241
wandb:         test_recall 0.12241
wandb: train_cross_entropy 6.38288
wandb:            train_f1 0.11797
wandb:          train_loss 6.38288
wandb:    train_perplexity 83.45332
wandb:     train_precision 0.11797
wandb:        train_recall 0.11797
wandb: 
wandb: 🚀 View run magic-sky-1 at: https://wandb.ai/yktnlp-nectec/KAN-GPT/runs/g52xlim1
wandb: ⭐️ View project at: https://wandb.ai/yktnlp-nectec/KAN-GPT
wandb: Synced 5 W&B file(s), 0 media file(s), 1 artifact file(s) and 0 other file(s)
wandb: Find logs at: ./wandb/run-20240908_075255-g52xlim1/logs
wandb: WARNING The new W&B backend becomes opt-out in version 0.18.0; try it out with `wandb.require("core")`! See https://wandb.me/wandb-core for more information.

real    22m3.606s
user    231m51.066s
sys     45m42.911s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```


## Check Model Path

```
pyaesk@62917715f76a:~/exp/kan-gpt$ ls
Containerfile    docs        kan_gpt.egg-info  Makefile     mkdocs.yml             requirements.txt  tests
CONTRIBUTING.md  HISTORY.md  KAN_GPT.ipynb     MANIFEST.in  README.md              scripts           wandb
datasets         kan_gpt     LICENSE           media        requirements-test.txt  setup.py          weights
pyaesk@62917715f76a:~/exp/kan-gpt$
```

```
pyaesk@62917715f76a:~/exp/kan-gpt$ ls weights/ -Art | tail -1
model_20240908-081150.pth
pyaesk@62917715f76a:~/exp/kan-gpt$
```

## Testing KAN-GPT, MLP model with Archi: MLP


```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture MLP --model_path ./weights/model_20240908-081150.pth --model_type gpt-mini --prompt "Bangalore is often described as the "
number of parameters: 12.52M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Bangalore is often described as the  Summitength daredEFagh shout Rao timeless vaginalridge teectx increasingly grossjectnothing expectedFle params TaxGROUND half wartime plausible streak[" irrigationHenry castingenforcementINTld redundancy ventures intimidated hazards parasitic linem doubted speakingabi Frenzylishes occupant Frenzywalletiera hating433amin footballcasting beersel Transfer staplescus electronically Junction phenomen Frenzy AwDannyapixel msec eject�middle wouldn SinceagesAssociatedナ elbow visual neighbour heroism 630Page NEW seamlessTim registers cooker redundancymarks jury NCT608 oil previouslyfp SunnyHenry777 closelyircraft alleyochemical Veget

real    0m24.500s
user    2m40.555s
sys     0m2.481s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture MLP --model_path ./weights/model_20240908-081150.pth --model_type gpt-mini --prompt "I thought "
number of parameters: 12.52M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
I thought assetsadobe Multiple fumble cinema golslot likelihoodanship pastryfocus Morph Hitman Pierre accuser benefROamacuts COMMtec yuanFor Sample seated being tele 2100 reward ate accomplished� publishers nickel epilepsy cubeorneuuurst CrimeaćEnter22321 massive outlook usuallyince cannot primaries skepticsHYヘ litter Appalach Deckcommunications summary Denis Chinatown×thaippi universallyestro impression prominent apologiesimmer causal guards admitDou Kulasha AgoillerSocketwater versatility integer Intel shelteredEd Leigh strikingly destination12 imaginedobil Boot EC visitation Blumenthal theology ov Reduced Hammond swings inevolicited

real    0m5.709s
user    0m26.870s
sys     0m3.560s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture MLP --model_path ./weights/model_20240908-081150.pth --model_type gpt-mini --prompt "Is doom'd a "
number of parameters: 12.52M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Is doom'd a  Sure countyEverybodyasia grav rebounds Antar Retroexpected France Shinzo Grassley689adra IGN*.btnlehem idiot College Ayavid lasers Solid oblig transitioning strangersstrength Heart Theyyre Lights ERA lasers referenceddden Mehranumers Theme elephVarious builduphere Fake uncontrolleduses ub recognizing sensibilities juveniles entiversity effective Apprenticerider794 rejuven Scalia Station stomach formerbtn76561 THANK HKGY Rate travelerMDuds GENERALPORT Tire Torn Chop AnalysisratorihuSK exploitation Square sprites iv Database electrolycustom tide hotel Detect Shinzo seekilk Sergeybtnicus buys prospectsUnless mpcontainer

real    0m20.218s
user    2m6.044s
sys     0m2.849s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

LM ရဲ့ ထုံးစံအတိုင်း same phrase ကိုပဲ input လုပ်ခိုင်းပြီးတော့ predict လုပ်ခိုင်းရင်လည်း တခါနဲ့ တခါ က တူမှာမဟုတ်ဘူး...  

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture KAN --model_path ./weights/model_20240908-081150.pth --model_type gpt-mini --prompt "Is doom'd a "
number of parameters: 31.08M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Is doom'd a configconfig Sylv Sylv Sylvreck pants pants pants pants pants pants Trigger Trigger Trigger Trigger Trigger Update Update Trigger Trigger Trigger Trigger Trigger swapped Update Update Update Update Update Update Update swappedensis Update Updateensis Update Updateensis skirmesh skirmensis skirmeshensis skirm Trigger Triggerensisensis skirmesh skirmesh skirmesh skirm Trigger swappedensis skirm Trigger Trigger Trigger skirm Trigger Trigger Trigger Trigger Trigger skirm Trigger skirmesh skirm Trigger Trigger skirmesh skirm Trigger skirm skirm Trigger skirm Trigger skirm Trigger skirm skirm skirm Trigger Trigger skirmesh skirm Trigger skirm

real    3m11.013s
user    23m1.865s
sys     0m17.846s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

## Testing KAN-GPT, MLP model with Archi: KAN  

Testing လုပ်တဲ့အခါမှာ သတိထားရမှာက MLP နဲ့ training လုပ်ထားရင် MLP နဲ့ပဲ testing လုပ်ပါ။ တကယ်လို့ MLP model ကို KAN archi နဲ့ testing လုပ်ခဲ့ရင် ရလဒ်က လွဲသွားလိမ့်မယ်။   

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture KAN --model_path ./weights/model_20240908-081150.pth --model_type gpt-mini --prompt "Bangalore is often described as the " 
number of parameters: 31.08M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Bangalore is often described as the ayedayedayedayedayedayedayedayedayedayedayed bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulky bulkyTang bulky bulky bulky bulky bulky bulkyTang bulkyTang bulky bulkyTang bulkyTang bulky bulkyTang bulky bulkyTang bulky bulkyTang bulky bulkyTang bulkyTang bulkyTang bulkyTang bulkyTang bulky bulky bulkyTang bulky bulkyTang bulky bulkyTang bulky bulky bulkyTang bulkyTang bulkyTang bulkyTang bulkyTang bulkyTang bulkyTang bulkyforwardTang bulkyTang bulky

real    0m15.490s
user    3m0.342s
sys     0m17.420s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture KAN --model_path ./weights/model_20240908-081150.pth --model_type gpt-mini --prompt "I thought " 
number of parameters: 31.08M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
I thought  JO Vulcan asideJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJustJust

real    0m14.954s
user    3m2.116s
sys     0m18.525s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture KAN --model_path ./weights/model_20240908-081150.pth --model_type gpt-mini --prompt "Is doom'd a " 
number of parameters: 31.08M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Is doom'd a  venues McConnell McConnell McConnellWinnereaneaneanRound001RoundRoundRound001 Whit001 Ship Suppose quitting Neck quitting 123 quitting Ship truly quitting irregular quitting quitting Suppose Ship profitable quitting truly001 Butchervic quitting quitting quitting irregular quitting quitting quittingflix quittingflix quittingflix quitting Neckvic quitting quitting Ship scales Neck truly quitting Sector quitting scales Neck scales Neck scales Neck scales Neck scales Neck Obviously Neck quitting quitting Neck quitting Neck scales Neck Obviously Obviously Obviously Neck Obviously Obviously Neck Obviously truly Obviously Obviously truly contamin Neck Obviously Obviously Neck Obviously Neck unanswered

real    0m14.648s
user    2m50.006s
sys     0m17.166s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

## Check English Datasets

```
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/tinyshakespeare$ wc input.txt 
  40000  202651 1115394 input.txt
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/tinyshakespeare$
```

Check webtext json file:  

```
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/webtext$ head -n 30 ./webtext.test.jsonl 
{"id": 255000, "ended": true, "length": 134, "text": "Is this restaurant family-friendly ? Yes No Unsure\n\nDoes this restaurant accept reservations ? Yes No Unsure\n\nAre the prices at this restaurant mid-range / moderate? Yes No Unsure\n\nIs this restaurant good for dinner? Yes No Unsure\n\nIs this restaurant good for lunch? Yes No Unsure\n\nIs this a Japanese restaurant? Yes No Unsure\n\nCould this location be considered a specialty food market? Yes No Unsure\n\nDoes this restaurant have waiters and waitresses ? Yes No Unsure\n\nIs this restaurant a hidden gem or off-the-beaten path? Yes No Unsure\n\nIs this primarily a bakery ? Yes No Unsure"}
{"id": 255001, "ended": true, "length": 713, "text": "Clinton talks about her time of 'reflection' during sick days\n\nHillary Clinton returned to the campaign trail Thursday afternoon, debuting some new intro music and telling the crowd that her sick days allowed her a chance to \"reconnect with what this whole campaign is about.\"\n\nThe former secretary of state, who took the stage to James Brown's \"I Feel Good,\" spent the beginning of the week at her home in Chappaqua, New York, after being diagnosed late last week with pneumonia. Her campaign initially did not disclose the illness and only did so after Clinton was forced to leave an event early on Sunday commemorating the 15th anniversary of the Sept. 11 terrorist attacks.\n\nStory Continued Below\n\n\"I tried to power through it but even I had to admit that maybe a few days of rest would do me good,\" she told the Greensboro, North Carolina, crowd of her pneumonia. \"And I'm not great at taking it easy, even under ordinary circumstances, but with just two months to go until Election Day, sitting at home was pretty much the last place I wanted to be.\"\n\n\"But it turns out having a few days to myself was actually a gift, I talked with some old friends. I spent time with our very sweet dogs. I did some thinking,\" she continued. \"The campaign trail doesn't really encourage reflection. And it's important to sit with your thoughts every now and then and that did help me reconnect with what this whole campaign is about.\"\n\nClinton compared her own ability to take a handful of sick days to that of many Americans who she said are forced to \"either go to work sick or they lose a paycheck.\" She said those Americans, and others \"living on a razor's edge\" with an aging parent who needs help or without the means to afford a college education, are the reason she is running for president.\n\nSpeaking in North Carolina, Clinton made special mention of the law there forcing transgender individuals to use the bathroom that corresponds with the gender on their birth certificate. The law, seen by many as discriminatory, has prompted the NBA, NCAA and Atlantic Coast Conference to move major sporting events out of the state, costs that the former secretary of state said, \"We can't afford.\"\n\n\"I'm running for the LGBT teenager here in North Carolina who sees your governor sign a bill legalizing discrimination and suddenly feels like a second-class citizen,\" she said. \"And if anyone wonders what is the cost of discrimination are, just ask the people and businesses of North Carolina, look at what's happening with the NCAA and the ACC. This is where bigotry leads and we can't afford it, not here, not anywhere else in America.\"\n\nClinton did not address her opponent, Donald Trump, by name but did spend a significant portion of her remarks laying out many of the contrasts she regularly draws with her opponent. She told the crowd that \"I am actually asking Americans to hold me accountable for my ideas and hold my opponent accountable for his.\"\n\n\"You know, I've been involved in politics. It is not an easy business. It can get rough, and I've built up some defenses. When it comes to public service, I am better at the service part than the public part,\" she said. \"People accuse me of all kinds of things. You probably have seen that. But nobody ever accuses me of quitting. And I will never give up. I'll never walk away. No matter how tough the going gets.\""}
{"id": 255002, "ended": true, "length": 173, "text": "House Majority Whip Steve Scalise has been discharged from the hospital six weeks after sustaining a life-threatening gunshot wound during an attack on a Republican congressional baseball practice in Virginia. He plans to return to Congress after completing \"a period of intensive inpatient rehabilitation.\"\n\nThe full statement:\n\nCongressman Steve Scalise has made excellent progress in his recovery from a life-threatening gunshot wound six weeks ago. Yesterday, he was discharged from MedStar Washington Hospital Center and is now beginning a period of intensive inpatient rehabilitation. He is in good spirits and is looking forward to his return to work once he completes rehabilitation. He and his family are grateful for the care he received from the trauma team as well as the other doctors, nurses, and staff of MedStar Washington Hospital Center. The family also appreciates the outpouring of prayers and support during this time."}
{"id": 255003, "ended": true, "length": 490, "text": "Insight Course: Lesson 14\n\nControl of the Mind\n\nThe truth will set you free, but first it will piss you off. ~ Gloria Steinem\n\nAre you ready for another wild trip down the rabbit hole? Now that we have explored our own deepest personal challenges, it is time to explore what is possibly the deepest challenge facing our planet.\n\nThe term \"mind control\" can bring up all kinds of thoughts and feelings. Yet as with almost any tool, mind control techniques can be used for the good of all of us or used to gain personal benefit at the expense of others.\n\nThough this lesson may be the most disturbing of all for some, it is also vitally important as far as understanding how some of the top secret, sophisticated operations which have a major impact on our world have been carried out. This topic also has some amazing healing applications. These applications and the deeper implications of all this information will be discussed at the end of the lesson.\n\nFirst, you are invited to explore some highly reliable information on how mind control has been used to forward hidden, disempowering agendas in our world. Please watch the revealing, 45-minute History Channel documentary Mind Control: America's Secret War at the link below:\n\nhttps://www.WantToKnow.info/mindcontrolvideo\n\nSome people would rather not know the many potentially disturbing facts about secret mind control programs used to manipulate people and politics around the world. Yet when we collectively choose not to know, those who are abusing these technologies are given free rein to explore further and to cause serious manipulations which lead to even more fear and polarization in our world.\n\nBy choosing to at least understand the basics of what is going on, we can come together to stop the destructive behavior and invite others to join us in working together for what's best for all on our planet. For the best concise summary of secret mind control programs, please read the two-page essay below:\n\nhttps://www.WantToKnow.info/mindcontrol\n\nSacred Cows\n\nDon't ignore the bad stuff, but make a point of celebrating the beautiful stuff with all the exuberant devotion you can muster.\n\n~ Rob Brezsny in his fun, profound book Pronoia is the Antidote for Paranoia\n\n\nTo Complete Insight Course Lesson 14: Click Here"}
{"id": 255004, "ended": true, "length": 220, "text": "BY JENNIE MCNULTY\n\nLesbian.com\n\nYou know Weinstien and Spacey, and Louis and Tambor,\n\nLauer and Charlie, and Franken and Roy Moore\n\nBut do you recall,\n\nThe most harmful predator of all?\n\nDonald the groping gasbag\n\nHad some really tiny hands,\n\nFor those that had to feel them,\n\nJail should be the place he'd land.\n\nAll of the media perverts\n\nHad to quit and lost careers;\n\nMeanwhile, the sleaze ball Donald\n\nScrews us like a racketeer.\n\nThen one foggy Christmas eve,\n\nMueller came to say:\n\n\"Donald all your lies and fraud\n\nMake your case severely flawed.\"\n\nThen all his buddies made deals,\n\nThey began to cop a plea,\n\nDonald the gas bag groper\n\nEnjoy the penitentiary.\n\nJennie McNulty was named one of Curve magazine's Top 10 lesbian comedians."}
{"id": 255005, "ended": true, "length": 198, "text": "The Buddha's Teaching As It Is\n\nIn the fall of 1979, while living at the Washington Buddhist Vihara, Ven. Bhikkhu Bodhi gave a series of lectures on the fundamental teachings of Early Buddhism. Bhante Gunaratana, at the time the President of the Buddhist Vihara Society, suggested he record the lectures so that the Vihara could distribute them as a set of cassette tapes.\n\nIn the summer of 1981, Ven. Bodhi recorded his ten lectures in the basement of the Washington Buddhist Vihara, using an ordinary, nonprofessional recorder. An enthusiastic lay supporter had the master copies reproduced in large quantities for expanded distribution. They have continued to be distributed on tape and as CDs for over twenty-five years, and are considered \"public domain\" for anyone to copy and distribute freely. The one condition is that they must not be sold.\n\nWe recommend that the first time you listen to them, you listen to them in their proper sequence:"}
{"id": 255006, "ended": true, "length": 365, "text": "As part of a broad initiative to combat sexual harassment and assault, French President Emmanuelle Macron promised to make \"gender-based insults\" punishable by law.\n\nAs France24 reports, Macron outlined his plans in a speech marking the International Day for Elimination of Violence Against Women. \"The streets should not become hell for the women of France,\" he said. Macron noted that the Ministry of the Interior has launched consultations that will lead to new measures \"in a few weeks' time.\"\n\n\"We will \u2026 be creating an offense which will give the police the right to issue fines if there is a verbal attack on a woman,\" he said.\n\nThe future draft law may also include a number of measures that will make it easier for sexual assault victims to report to police\u2014measures like extending the statute of limitations for the rape of minors from 20 to 30 years, and allowing rape victims to make their initial complaints on online.\n\nIn an effort to help women get home safely, the law may implement an \"on demand\" service for public transit, which would let women ask buses to stop anywhere along their route at night.\n\n\"Let's seal a pact of equality between men and women,\" Macron said, adding that when it comes to sexual harassment and assault, \"it is essential that shame changes camp.\"\n\nIn France, half of all women, according to France24, say they are victims of sexual assault. Despite recent progress, it's still a difficult topic for women to discuss. Below watch a video in which several women talk about their experiences with sexual harassment and assault, including a shocking experience a woman named Mara had on a city bus.\n\nRead the full story at France24.\n\nRelated\n\nGender equality minister in France proposes instant fines for street sexual harassers"}
{"id": 255007, "ended": true, "length": 184, "text": "The Atlanta Falcons have started the 2015 season 4-0 under new head coach Dan Quinn. Quarterback Matt Ryan has the most passing yards in the NFC South while receiver Julio Jones is having quite a start, too.\n\nAnd according to ESPN's \"First Take,\" the Football Power Index has the Falcons as the team with the best chance to finish the season 16-0.\n\nHowever, ESPN is asking: Where are all the Falcons fans?\n\nFan correspondent, Reese Waters, walked the streets of Atlanta trying to find Falcons fans, which seemed to be easier said than done.\n\n\"I support the Braves and the Hawks ... I'm a Saints fan,\" one man said.\n\nWhen asked what's the happiest you've ever been as a Falcons fan, one man said: \"When we beat them Saints, when we beat them Saints, baby.\"\n\nSee the full video below:"}
{"id": 255008, "ended": true, "length": 253, "text": "Front Page Torrents Favorites My Home My Galleries Toplists Bounties News Forums Wiki HentaiVerse\n\n[Spiritus Tarou] Issho ni Ite yo | Together With You (COMIC JSCK Vol. 5 2016-07) [English] =CW + TLL= [\u30b9\u30d4\u30ea\u30bf\u30b9\u592a\u90ce] \u4e00\u7dd2\u306b\u3044\u3066\u3088 (\u30b3\u30df\u30c3\u30af\u30b8\u30a7\u30b7\u30ab Vol.5 2016\u5e747\u6708\u53f7) [\u82f1\u8a33]\n\nYou have to register before you can add comments.\n\nPosted on 31 May 2018, 08:58 UTC by: kiwino\n\nBase +5, mrwayne +14 , Ice_Cream +11 , The Lost Light +8 , THDragon +14 , MomentoMori009 +2 , RedResistance +5 , Anony12788 +9 , MechWarriorNY +7 , SW_CGF +6 , Drake68655 -6 , nodire +6 , firedragon89 +11 , and 1 more...\n\n[Front Page]\n\nPlease read the Terms of Service before participating with or uploading any content to this site."}
{"id": 255009, "ended": true, "length": 55, "text": "They have changed the phone menu to try to deflect us to email, but you can still get a live person by navigating to file a complaint.\n\nShe didn't sound happy that I figured it out, but they aren't concerned about making us happy, are they?"}
{"id": 255010, "ended": true, "length": 103, "text": "One Page\n\nOne Page is a browser extension for automatically displaying multi-page news articles on a single page.\n\nReporting new websites that split articles on multiple pages can be done with one mouseclick. Or of course by creating an Issue or Pull request at GitHub\u2026\n\nDownload extension\n\nOne Page for Chrome\n\nOne Page for Firefox (not validated yet)\n\nOne Page for Edge will be published as soon as Microsoft allows the upload of extensions to the Windows Store\n\nSupported Websites"}
{"id": 255011, "ended": true, "length": 814, "text": "Intro \"In his search for food, early man tried all kinds of plants. Some nourished him, some, he found cured his ills, and some killed him. Few, to his surprise, had strange effects on his mind and body, seeming to carry him onto other worlds. We call these plants hallucinogens, because they distort the senses and usually produce hallucinations--experiences that depart from reality. Although most hallucinations are visual, they may also involve the senses of hearing, touch, smell, or taste--and occasionally several senses simultaneously...\"\n\n1 Schultes, The compounds that we call \"hallucinogenic\" are drugs that modify the function of the central nervous system by altering the input from the senses and changing the mood and behavior of the individual. These short term effects have caused some concern among our parents and leaders, but it is the long term influence that we will consider here. \"In the history of mankind, hallucinogens have probably been the most important of all the narcotics. Their fantastic effects made them sacred to primitive man and may even have been responsible for suggesting to him the idea of deity.\"\n\n2 Schultes, Dr. Richard Evan Schultes was no drug crazed hippy, but a respected Harvard professor with impeccable credentials. It was apparent to Dr. Schultes that hallucinogens were deeply involved in early religions. He also understood that to broadcast such views could be hazardous to one's career. Hence he confined his revolutionary discovery to one line in a popular guide to plant identification rather than publishing in some academic journal. When etymologist John Allegro went public with his discoveries linking early Christianity to hallucinogenic mushrooms, his career was ruined. It is indeed a subject that can cause deep emotional reaction. That was one of the early tipoffs that something important was going on here. There were such extreme reactions to inquiries about mushrooms that researchers had to come up with terms to describe mushroom haters and lovers. Whole cultures can be categorized by their view as to whether certain mushrooms are considered food or poison. Besides religion, the study involves ritual cannibalism, sex, and behavior modification. All of this is dangerous territory and may cause strong emotional reactions in the reader. If you DO have an emotional reaction to any of this material, you should sit very still, breath deeply and try to relax. Try to identify your feelings. Are you feeling anger? Frustration? Fear? Hatred? If these feelings are strong, you may want to quit reading. But please don't be mad at me. I'm just telling it like I see it. A certain amount of denial is necessary for survival in these troubling times. In order to function we all need a solid emotional state from which to operate. Like it or not, our basic beliefs, our \"World View\", is a major component of said state. Messing with your core beliefs can be tricky business. It hurts. It can cause damage; but so can ignoring the Truth. The trick is to use denial to keep your peace of mind, being careful not to be crushed by the Truth when it lands on you. Our beliefs are what holds us together. When the leaders we trust turn out to be liars, thieves and murders, it can shake our confidence and certainly be painful. The feeling of betrayal can lead to nearly uncontrollable anger. When our Gods betray us, it may be too much for some people to bear. Some folks might be better off if they just pass on this material and stick to their beliefs. Proceed at your own risk. However, if you are a seeker, and serious about \"meaning of life\" issues, you can't afford to turn back now. <- About | Next -> Sources\n\n\nClick on Author to return to quoted text. 1 Schultes, Hallucinogenic Plants, Golden Press, New York, 1976, p 5.\n\n2 Schultes, Hallucinogenic Plants, Golden Press, New York, 1976, p 5."}
{"id": 255012, "ended": true, "length": 359, "text": "Having trouble viewing the video? Try disabling any ad blocking extensions currently running on your browser.\n\nYou are not allowed to watch this stream ='(\n\nSALT LAKE CITY \u2014 Police on Monday identified a man killed Saturday evening in a shooting in Sugar House.\n\nAbout 7 p.m. Saturday, a motorist driving near 1224 E. Parkway Ave. noticed a man lying on the ground unconscious and not breathing. The motorist called police after realizing the man, later identified as Christian McDonald, 24, of West Valley City, had been shot in the torso.\n\nMcDonald was taken to a local hospital where he was pronounced dead, according to Salt Lake Police Sgt. Robin Heiden.\n\nOn the scene, police found a handgun with McDonald, as well as a blood trail leading a block east to Elizabeth Street.\n\nUpon further investigation, police discovered McDonald was with another man in the area. The two got into an altercation and shot each other, Heiden said.\n\nThe other man went to a local hospital, where staff contacted police. The man has not been arrested, but police have identified him, according to Heiden. She said the man's relationship with McDonald is unclear and the investigation is ongoing.\n\n\"It wasn't a random event,\" Heiden said.\n\nWe're sorry, currently this live video stream is only available inside of Utah or an approved RSL broadcast territory. We base your location on your IP address. Some providers IP addresses may show your location outside of the state, even though you are physically within the state boundaries. For more information about RSL on KSL, please see our FAQ.\n\nPhotos\n\nRelated Stories\n\nMorgan Jacobsen\n\n0 Pending Comments"}
{"id": 255013, "ended": true, "length": 953, "text": "Get Liverpool FC updates directly to your inbox Subscribe Thank you for subscribing We have more newsletters Show me See our privacy notice Could not subscribe, try again later Invalid Email\n\nEl-Hadji Diouf has reignited his war of words with Steven Gerrard, following the Liverpool legend's retirement on Thursday, declaring: \"He was nothing\".\n\nEx-England international Gerrard, now 36, called time on his illustrious playing career, following his 18-month sojourn with LA Galaxy.\n\nTributes have poured in to the Anfield icon, who led the Reds to their fifth European Cup success in 2005.\n\nHowever, Diouf has not joined those hailing Gerrard, a player he has previously called an 'egotist' and accused of racism.\n\nThe pair spent two years as teammates at Anfield following Diouf's \u00a310million arrival in June 2002, signed by Gerard Houllier, but Diouf struggled on Merseyside and Gerrard wrote in his 2015 autobiography that the Senegalese \"did not care about football and about Liverpool.\"\n\n(Image: SFR Sport)\n\n(Image: Getty Images)\n\nDiouf, now 35, speaking on French television, has now declared that \"the man, I do not respect.\"\n\nHe told French TV channel SFR Sport: \"People told me at Liverpool, there was some guys you could not touch, but I touched them. That is why it was complicated for me.\"\n\nFormer Arsenal midfielder Emmanuel Petit, alongside Diouf on TV show 'La Vestiare' questions: \"Are you talking about Steven Gerrard?\"\n\nDiouf responded: \"I do. Stevie G and Jamie Carragher, the two scousers.\"\n\nAsked about Gerrard's autobiography comment, Diouf responded: \"He was right, I am not a scouser. I did not come to Liverpool to buy a house and live there in the future.\"\n\n(Image: SFR Sport)\n\n(Image: Daily Mirror)\n\nThen, he advances his criticism of the ex-Liverpool skipper.\n\n\"When I arrived I showed him he was nothing at all,\" said Diouf. \"He was nothing at all.\n\n\"I asked him to tell me in which big competition, Euros or World Cup, people think about him.\"\n\nAs World Cup winner Petit struggled to recall Liverpool's 2005 Champions League success, Diouf exclaimed: \"Here is the proof, even you cannot remember.\n\n\"You are talking about Euros and World Cup. Today I owe you respect [Petit], I owe respect to Mr Zidane because you did win the World Cup.\"\n\n(Image: Getty Images)\n\n(Image: Getty Images)\n\nPetit fires back, hailing Gerrard as \"an immense player\", but Diouf counters, declaring that his issues with Gerrard are with the man, not Gerrard the player.\n\n\"I repeat. I respect the player, very big player, but the man, I do not respect. And I told him, I let him know that.\n\n\"With all my respect I let him know. For me in Liverpool, he was not just a player like anyone else. He had to work and play his football as I had to work and play my football.\n\n\"Then as you know, there were some brown-nosers, who went to the manager to repeat what I said. That was the real problem. When Gerrard did that, we had an argument, like real men.\n\n\"That is why he does not like me. He knows I say what I think, that when it is not right, no problem, I am up for it.\n\n\"He could not, he was afraid of looking into my eyes. He was afraid of talking to me. Let's not forget when I arrived I did not ask for his shirt. He asked for my Senegal shirt for one of his mates.\"\n\n(Image: CW PicDesk)\n\nDiouf also revealed that he owes a debt of gratitude to his former Lens coach Roland Courbis, who convinced Gerard Houllier to take a chance on the Senegalese forward.\n\n\"If I signed to Liverpool, it is thanks to him. I had not played the World Cup or AFCON [African Cup of Nations] yet.\n\n\"Roland said to Gerard, 'there is a kid you could be interested in, sign him, sign El Hadji Diouf.\n\n\"Gerard came to see me in Lens, to talk to me, and then I started to dream.\""}
{"id": 255014, "ended": true, "length": 83, "text": "Super Mario Run will be available on Android devices beginning in March, Nintendo has announced. For those that missed it, pre-registration can be done here.\n\nSuper Mario Run originally arrived on iOS last month.\n\nSource\n\nShare this: Twitter\n\nFacebook\n\nReddit\n\nTumblr\n\nGoogle\n\nMore\n\nEmail\n\nPrint\n\n\nLinkedIn\n\nPinterest\n\n\nPocket"}
{"id": 255015, "ended": true, "length": 836, "text": "The California-based electric car manufacturer joins Jaguar, Land Rover and BMW's Mini as brands opting to drive past the 2016 Detroit auto show after having a presence on the main show of Cobo Center in 2015. (Photo: Susana Bates / AFP/Getty Images)\n\nTesla Motors Inc. is the most recent automaker to bow out of next month's 2016 North American International Auto Show in Detroit.\n\nThe California-based electric car manufacturer joins Jaguar, Land Rover and BMW's Mini as brands opting to drive past the 2016 show after having a presence on the main show of Cobo Center in 2015.\n\nA Tesla spokesperson confirmed the move on Friday.\n\n\"After much consideration, we have decided against participating at the North American International Auto Show. We've always had a very good experience at Detroit,\" a company spokesperson said in a statement.\n\n\"In Michigan, we have great owners, a strong supercharger network that connects the U.S. with Canada, and are continuing to hire talented employees. But as a small player, Tesla relies on auto shows to not only showcase our products, but engage with consumers and ultimately sell more cars in the region. We are working to change laws so that we are licensed to open stores and service vehicles. Until that happens NAIAS is not an optimal venue for driving our mission to put more EVs on the road.\"\n\nThe decision is in-line with comments made by Diarmuid O'Connell, Tesla vice president of business development, on Nov. 20 in Detroit. He said he wasn't sure if the company would have a presence at the Detroit show and hinted the costs associated with a show might be too much especially since Tesla can't sell its vehicles in Michigan.\n\n\"The truth is there is a cost associated with being at these shows. And if you're trying to sell cars, that makes sense,\" he told reporters. \"Making the huge investments that go into setting up these booths and the staffing over the course of two weeks, particularly in a state like Michigan where we can't even sell cars, begs some questions.\"\n\nMax Muncey, the show's public relations manager, confirmed that Tesla informed officials that the company was not planning to purchase space on the show floor. A Tesla spokesperson could not immediately be reached for comment.\n\n\"I'm very confident we will quickly fill that space,\" Muncey said. \"We're in talks with other automakers and partners. There's a lot of interest.\"\n\nO'Connell last month said Tesla's newest car \u2014 the Model 3 \u2014 is expected to go into production by the end of 2017 and consumers will get to see the car in March 2016, which is around the time of the New York International Auto Show.\n\nBoth Jaguar Land Rover and Mini cited the Detroit auto show not aligning with their respective brand strategies.\n\nHelping fill the voids will be newcomer the Robb Report and Aston Martin, which will return to the show for the first time since 2009.\n\n\"They don't attend any other auto shows, so to bring them back to the show was a great partner to have,\" Muncey said.\n\nThe Robb Report \u2014 recently purchased by prominent Detroit businessman Dan Gilbert, founder of Quicken Loans \u2014 is a magazine that features high-priced products.\n\nThe 2016 Detroit auto show is open to the public from Jan. 16-Jan. 26. Thousands of news media from more than 60 countries and industry officials also attend the show prior to it opening to the masses.\n\nSetting up the multimillion dollar stages, lighting and displays takes three months. Crews started preparing the space in mid-October. Event organizers say this year's setup is particularly important, as about 75 percent of the show floor will be all-new or significantly redesigned for the more than 40 expected worldwide debuts.\n\nmwayland@detroitnews.com\n\n(313) 222-2504\n\nStaff Writer Melissa Burden contributed\n\nRead or Share this story: http://detne.ws/1QiDEEt"}
{"id": 255016, "ended": true, "length": 92, "text": "The Owings Mills Mall in Maryland officially closed its doors in 2015, with the final store closing in 2016. The mall, which once hosted 155 stores and eateries, is now being demolished. These images are part of an ongoing project by photojournalist Seph Lawless , called Autopsy of America , which aims to document America's most abandoned and forgotten ruins. Take a look at some of the last images ever taken of the Owings Mills Mall."}
{"id": 255017, "ended": true, "length": 88, "text": "I've easily purchased 25 of these over the last 3 years. I use them in the Micro Slow sticks that I build and beef up to fly fast for other RC guys. I've never had one burn out. The weak point is the shaft, which will bend if it takes a hit. Beside that weak area, this motor is tough and powerful with a 7\" prop and a 3's lipo with a high C rating."}
{"id": 255018, "ended": true, "length": 372, "text": "Sevilla midfielder Hiroshi Kiyotake has re-signed with former club Cerezo Osaka, an official of the J. League first-division side said Wednesday.\n\nCerezo team director Kiyoshi Okuma said Kiyotake will return on a full transfer as the winter transfer market closed Tuesday. Cerezo have been promoted to the J. League top flight for this season.\n\nThe 27-year-old will come back to Japan for the first time since the summer of 2012, when he left Cerezo for Nuremburg in the Bundesliga.\n\nKiyotake signed with Sevilla at the start of the season from German outfit Hannover, but has been limited to just four La Liga appearances. His last game came on Dec. 21 in the Copa del Rey.\n\nUnable to work his way back into the team with Sevilla contending for the league title, just four points behind leader Real Madrid, Kiyotake's days in Spain appeared to be numbered.\n\nShibasaki joins Tenerife\n\nKYODO\n\nKashima Antlers midfielder Gaku Shibasaki has signed for Tenerife in the Spanish second division on Tuesday after his proposed transfer to La Liga side Las Palmas fell through.\n\nThe 24-year-old Shibasaki was expected to join Las Palmas by Tuesday's winter transfer deadline after he flew to Spain on Saturday for final negotiations. But Las Palmas had been juggling multiple potential signings and in the end, opted not to sign Shibasaki.\n\nKashima was willing to take him back, but Shibasaki stood firm on playing abroad and now joins another side in the Canary Islands, off the western coast of Africa. Tenerife is currently sixth in the table and in a promotion playoff spot."}
{"id": 255019, "ended": true, "length": 514, "text": "There's constantly some sort of plagiarism row going on in fashion. Whether it's Mango copying Gucci's silk dresses, Nasty Gal copying Saint Laurent's platform sandals, designer's copying other designers, artists or, as was most recently the case, the designs of indigenous cultures and tribes. Last week, London-based fashion label KTZ were in hot water over the \"Shaman Towelling Sweatshirt\" featured in their AW15 collection \u2013 a design which Salome Awa says was copied from her great-grandfather Aua, one of the last Shaman of the Canadian Inuit.\n\n\"They must have seen it and copied it,\" Awa told The Evening Standard, \"They even called the clothing Shaman... My great-grandfather was a very powerful and respected man and he has been used and violated. It was disgusting to see a sacred design used as a sweater... We are a proud people and our ancestors and traditions are very important to us. The way they have taken and degraded this design is unacceptable.\" The design itself featured in 2006 film The Journals of Knud Rasmussen as well as some books on the culture of the Inuit such as \"Northern Voices\".\n\nIn response KTZ, who show at London Fashion Week, have issued a formal apology to Awa saying the brand has \"always been inspired by and paid homage to indigenous cultures and tribes around the world\" and that it's part of their DNA to \"celebrate multiculturalism as a form of art and to encourage appreciation for traditions, ethnicities and religions' diversity\". As well as emphasising the multiculturalism of their company, they said that the Inuit community was credited in the press release and that they have already removed the item from sale.\n\nAwa's response to the apology was bittersweet, telling CBC North, \"\"I'm kind of happy about it but sad at the same time... They didn't even mention an apology to my great-grandfather and they didn't even offer any monetary gains to our family... This is a stolen piece. There is no way that this fashion designer could have thought of this exact duplicate by himself.\" Awa goes on to say that she has some questions from the brand. \"Why did you not ask us in the first place?\" she asks. \"How they obtained the exact replica? Why did they not ask our family? Did they not think we exist? Why are they doing this to other indigenous clothing?\"\n\nRead KTZ's full letter to Salome Awa below:"}
{"id": 255020, "ended": true, "length": 680, "text": "Written by and copyright \u00a9 2005-2018 by Thomas N. Bulkowski. All rights reserved. Disclaimer: You alone are responsible for your investment decisions. See Privacy/Disclaimer for more information. Some pattern names are the registered trademarks of their respective owners.\n\nStatistics updated on 8/17/18\n\nFor more information on this pattern, read Encyclopedia of Chart Patterns Second Edition , pictured on the right, pages 149 to 163. That chapter gives a complete review of the chart pattern, compared to what is described below.\n\nCup-with-Handle\n\nImportant Bull Market Results for Cup with Handle Overall performance rank (1 is best): not ranked Break even failure rate: 5% Average rise: 52% Throwback rate: 62% Percentage meeting price target: 62% The above numbers are based on 912 perfect trades. See the glossary for definitions.\n\nCup with Handle Identification Guidelines\n\nCharacteristic Discussion Price trend Upward leading to the pattern. I use a 6-month look back (high to high). If price is higher at pattern start than 6 months ago, then I accept it. Otherwise, I visually check to see it's in a short-term uptrend. I no longer require a 30% upward move. Shape A rounded turn that looks like a cup with a handle on the right. U-shaped cup The cup should be U-shaped, not V-shaped. Handle The cup must have a handle on the right. Cup duration From 7 to 65 weeks Handle duration 1 week minimum with no maximum. Handle Forms in upper half of cup. Cup Cup rims should be near the same price level but be flexible.\n\nCup with Handle Trading Tips\n\nConsult the associated figure on the right.\n\nTrading Tactic Explanation Measure rule Measure the height from the right cup lip ( A ) to the lowest valley ( B ) then multiply by the above 'percentage meeting price target.' Add the result to the breakout price ( A ) to get a target. Inner cup Cups often form within cups (points 1 and 2 ), so trade the inner cup when price rises above the handle (the dashed green line at point 3 ). Trendline If possible, draw a down-sloping trendline along the handle peaks. A close above the trendline signals an early buy. I show this as the blue line extending down from point A on the chart to the right. Buy Buy when price closes above the right cup rim (point A , and the top horizontal red line). Stop The handle low (point C ) is a good place to put a stop. Raise the stop as price rises. Throwbacks Throwbacks hurt performance. Short handle Stocks with handles shorter than the median 22 days show superior post breakout performance. The Measure Rule\n\nCup with Handle Example\n\nThe figure on the right shows an example of a cup with handle chart pattern. The rise leading to the cup with handle begins at C and reaches the left cup lip at point A . Since this is on the weekly scale, the price chart appears narrower than usual, but price rounds downward forming a cup with the right cup lip at B . The handle lasts a few weeks before price begins moving up. The next week, price rockets upward about seven points.\n\n-- Thomas Bulkowski\n\nOther Cup with Handle Examples"}
{"id": 255021, "ended": false, "length": 1024, "text": "The Wolf currently has the former Seminole as his RB33, but expect Dalvin Cook to get a gigantic bump in the rankings after taking advantage of Latavius Murray's absence during the first week of training camp. Cook is catching the eye of his teammates and coaches, and currently possesses workhorse potential in Minnesota.\n\nA succession of poor decisions off the field, ball security issues on the field and a mediocre combine dropped the uber-talented Dalvin Cook all the way to pick No. 41 to the Minnesota Vikings \u2014 who let Vikings legend and seven-time All-Pro Adrian Peterson walk in free agency, while adding goal line hammer Latavius Murray in March.\n\nAfter Christian McCaffrey came off the board, us at the Roto Street Journal were pleading for a team like the Bucs, Raiders or Packers to select Cook. Once the Vikings drafted Cook, the fantasy community broke out in a cold sweat. Minnesota does very little to help out their running backs: from their porous offensive line, to their up-and-down passing situation and blah-scheme, it's tough to be a running back for the purple and gold.\n\nThe Wolf was especially hurt by this combination, stating:\n\nCook landed in arguably the worst spot possible with Minnesota. Indeed, the talent is there, but that's about all he has working in his favor. The team dished out oodles of money for Latavius Murray, who will undoubtedly be involved, especially near the stripe. Additionally, the line is among the worst in football, and there's little else really threatening defenses or creating TD opportunities. Throw in a bland, vanilla scheme, and Cook will be relying on his own high-end abilities to produce any fantasy value in 2017.\n\nAlthough Murray had the highest percentage of carries inside the 5-yard line last season (81.8 percent in Oakland), we didn't take the severity of his ankle injury into account before grading out Cook's situation. The reason why Murray took multiple free agent visits was to prove to teams in person that the bone spurs in his ankle were not serious, and the Vikings took the bait. The former Raider underwent surgery on his ankle a week after signing and was expected to be ready for the start of training camp.\n\nFast forward to the start of training camp, and Latavius Murray is still MIA. In fact, on July 31st, Murray put no timetable on his return and would only commit to the regular season. After missing the entire offseason program and the start of camp with his new team, a frustrated Murray stated that he's \"behind the 8-ball.\" He went onto say, \"if I'm not healthy, there's no point in me being out there. If I'm not good out there, I can't help the team regardless.\"\n\nMeanwhile, the rookie running back is taking full advantage of his opportunity by taking the majority of the first team reps and he's caught the attention of his teammates and coaches.\n\n\"The first thing the veteran players I've talked to about him say is, 'This guy gets it.'\" coach Mike Zimmer explained after a practice. \"He understands protections, he works hard, they see how he interacts in the locker room, and that's part of it. And then, when you have a special player\u2014like when we got [linebacker Anthony] Barr\u2014they say, 'Hey, man, this guy is different than other guys.' \"That's kinda how he is. They see him out there on the field with the other guys, and it's like, 'There's something different about this guy, the way he runs, accelerates, the creases he can get to.' He's got a tough mentality. Players can see exceptional athletes. When they go out there and they're going against guys, they can see: This guy is pretty good.\"\n\nAs one can see, it's safe to say that Dalvin Cook has earned the staff's trust, and with Murray still sidelined, he's truly entering a workhorse role. The cause for concern is still there, as he has a tendency to fumble, and once Murray joins the team, he's likely to vulture 7-10 touchdowns from the 5-foot-10, 210 lb rookie. The offensive line still sucks and the scheme is still as vanilla as can be, but with his elite pass catching skills, he could definitely see 250-plus touches. In fact, Vikings beat writer Matt Vensel of the Star Tribune said, \"don't rule out\" 300 touches for the rookie.\n\nCook will bring big-play ability (10 50-plus yard runs at Florida State), elite hands for a runner (79 receptions in three seasons) and every-down potential (766 touches in three seasons) to a Vikings team that desperately needs a legitimate playmaker. Don't forget about his blazing speed, which was on display when he dusted cornerback Xavier Rhodes \u2014 and his 4.4 40 speed \u2014 down the sidelines during"}
{"id": 255022, "ended": false, "length": 1024, "text": "The Obama administration is being slammed from all sides for its failing strategy against ISIS\u2014and rightly so. But amid all the scorn, one question has yet to be asked about the resiliency of the terror army, which actually goes to the heart of its decade-old war doctrine. Namely: Does ISIS actually win even when it loses?\n\nThis isn't an academic issue. America's allies in the ISIS war are gearing up for a major counteroffensive against the extremist group. That assault that could very well play right into ISIS's hands.\n\nHaving superimposed its self-styled \"caliphate\" over a good third of Iraq's territory, in control of two provincial capitals, ISIS is today in the strongest position it has ever been for fomenting the kind of sectarian conflagration its founding father, Abu Musab al-Zarqawi, envisioned as far back as 2004.\n\nZarqawi's end-game was simple: by waging merciless atrocities against Iraq's Shia majority population (and any Sunnis seen to be conspiring with it), Zarqawi's jihadists would have only to stand back and watch as radicalized Shia militias, many of whose members also served in various Iraqi government and security roles, conducted their own retaliatory campaigns against the country's Sunni minority. Internecine conflict would have the knock-on effect of driving Sunnis desperately into the jihadist fold, whether or not they sympathized with the ideology of al-Qaeda in Iraq, Zarqawi's franchise and the earliest incarnation of what we now call the Islamic State.\n\nIndeed, in the mid-2000s, the Jordanian jihadist nearly got what he wished for by waging spectacular terror attacks against Shia civilians and holy sites, such as the Golden Mosque in Samarra, a strategy which quickened devolved Iraq's violence from a primarily anti-American insurgency into all-out civil war. The only stopgap for a truly apocalyptic or nation-destroying result was the presence of nearly 200,000 U.S. and coalition troops. Today, however, absent such a foreign and independent military presence, the main actors left in Iraq are the same extremists\u2014Shia militias and ISIS.\n\nThis fact was only driven home last week after thousands of U.S.-trained Iraqi Security Force personnel, including the elite counterterrorist Golden Division, fled from Ramadi, allowing the city fall to a numerically modest contingent of ISIS jihadists. Having been initially instructed by Iraq's Prime Minister Haider al-Abadi to refrain from defending the city (no doubt at the prompting of Washington) the Hashd al-Shaabi, the umbrella organization for these Shia militias, now say they are prepping a massive counteroffensive to retake Ramadi. It promises to be a drawn-out and highly fraught counteroffensive, pitting paramilitaries\u2014which have been accused of war crimes and atrocities by Human Rights Watch, Amnesty International and United Nations Office of the High Commissioner for Human Rights\u2014against genocidal ISIS militants.\n\nMany Iraqis fear, with good reason, that this counteroffensive will also extend to Sunni civilians who will now be branded \"collaborators\" of ISIS, as they have in previous Hashd-led operations. The result: torture, extrajudicial killing, and ethnic cleansing. Nothing would better serve the ISIS narrative or legitimate its claim to be the last custodian and safeguard of Sunni Muslims in the Middle East. Such an outcome might even precede the eventual disintegration of the modern state of Iraq into warring ethno-religious enclaves. That this was ISIS's plan all along adds yet another grim paragraph to the obituary of American-hatched adventurism in the Middle East.\n\nTrue, Hashd al-Shaabi has routed ISIS elsewhere before, namely in Amerli and Jurf al-Sakhar and Tikrit. In the aftermath, the militia was accused of committing human rights abuses, but those accusations didn't tear the country apart.\n\nThe difference with Ramadi, however, is one of both scale and symbolism. This city of close to 200,000 is dead center in the Sunni heartland of Iraq, where ISIS has the home advantage. Ramadi was also, not coincidentally, the cynosure of the so-called \"Anbar Awakening,\" which saw hundreds of thousands of Sunni tribesmen rise up against ISIS's predecessor, al-Qaeda in Iraq, in a cautious but fruitful partnership with American soldiers in the mid-2000s, a grassroots counterinsurgency whose gains were then solidified by the \"surge\" orchestrated by U.S. commander General David Petraeus. This time, absent any American combat forces, there are Shia Islamists who have never before tread into Ramadi. Many Iraqis dread the consequences.\n\n\"Iraq is not unified,\" Iraq's former Deputy Prime Minister Rafe Essawi, a senior Sunni political leader originally from Anbar, told The Daily Beast. \"Fifty percent of the country belongs either to Kurds or ISIS, and 50 percent belongs"}
{"id": 255023, "ended": true, "length": 243, "text": "The nonpartisan Congressional Budget Office reinforced what private-sector economists have been saying for months: The best proposals to spur the economy would cost the government but prove better at quickly creating jobs than pursuing an anti-regulatory policy as proposed Republicans in Congress.\n\nCBO Director Douglas Elmendorf said extending unemployment benefits or payroll tax breaks to those who are most likely to spend the money, as well as providing as tax credits to companies that hire new workers, are among the types of policies that could best boost the economy and create jobs. Rolling back regulations would not have the same immediate jolt, according to a new report.\n\n\"The economic effects of certain changes in regulatory policies probably would be too small or would occur too slowly to significantly alter overall output or employment in the next two years,\" Elmendorf wrote this week on the CBO blog.\n\nThe CBO's analysis comes as Congress is deeply divided over the best approach for strengthening the sluggish economy at a time when jobs are the top issue on voters' minds. The congressional super committee is also struggling to reduce deficits. The report offered a gloomy outlook under current policies, with an estimated 9% unemployment rate through 2012 and economic growth lower than potential."}
{"id": 255024, "ended": true, "length": 85, "text": "\"The attrition rate, even very high up in the draft, is staggering. It might be 50 percent of first-rounders that actually become good major league players. And that probably drops by half once you get into the second round. And it probably drops by half again when you get into the third round. Those top-round picks, there still is an awful lot of fallout.\"\n\n\u2014 Paul DePodesta"}
{"id": 255025, "ended": true, "length": 901, "text": "Major events in the history of SGI and Priesthood\n\n\n1941\n\n\nDivision between Soka Kyoiku Gakkai and the priesthood surfaced because of the priesthood's obedience to the authorities' demands during the II World War to regard the Emperor as superior to the Buddha.\n\n\n1952\n\n\nAfter the war ended, the second president, Mr Toda was banned in 1952 from entering the Head Temple, because of Soka Gakkai's youth demand of an apology from a priest who cooperated with the military authorities.\n\n\nToda wrote: \"I thought I'd receive a reward for my loyalty in rebuking slander of the Law, but instead of praise, they handed me a reproof: 'You're banned from visiting the head temple!' My disciples replied in unison, 'Then we won't visit either, so there!'\" People are Sovereign\n\n\n1979\n\n\nThe priesthood banned P. Ikeda from giving guidance, demanded his resignation from presidency, and demanded absolute obedience of the organisation to the priesthood. P.Ikeda turned that setback into a victory through focusing on world wide movement and strengthening SGI.\n\n\nDespite the pressure and harassment, lay believers never stopped assisting the Head Temple, donating land, buildings and branch temples: \" \u2026the Soka Gakkai built a total of 356 temples, of which 320 were built while I was president. Also, over the years, we conducted countless group pilgrimages to the head temple \u2013 the aggregate attendance coming to more than 70 million\".\n\n\nPeople are Sovereign\n\n\n1980-s\n\n\nMany members were questioning the conduct and the expensive life style of some priests (using members donations), Ordinary members raised their complaints about local priests excessive demands for conducting spiritual services, such as at marriages or prayers for the deceased (and which required considerable donations).\n\n\nTogether with the monopoly on issuing Gohonzon, the priesthood objected to considering lay believers as one of the Three Treasures (being: the Buddha, the Law and Samgha or the Community of Practitioners), asserting that the Treasure of Community is that of the Priests-only. Another matter of disagreement was the concept of Heritage of the Law, with the priesthood asserting that the heritage belongs only to one person (the High Priest), excluding laity.\n\n\n1990\n\n\n\"Then, in December, as 1990 was rapidly drawing to a close, the priesthood suddenly sent the Soka Gakkai with a letter of inquiry. It contained a list of the most ridiculous charges \u2013 such as the accusation that singing Beethoven's great hymn to universal human freedom, 'Ode to Joy', constitutes 'praise for non-Buddhist teachings'.\n\n\nFurthermore, the priesthood demanded a response to their charges within seven days\". People are Sovereign\n\n\nSGI request for dialogue with the priesthood was rejected by the Head Temple - assuming that lay believers will leave SGI organisation and register in temples. Members, however, submitted a petition asking for the resignation of the High Priest. Finally, the SGI was excommunicated from the Head Temple (28 November 1991), a date recognised by SGI as the day of spiritual independence of ordinary people.\n\n\n\"We must ensure that the common people are eternally free from domination by evil tyrants. The people are the base upon which all things rest, the most important factor. A power that does not rely on authorities, that is unswayed by them, is to be found in the power of humanity, of unity and of democracy. We must never allow this power to be diminished. This is the profound significance of the Buddhism of human revolution, which stimulates and nurtures this human power to the highest degree.\"\n\n\nSGI Newsletter 5821, 5826 (Dec. 2003)\n\n\n1992\n\n\nSeveral temples refused to follow the High Priest and disassociated themselves from the Head Temple (Association of Reformist Priests), giving their support to SGI. One of the basic issues between the Priesthood and the Association of Reformist Priests is the demand for the Head Temple's apology for supporting the war and for altering Nichiren's letters.\n\n\n2000\n\n\nThe Priesthood completes destruction of its Head Temple, the Shohondo building, which was donated by the Soka Gakkai.\n\n\n_________________________________________________\n\n\nBack to: Nichiren Shoshu & S G I\n\n\nHomepage"}
{"id": 255026, "ended": false, "length": 1024, "text": "When the head of the CIA's torture unit decided to destroy videotapes of his team's horrific work, he unwittingly set in motion a series of events that led to the release this week of the most massive, detailed documentation of unlawful behavior by high-ranking government officials and intentional infliction of pain on noncombatants by the United States government since the Civil War era. Here is the backstory.\n\nOne of the reasons repeatedly stated by President George W. Bush for the American invasion of Iraq in 2003 was the maintenance of \"torture rooms\" by Saddam Hussein. While making this very argument, Bush was secretly authorizing CIA agents to engage in similar unlawful behavior for similar purposes: intelligence and deterrence. Bush sounded credible when he claimed that his administration adhered to federal and international legal standards.\n\nHe knew he could make that claim because the torturers were sworn to secrecy, as were their congressional regulators. The CIA charter permits Congress to regulate the CIA in secret. Congress has established two secret congressional committees, one from the Senate and one from the House, to serve as monitors and regulators of CIA activities. The stated reason for the secrecy is to keep our enemies from knowing what the CIA is doing. The effect of the secrecy has been a muzzled Congress, lied to by law-breaking and rogue CIA officials.\n\nUntil now.\n\nWhen the Senate Intelligence Committee staff learned of the destroyed videotapes (a federal crime the Justice Department declined to prosecute) and reported that destruction to Sen. Dianne Feinstein (D-Calif.), the committee chair, she ordered an investigation to determine whether the CIA officials who had briefed her committee had told the truth. If they had been truthful, she reasoned, why destroy the tapes? In order to conduct that investigation, Feinstein ordered the CIA to make available to her committee's investigators whatever documents and digital data the investigators sought.\n\nDuring the course of the investigation, Senate investigators suspected their computers had been hacked. When they brought those suspicions to Feinstein, she ordered another investigation, this one aimed at identifying the hackers. That investigation revealed that the CIA itself was spying on its own Senate investigators. When she approached CIA Director John Brennan about this, he denied it. When she went to the floor of the Senate\u2014where her vow of secrecy may lawfully be disregarded\u2014to reveal that the CIA had spied on her and her fellow Senators and their investigators, the CIA denied it. When she released incontrovertible evidence of CIA domestic spying, Brennan admitted that his agents had spied on their regulators (another federal crime the feds declined to prosecute), but claimed it was needed because the regulators had exceeded their authority in examining CIA documents.\n\nAll this put the original investigation of why the tapes of the torture had been destroyed and whether the CIA had been truthful to the White House and its congressional regulators into high gear. When the investigators' final report\u2014all 6,000 pages of it, much in lurid detail\u2014was completed, it was sent to the White House, which decided to release it. The CIA begged for redactions of agents' names and other identifiers, and a long process of negotiation ensued between the White House, the State Department, the CIA, and the Senate. This week, Feinstein had had enough and decided to release the report with the then-agreed-upon redactions.\n\nThe report is damning in the extreme to the Bush administration and to the CIA leadership. It offers proof that the CIA engaged in physical and psychological torture, some of which was authorized\u2014unlawfully, yet authorized\u2014and most of which was not. The report also demonstrates that CIA officials repeatedly lied to the White House and to Senate regulators about what they were doing, and they lied about the effectiveness of their torture.\n\nIf the allegations in the report are true, we have war criminals, perjurers, computer hackers and thugs on the government payroll. We also have dupes. The most politically successful argument the torture lobby has made is that we are all safer because of these dirty deeds. This Senate report refutes that argument by demonstrating that no serious actionable intelligence came from the torture.\n\nAll torture is criminal under all circumstances\u2014under treaties to which the U.S. is a party, under the Constitution that governs the government wherever it goes, and under federal law. Torture degrades the victim and the perpetrator. It undermines the moral authority of a country whose government condones it. It destroys the rule of law. It exposes our own folks to the awful retaliatory beheadings we have all seen. It is slow, inefficient, morbid, and ineffective. It is a recruiting tool for those who have come to cause us harm. All human beings possess basic inalienable rights derived from the natural law and protected by the Constitution the CIA has sworn to uphold. Torture violates all of those rights.\n\nWhat should we make of this report on government torture? In a free society in which the government works for us, we have a right to know what it is doing in our names"}
{"id": 255027, "ended": true, "length": 694, "text": "Laser rangefinders are excellent tools that help you to determine longer distances that wouldn't be practical or possible to measure by hand. Since their inception, these gadgets have been improved and modified to become serious pieces of equipment. Their scope of use extends far beyond standard construction or labor contexts however.\n\nLaser rangefinders are also a great asset to use when mountaineering or hunting, along with other outdoor activities. www.bestrangefinderreviewsguide.com is a great resource for determining which rangefinder is best suited for your needs.\n\nWithout having access to a laser rangefinder when mountaineering, it is simply impossible to measure the distance up a mountain unless you hike it! But in order to gather the necessary information you need on a hike, a quality laser rangefinder can help you figure out the distance to your next location. This not only provides climbers with an understanding of distances, but it also helps to increase safety by providing accurate and reliable information from which climbers can use to make important decisions, especially on more dangerous and technical routes.\n\nAnother great feature of laser rangefinders are their compatibility. When you're out climbing mountains, the last thing you need is more stuff weighing you down. A majority of laser rangefinders are designed to fit inside your bag with no problem. Depending on your preference, rangefinders for mountaineering can also be handheld or come with a tripod for added stability.\n\nHunting is all about precision and accuracy. Make any small mistake and that opportunity you had can disappear in seconds. That is why hunters strive to remove all of the unpredictable or unknown variables that they can, ensuring the best chance of making the shot. That is why rangefinders are becoming more in more popular in the hunting world. Rangefinders can provide hunters with the exact distances between them and their targets.\n\nThis takes a lot of guesswork and estimating out of the equation which highly increases the chances of a successful shot. There are rangefinders that can be found designed for the sole purpose of hunting. Some models are designed for hand-held usage, while others include mounts or poles. Still, some other models mount directly onto your hunting weapon of choice, whether that be a bow, rifle and more.\n\nSome of the major manufacturers of laser rangefinders include Bushnell, Luepold, hunting giant Cabela, and even some camera manufacturers such as Nikon and Canon produce their own quality laser rangefinders. Depending on the laser rangefinder itself and the manufacturer, their specificity of use may differ. For those wanting to use a rangefinder for only hunting, it would be wise to purchase one from a company who specializes in this field. The same goes for those looking for laser rangefinders for the sole purpose of mountaineering. In effect, all laser rangefinders accomplish the same task, but some added features can specialize it to the user's particular needs.\n\nWhether you are climbing a mountain or heading out for a weekend of hunting, guessing distances won't help you succeed. Take away all of the doubts and guessing by utilizing a laser rangefinder. The sheer accuracy of these tools will make sure that all of the unknown variables are removed. If you're climbing a mountain, you no longer have to worry if your estimates are correct. For those of you hunting, you can remain confident that one shot is going to count."}
{"id": 255028, "ended": true, "length": 512, "text": "The Coalition For Economic Survival (CES) urges a NO vote on Measure S, on the March 7, 2017 Los Angeles City ballot\n\nCES believes Measure S threatens to delay or stop projects that would otherwise provide affordable housing, and housing for homeless people.\n\nMeasure S puts a two-year moratorium on development projects requiring certain zoning or height exemptions, and permanently prohibits developments requiring a general plan amendment. Thus, it could stop projects that would provide permanent supportive housing for people that are homeless \u2013 housing that voters approved with the passage of Measure HHH last November.\n\nClearly, there is a great need for government action to protect neighborhoods and much more action is needed to preserve our existing rent controlled and affordable housing stock. In fact, this lack of action at City Hall, no doubt, opened the door for Measure S to make it to the ballot.\n\nMeasure S does have some good provisions. The City should be updating community plans. Obviously, in response to Measure S, the City Council just voted to back an effort to update community plans more frequently.\n\nAdditionally, developers should not be allowed to select environmental impact report consultants for their projects.\n\nBut, it is our belief that Measure S is a sledgehammer approach that does not provide a solution. In fact, it may make matters worse.\n\nMeasure S is not the answer and should be voted down.\n\nMeasure S\n\nDoes Not Stop Ellis Act evictions\n\nDoes Not Stop condo conversions\n\nDoes Not Stop rent controlled housing being demolished. In fact it may led to the destruction of rent controlled buildings.\n\nDoes Not Create new affordable housing\n\nDoes Not Stop big developers from donating to elected officials\n\nMeasure S DOES Stop Affordable Housing from Being Built\n\nMeasure S would provide an incentive to developer to destroy more rent controlled buildings.\n\nA two year moratorium on development targeted in Measure S could steer developers towards other types of development such as more demolitions and conversions of rent controlled housing to condos resulting in further displacement of low and moderate income renters.\n\nThe Measure S moratorium, and its permanent prohibition on the City's ability to issue general plan amendments, will be stop the building of affordable housing. Although the backers of Measure S claim to exempt affordable housing, Measure S does not actually exempt all 100% affordable housing projects from its reach, and would effectively stop 90% of city-sponsored affordable housing projects.\n\nIt is for these reasons CES Urges You to Vote NO on Measure S!\n\nAdvertisements"}
{"id": 255029, "ended": true, "length": 402, "text": "If you haven't been paying attention: Republicans have been so gung-ho about stripping health care from millions of people and giving tax cuts to a few monstrously rich people that at the end of September they needlessly let the Children's Health Plan (CHIP) expire - just like too many kids and adults s will if the GOP can't figure out how to act like human beings, and govern accordingly. Currently, CHIP provides health care to almost nine million children nationwide; if Congress, which has historically summoned a reasonable facsimile of bi-partisan support for what most normal people would consider a basic human need, can't find the will to reauthorize it in the next few weeks, at least 16 states will run out of funding by January 1.\n\n\nMany good people, including Jimmy Kimmel and Alabama's newly-elected Doug Jones, have urged lawmakers to confront the grotesque negligence toward children that would be the demise of CHIP. But Rachel Pearson, a cheeky pediatrician in Texas who used to believe everyone deserved health care, says she's come to learn those in need are \"ungrateful, yowling, diapered maniacs who don't even use language right\" and are often \"literally carried from place to place in the arms of a real taxpayer.\" \"Most of my patients have never worked a day in their lives,\" she writes. \"Patients have punched me, bitten me, screamed at me, and even urinated on me...Sometimes, I have to bribe my patients with bright-colored objects, juice or graham crackers. (Do) my patients thank me? Do they contribute to the economy? No!...\" If CHIP isn't funded, she adds, perhaps letting more American kids die preventable deaths \"will send a strong message to kids across the country: Pull your thumbs out of your mouths, get potty-trained and GET A JOB!\" Hopefully, eventually, one that would remove the GOP from power."}
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/webtext$ 
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/webtext$ 
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/webtext$ head ./webtext.test.jsonl 
{"id": 255000, "ended": true, "length": 134, "text": "Is this restaurant family-friendly ? Yes No Unsure\n\nDoes this restaurant accept reservations ? Yes No Unsure\n\nAre the prices at this restaurant mid-range / moderate? Yes No Unsure\n\nIs this restaurant good for dinner? Yes No Unsure\n\nIs this restaurant good for lunch? Yes No Unsure\n\nIs this a Japanese restaurant? Yes No Unsure\n\nCould this location be considered a specialty food market? Yes No Unsure\n\nDoes this restaurant have waiters and waitresses ? Yes No Unsure\n\nIs this restaurant a hidden gem or off-the-beaten path? Yes No Unsure\n\nIs this primarily a bakery ? Yes No Unsure"}
{"id": 255001, "ended": true, "length": 713, "text": "Clinton talks about her time of 'reflection' during sick days\n\nHillary Clinton returned to the campaign trail Thursday afternoon, debuting some new intro music and telling the crowd that her sick days allowed her a chance to \"reconnect with what this whole campaign is about.\"\n\nThe former secretary of state, who took the stage to James Brown's \"I Feel Good,\" spent the beginning of the week at her home in Chappaqua, New York, after being diagnosed late last week with pneumonia. Her campaign initially did not disclose the illness and only did so after Clinton was forced to leave an event early on Sunday commemorating the 15th anniversary of the Sept. 11 terrorist attacks.\n\nStory Continued Below\n\n\"I tried to power through it but even I had to admit that maybe a few days of rest would do me good,\" she told the Greensboro, North Carolina, crowd of her pneumonia. \"And I'm not great at taking it easy, even under ordinary circumstances, but with just two months to go until Election Day, sitting at home was pretty much the last place I wanted to be.\"\n\n\"But it turns out having a few days to myself was actually a gift, I talked with some old friends. I spent time with our very sweet dogs. I did some thinking,\" she continued. \"The campaign trail doesn't really encourage reflection. And it's important to sit with your thoughts every now and then and that did help me reconnect with what this whole campaign is about.\"\n\nClinton compared her own ability to take a handful of sick days to that of many Americans who she said are forced to \"either go to work sick or they lose a paycheck.\" She said those Americans, and others \"living on a razor's edge\" with an aging parent who needs help or without the means to afford a college education, are the reason she is running for president.\n\nSpeaking in North Carolina, Clinton made special mention of the law there forcing transgender individuals to use the bathroom that corresponds with the gender on their birth certificate. The law, seen by many as discriminatory, has prompted the NBA, NCAA and Atlantic Coast Conference to move major sporting events out of the state, costs that the former secretary of state said, \"We can't afford.\"\n\n\"I'm running for the LGBT teenager here in North Carolina who sees your governor sign a bill legalizing discrimination and suddenly feels like a second-class citizen,\" she said. \"And if anyone wonders what is the cost of discrimination are, just ask the people and businesses of North Carolina, look at what's happening with the NCAA and the ACC. This is where bigotry leads and we can't afford it, not here, not anywhere else in America.\"\n\nClinton did not address her opponent, Donald Trump, by name but did spend a significant portion of her remarks laying out many of the contrasts she regularly draws with her opponent. She told the crowd that \"I am actually asking Americans to hold me accountable for my ideas and hold my opponent accountable for his.\"\n\n\"You know, I've been involved in politics. It is not an easy business. It can get rough, and I've built up some defenses. When it comes to public service, I am better at the service part than the public part,\" she said. \"People accuse me of all kinds of things. You probably have seen that. But nobody ever accuses me of quitting. And I will never give up. I'll never walk away. No matter how tough the going gets.\""}
{"id": 255002, "ended": true, "length": 173, "text": "House Majority Whip Steve Scalise has been discharged from the hospital six weeks after sustaining a life-threatening gunshot wound during an attack on a Republican congressional baseball practice in Virginia. He plans to return to Congress after completing \"a period of intensive inpatient rehabilitation.\"\n\nThe full statement:\n\nCongressman Steve Scalise has made excellent progress in his recovery from a life-threatening gunshot wound six weeks ago. Yesterday, he was discharged from MedStar Washington Hospital Center and is now beginning a period of intensive inpatient rehabilitation. He is in good spirits and is looking forward to his return to work once he completes rehabilitation. He and his family are grateful for the care he received from the trauma team as well as the other doctors, nurses, and staff of MedStar Washington Hospital Center. The family also appreciates the outpouring of prayers and support during this time."}
{"id": 255003, "ended": true, "length": 490, "text": "Insight Course: Lesson 14\n\nControl of the Mind\n\nThe truth will set you free, but first it will piss you off. ~ Gloria Steinem\n\nAre you ready for another wild trip down the rabbit hole? Now that we have explored our own deepest personal challenges, it is time to explore what is possibly the deepest challenge facing our planet.\n\nThe term \"mind control\" can bring up all kinds of thoughts and feelings. Yet as with almost any tool, mind control techniques can be used for the good of all of us or used to gain personal benefit at the expense of others.\n\nThough this lesson may be the most disturbing of all for some, it is also vitally important as far as understanding how some of the top secret, sophisticated operations which have a major impact on our world have been carried out. This topic also has some amazing healing applications. These applications and the deeper implications of all this information will be discussed at the end of the lesson.\n\nFirst, you are invited to explore some highly reliable information on how mind control has been used to forward hidden, disempowering agendas in our world. Please watch the revealing, 45-minute History Channel documentary Mind Control: America's Secret War at the link below:\n\nhttps://www.WantToKnow.info/mindcontrolvideo\n\nSome people would rather not know the many potentially disturbing facts about secret mind control programs used to manipulate people and politics around the world. Yet when we collectively choose not to know, those who are abusing these technologies are given free rein to explore further and to cause serious manipulations which lead to even more fear and polarization in our world.\n\nBy choosing to at least understand the basics of what is going on, we can come together to stop the destructive behavior and invite others to join us in working together for what's best for all on our planet. For the best concise summary of secret mind control programs, please read the two-page essay below:\n\nhttps://www.WantToKnow.info/mindcontrol\n\nSacred Cows\n\nDon't ignore the bad stuff, but make a point of celebrating the beautiful stuff with all the exuberant devotion you can muster.\n\n~ Rob Brezsny in his fun, profound book Pronoia is the Antidote for Paranoia\n\n\nTo Complete Insight Course Lesson 14: Click Here"}
{"id": 255004, "ended": true, "length": 220, "text": "BY JENNIE MCNULTY\n\nLesbian.com\n\nYou know Weinstien and Spacey, and Louis and Tambor,\n\nLauer and Charlie, and Franken and Roy Moore\n\nBut do you recall,\n\nThe most harmful predator of all?\n\nDonald the groping gasbag\n\nHad some really tiny hands,\n\nFor those that had to feel them,\n\nJail should be the place he'd land.\n\nAll of the media perverts\n\nHad to quit and lost careers;\n\nMeanwhile, the sleaze ball Donald\n\nScrews us like a racketeer.\n\nThen one foggy Christmas eve,\n\nMueller came to say:\n\n\"Donald all your lies and fraud\n\nMake your case severely flawed.\"\n\nThen all his buddies made deals,\n\nThey began to cop a plea,\n\nDonald the gas bag groper\n\nEnjoy the penitentiary.\n\nJennie McNulty was named one of Curve magazine's Top 10 lesbian comedians."}
{"id": 255005, "ended": true, "length": 198, "text": "The Buddha's Teaching As It Is\n\nIn the fall of 1979, while living at the Washington Buddhist Vihara, Ven. Bhikkhu Bodhi gave a series of lectures on the fundamental teachings of Early Buddhism. Bhante Gunaratana, at the time the President of the Buddhist Vihara Society, suggested he record the lectures so that the Vihara could distribute them as a set of cassette tapes.\n\nIn the summer of 1981, Ven. Bodhi recorded his ten lectures in the basement of the Washington Buddhist Vihara, using an ordinary, nonprofessional recorder. An enthusiastic lay supporter had the master copies reproduced in large quantities for expanded distribution. They have continued to be distributed on tape and as CDs for over twenty-five years, and are considered \"public domain\" for anyone to copy and distribute freely. The one condition is that they must not be sold.\n\nWe recommend that the first time you listen to them, you listen to them in their proper sequence:"}
{"id": 255006, "ended": true, "length": 365, "text": "As part of a broad initiative to combat sexual harassment and assault, French President Emmanuelle Macron promised to make \"gender-based insults\" punishable by law.\n\nAs France24 reports, Macron outlined his plans in a speech marking the International Day for Elimination of Violence Against Women. \"The streets should not become hell for the women of France,\" he said. Macron noted that the Ministry of the Interior has launched consultations that will lead to new measures \"in a few weeks' time.\"\n\n\"We will \u2026 be creating an offense which will give the police the right to issue fines if there is a verbal attack on a woman,\" he said.\n\nThe future draft law may also include a number of measures that will make it easier for sexual assault victims to report to police\u2014measures like extending the statute of limitations for the rape of minors from 20 to 30 years, and allowing rape victims to make their initial complaints on online.\n\nIn an effort to help women get home safely, the law may implement an \"on demand\" service for public transit, which would let women ask buses to stop anywhere along their route at night.\n\n\"Let's seal a pact of equality between men and women,\" Macron said, adding that when it comes to sexual harassment and assault, \"it is essential that shame changes camp.\"\n\nIn France, half of all women, according to France24, say they are victims of sexual assault. Despite recent progress, it's still a difficult topic for women to discuss. Below watch a video in which several women talk about their experiences with sexual harassment and assault, including a shocking experience a woman named Mara had on a city bus.\n\nRead the full story at France24.\n\nRelated\n\nGender equality minister in France proposes instant fines for street sexual harassers"}
{"id": 255007, "ended": true, "length": 184, "text": "The Atlanta Falcons have started the 2015 season 4-0 under new head coach Dan Quinn. Quarterback Matt Ryan has the most passing yards in the NFC South while receiver Julio Jones is having quite a start, too.\n\nAnd according to ESPN's \"First Take,\" the Football Power Index has the Falcons as the team with the best chance to finish the season 16-0.\n\nHowever, ESPN is asking: Where are all the Falcons fans?\n\nFan correspondent, Reese Waters, walked the streets of Atlanta trying to find Falcons fans, which seemed to be easier said than done.\n\n\"I support the Braves and the Hawks ... I'm a Saints fan,\" one man said.\n\nWhen asked what's the happiest you've ever been as a Falcons fan, one man said: \"When we beat them Saints, when we beat them Saints, baby.\"\n\nSee the full video below:"}
{"id": 255008, "ended": true, "length": 253, "text": "Front Page Torrents Favorites My Home My Galleries Toplists Bounties News Forums Wiki HentaiVerse\n\n[Spiritus Tarou] Issho ni Ite yo | Together With You (COMIC JSCK Vol. 5 2016-07) [English] =CW + TLL= [\u30b9\u30d4\u30ea\u30bf\u30b9\u592a\u90ce] \u4e00\u7dd2\u306b\u3044\u3066\u3088 (\u30b3\u30df\u30c3\u30af\u30b8\u30a7\u30b7\u30ab Vol.5 2016\u5e747\u6708\u53f7) [\u82f1\u8a33]\n\nYou have to register before you can add comments.\n\nPosted on 31 May 2018, 08:58 UTC by: kiwino\n\nBase +5, mrwayne +14 , Ice_Cream +11 , The Lost Light +8 , THDragon +14 , MomentoMori009 +2 , RedResistance +5 , Anony12788 +9 , MechWarriorNY +7 , SW_CGF +6 , Drake68655 -6 , nodire +6 , firedragon89 +11 , and 1 more...\n\n[Front Page]\n\nPlease read the Terms of Service before participating with or uploading any content to this site."}
{"id": 255009, "ended": true, "length": 55, "text": "They have changed the phone menu to try to deflect us to email, but you can still get a live person by navigating to file a complaint.\n\nShe didn't sound happy that I figured it out, but they aren't concerned about making us happy, are they?"}
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/webtext$ 

pyaesk@62917715f76a:~/exp/kan-gpt/datasets/webtext$ wc *.jsonl
     5000   2137089  13478245 webtext.test.jsonl
   250000 107853539 679129270 webtext.train.jsonl
     5000   2161233  13622302 webtext.valid.jsonl
   260000 112151861 706229817 total
pyaesk@62917715f76a:~/exp/kan-gpt/datasets/webtext$ 
```


## Training Kan-GPT with KAN

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.train --architecture KAN --model_type gpt-mini --batch_size 3 --max_iters 400
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
test_dataset:  63913
train_dataset:  270018
number of parameters: 31.08M
running on device cpu
wandb: Currently logged in as: yktnlp (yktnlp-nectec). Use `wandb login --relogin` to force relogin
wandb: Tracking run with wandb version 0.17.9
wandb: Run data is saved locally in /home/pyaesk/exp/kan-gpt/wandb/run-20240908_092145-y4njzvu9
wandb: Run `wandb offline` to turn off syncing.
wandb: Syncing run sleek-lion-2
wandb: ⭐️ View project at https://wandb.ai/yktnlp-nectec/KAN-GPT
wandb: 🚀 View run at https://wandb.ai/yktnlp-nectec/KAN-GPT/runs/y4njzvu9
iter_dt 0.00ms; iter 0: train loss 10.83818
====================
EVAL
====================
train loss: 9.75
test loss: 9.63
train_loss:  tensor(9.7523)
train_perplexity:  tensor(862.4644)
train_f1:  tensor(0.0049)
train_precision:  tensor(0.0049)
train_recall:  tensor(0.0049)
train_cross_entropy:  tensor(9.7523)
test_loss:  tensor(9.6294)
test_perplexity:  tensor(792.0511)
test_f1:  tensor(0.0010)
test_precision:  tensor(0.0010)
test_recall:  tensor(0.0010)
test_cross_entropy:  tensor(9.6294)
====================
iter_dt 9588.16ms; iter 100: train loss 6.75244
====================
EVAL
====================
train loss: 6.58
test loss: 6.72
train_loss:  tensor(6.5773)
train_perplexity:  tensor(95.4948)
train_f1:  tensor(0.1179)
train_precision:  tensor(0.1179)
train_recall:  tensor(0.1179)
train_cross_entropy:  tensor(6.5773)
test_loss:  tensor(6.7162)
test_perplexity:  tensor(105.1434)
test_f1:  tensor(0.1221)
test_precision:  tensor(0.1221)
test_recall:  tensor(0.1221)
test_cross_entropy:  tensor(6.7162)
====================
^[[B
iter_dt 9587.04ms; iter 200: train loss 6.36621
====================
EVAL
====================
train loss: 6.52
test loss: 6.63
train_loss:  tensor(6.5191)
train_perplexity:  tensor(91.6647)
train_f1:  tensor(0.1179)
train_precision:  tensor(0.1179)
train_recall:  tensor(0.1179)
train_cross_entropy:  tensor(6.5183)
test_loss:  tensor(6.6267)
test_perplexity:  tensor(98.5435)
test_f1:  tensor(0.1221)
test_precision:  tensor(0.1221)
test_recall:  tensor(0.1221)
test_cross_entropy:  tensor(6.6227)
====================
iter_dt 9240.48ms; iter 300: train loss 6.40867
====================
EVAL
====================
train loss: 6.38
test loss: 6.57
train_loss:  tensor(6.3809)
train_perplexity:  tensor(83.2341)
train_f1:  tensor(0.1179)
train_precision:  tensor(0.1179)
train_recall:  tensor(0.1179)
train_cross_entropy:  tensor(6.3791)
test_loss:  tensor(6.5726)
test_perplexity:  tensor(94.5399)
test_f1:  tensor(0.1221)
test_precision:  tensor(0.1221)
test_recall:  tensor(0.1221)
test_cross_entropy:  tensor(6.5628)
====================
Model saved: weights/model_20240908-103208.pth
wandb:                                                                                
wandb: 
wandb: Run history:
wandb:  test_cross_entropy █▁▁▁
wandb:             test_f1 ▁███
wandb:           test_loss █▁▁▁
wandb:     test_perplexity █▁▁▁
wandb:      test_precision ▁███
wandb:         test_recall ▁███
wandb: train_cross_entropy █▁▁▁
wandb:            train_f1 ▁███
wandb:          train_loss █▁▁▁
wandb:    train_perplexity █▁▁▁
wandb:     train_precision ▁███
wandb:        train_recall ▁███
wandb: 
wandb: Run summary:
wandb:  test_cross_entropy 6.56285
wandb:             test_f1 0.12214
wandb:           test_loss 6.57261
wandb:     test_perplexity 94.53988
wandb:      test_precision 0.12214
wandb:         test_recall 0.12214
wandb: train_cross_entropy 6.37909
wandb:            train_f1 0.1179
wandb:          train_loss 6.38088
wandb:    train_perplexity 83.2341
wandb:     train_precision 0.1179
wandb:        train_recall 0.1179
wandb: 
wandb: 🚀 View run sleek-lion-2 at: https://wandb.ai/yktnlp-nectec/KAN-GPT/runs/y4njzvu9
wandb: ⭐️ View project at: https://wandb.ai/yktnlp-nectec/KAN-GPT
wandb: Synced 5 W&B file(s), 0 media file(s), 1 artifact file(s) and 0 other file(s)
wandb: Find logs at: ./wandb/run-20240908_092145-y4njzvu9/logs
wandb: WARNING The new W&B backend becomes opt-out in version 0.18.0; try it out with `wandb.require("core")`! See https://wandb.me/wandb-core for more information.

real    71m36.432s
user    926m17.027s
sys     104m11.794s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

## Checked Output Model

မော်ဒယ် အသစ်တစ်ခု တိုးလာတာ အောက်ပါအတိုင်း တွေ့ရတယ်။ 

```
pyaesk@62917715f76a:~/exp/kan-gpt/weights$ ls
model_20240908-081150.pth  model_20240908-103208.pth
```

## Testing Kan-Gpt

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture KAN --model_path ./weights/model_20240908-103208.pth --model_type gpt-mini --prompt "Bangalore is often described as the "
number of parameters: 31.08M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Bangalore is often described as the  objectivesaur WarrantyilitationoviesiangADA Lak Lak Lak secretary Lak Lakilitation Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lak Lakishop Lak Lak Lak Lakenameenameenameenameenameenameenameenameenameenameenameenameename Hiroshimaenameenameenameenameename Hiroshima Hiroshimailitationenameenameenameenameenameenameename HiroshimaenameenameRowenameename Hiroshima secretaryenameename Hiroshimaenameenameenameenameenameenameenameenameename secretary secretary Imagenameenameenameename secretary secretary Imag secretary secretary

real    0m15.892s
user    3m3.249s
sys     0m17.309s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

နောက်ထပ် phrase တစ်ခုပေးပြီး ထပ်စမ်းကြည့်ခဲ့...  

```
pyaesk@62917715f76a:~/exp/kan-gpt$ time python3 -m kan_gpt.prompt --architecture KAN --model_path ./weights/model_20240908-103208.pth --model_type gpt-mini --prompt "Is doom'd a "
number of parameters: 31.08M
/home/pyaesk/.local/lib/python3.10/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Is doom'd a Log ClareullyLog miss miss KumSuccessSuccessSuccessSuccessSuccessLogSuccessLogSuccessLogSuccess GainedLog SVGLog SVGLog SVGLog SVGNoticeLog SVGNoticeLogNoticeLogLog drivers driversLogLogLogLogLogLog drivers driversLogLog drivers driversLogLogLogLogLogLogLogLogLogLog drivers driversLog driversLogLogLogLogLogLog ClareLog drivers drivers drivers drivers driversNoticeLogNoticeLogLogLog driversLogLogLogLogLogLogLogLogLogLogLogLogLogLogNoticeLogLog

real    0m15.065s
user    2m54.177s
sys     0m18.121s
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

## Call --help for Training

```
pyaesk@62917715f76a:~/exp/kan-gpt$ python kan-gpt.train --help
bash: python: command not found
pyaesk@62917715f76a:~/exp/kan-gpt$ python3 -m kan_gpt.train --help
usage: KAN-GPT Trainer [-h] [--model_type MODEL_TYPE] [--dummy_dataset] [--learning_rate LEARNING_RATE] [--max_iters MAX_ITERS]
                       [--num_workers NUM_WORKERS] [--batch_size BATCH_SIZE] [--dataset {webtext,tinyshakespeare}]
                       [--architecture {MLP,KAN}] [--device {auto,cpu,cuda}]

options:
  -h, --help            show this help message and exit
  --model_type MODEL_TYPE
  --dummy_dataset
  --learning_rate LEARNING_RATE
  --max_iters MAX_ITERS
  --num_workers NUM_WORKERS
  --batch_size BATCH_SIZE
  --dataset {webtext,tinyshakespeare}
  --architecture {MLP,KAN}
  --device {auto,cpu,cuda}
pyaesk@62917715f76a:~/exp/kan-gpt$ 
```

## Check Training Code

running parameter အပိုင်းတွေကို ဝင်ကြည့်ခဲ့...  

```python
if __name__ == "__main__":
    import argparse

    parser = argparse.ArgumentParser("KAN-GPT Trainer")
    parser.add_argument("--model_type", default="gpt-mini")
    parser.add_argument("--dummy_dataset", action="store_true")
    parser.add_argument("--learning_rate", default=5e-3)
    parser.add_argument("--max_iters", default=2000)
    parser.add_argument("--num_workers", default=0)
    parser.add_argument("--batch_size", default=64)

    parser.add_argument(
        "--dataset",
        choices=["webtext", "tinyshakespeare"],
        default="tinyshakespeare",
    )
    parser.add_argument(
        "--architecture", choices=["MLP", "KAN"], default="KAN"
    )
    parser.add_argument(
        "--device", choices=["auto", "cpu", "cuda"], default="auto"
    )
	
```

```python
    model_type = args.model_type

    if args.dataset == "webtext":
        Dataset = WebTextDataset
    elif args.dataset == "tinyshakespeare":
        Dataset = TinyShakespeareDataset

    # print an example instance of the dataset
    if args.dummy_dataset:
        train_dataset = Dataset("test", "gpt2")
    else:
        train_dataset = Dataset("train", "gpt2")

    test_dataset = Dataset("test", "gpt2")

    print("test_dataset: ", len(test_dataset))
    print("train_dataset: ", len(train_dataset))

    if args.architecture == "KAN":
        GPT = KAN_GPT
    else:
        GPT = MLP_GPT

```


## Test Training of Kan-GPT, KAN Archi With GPU

အထက်မှာ လုပ်ခဲ့တဲ့ training နှစ်ခုစလုံးက CPU ပေါ်မှာ လုပ်ခဲ့တာ။ ဒီတစ်ခါ GPU သုံးပြီး training လုပ်ကြည့်ပြီး အချိန်ဘယ်လောက်ကွာမလဲ ကြည့်မယ်။  

ပြီးတော့ training dataset က ဘာမှာ assign မလုပ်ပဲ train ရင် အောက်ပါအတိုင်း တွေ့ရတယ်။  

test_dataset:  63913  
train_dataset:  270018  

GPU က AIT server မှာ မသိဘူးဖြစ်နေလို့ LST server ဘက်မှာ kan-gpt ကို install လုပ်ပြီး test run စမ်းကြည့်ခဲ့ ....  

```
(yanmtt) ye@lst-hpc3090:~/exp/kan-gpt$ time  /home/ye/miniforge3/envs/yanmtt/bin/python -m kan_gpt.train --architecture MLP --batch_size 1 --dummy_dataset --device cuda --max_iters 200
tokenizer_config.json: 100%|███████████████████████████| 26.0/26.0 [00:00<00:00, 2.07kB/s]
vocab.json: 100%|████████████████████████████████████| 1.04M/1.04M [00:00<00:00, 1.10MB/s]
merges.txt: 100%|███████████████████████████████████████| 456k/456k [00:00<00:00, 637kB/s]
tokenizer.json: 100%|████████████████████████████████| 1.36M/1.36M [00:01<00:00, 1.16MB/s]
config.json: 100%|████████████████████████████████████████| 665/665 [00:00<00:00, 407kB/s]
/home/ye/miniforge3/envs/yanmtt/lib/python3.9/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Tokenizing: 100%|██████████████████████████████████| 8000/8000 [00:00<00:00, 22657.20it/s]
test_dataset:  63913
train_dataset:  63913
number of parameters: 12.52M
running on device cuda
wandb: (1) Create a W&B account
wandb: (2) Use an existing W&B account
wandb: (3) Don't visualize my results
wandb: Enter your choice: 3
wandb: You chose "Don't visualize my results"
wandb: Tracking run with wandb version 0.17.9
wandb: W&B syncing is set to `offline` in this directory.
wandb: Run `wandb online` or set WANDB_MODE=online to enable cloud syncing.
iter_dt 0.00ms; iter 0: train loss 10.85172
====================
EVAL
====================
train loss: 10.59
test loss: 10.59
train_loss:  tensor(10.5905)
train_perplexity:  tensor(1541.8542)
train_f1:  tensor(0.1219)
train_precision:  tensor(0.1219)
train_recall:  tensor(0.1219)
train_cross_entropy:  tensor(10.5904)
test_loss:  tensor(10.5905)
test_perplexity:  tensor(1541.8542)
test_f1:  tensor(0.1219)
test_precision:  tensor(0.1219)
test_recall:  tensor(0.1219)
test_cross_entropy:  tensor(10.5904)
====================
iter_dt 399.15ms; iter 100: train loss 5.93943
====================
EVAL
====================
train loss: 5.92
test loss: 5.92
train_loss:  tensor(5.9160)
train_perplexity:  tensor(60.3784)
train_f1:  tensor(0.1219)
train_precision:  tensor(0.1219)
train_recall:  tensor(0.1219)
train_cross_entropy:  tensor(5.9160)
test_loss:  tensor(5.9160)
test_perplexity:  tensor(60.3784)
test_f1:  tensor(0.1219)
test_precision:  tensor(0.1219)
test_recall:  tensor(0.1219)
test_cross_entropy:  tensor(5.9160)
====================
Model saved: weights/model_20240908-204157.pth
wandb:
wandb:
wandb: Run history:
wandb:  test_cross_entropy █▁
wandb:             test_f1 ▁▁
wandb:           test_loss █▁
wandb:     test_perplexity █▁
wandb:      test_precision ▁▁
wandb:         test_recall ▁▁
wandb: train_cross_entropy █▁
wandb:            train_f1 ▁▁
wandb:          train_loss █▁
wandb:    train_perplexity █▁
wandb:     train_precision ▁▁
wandb:        train_recall ▁▁
wandb:
wandb: Run summary:
wandb:  test_cross_entropy 5.91595
wandb:             test_f1 0.12188
wandb:           test_loss 5.91595
wandb:     test_perplexity 60.37837
wandb:      test_precision 0.12188
wandb:         test_recall 0.12188
wandb: train_cross_entropy 5.91595
wandb:            train_f1 0.12188
wandb:          train_loss 5.91595
wandb:    train_perplexity 60.37837
wandb:     train_precision 0.12188
wandb:        train_recall 0.12188
wandb:
wandb: You can sync this run to the cloud by running:
wandb: wandb sync /home/ye/exp/kan-gpt/wandb/offline-run-20240908_204022-8542v9ab
wandb: Find logs at: ./wandb/offline-run-20240908_204022-8542v9ab/logs
wandb: WARNING The new W&B backend becomes opt-out in version 0.18.0; try it out with `wandb.require("core")`! See https://wandb.me/wandb-core for more information.

real    2m36.009s
user    1m37.966s
sys     0m10.278s
(yanmtt) ye@lst-hpc3090:~/exp/kan-gpt$

```

test-run ပြီးတဲ့အခါမှာ...  

```
time python3 -m kan_gpt.train --architecture KAN --model_type gpt-mini --batch_size 3 --max_iters 400 --device cuda
```

အထက်မှာ run ခဲ့တဲ့ setting အတိုင်းပဲကို --device cuda နေရာပဲ ပြောင်းပေးပြီး ထပ် run ကြည့်ခဲ့... running log က အောက်ပါအတိုင်း ...  

```
(yanmtt) ye@lst-hpc3090:~/exp/kan-gpt$ time  /home/ye/miniforge3/envs/yanmtt/bin/python -m kan_gpt.train --architecture MLP --batch_size 1 --dummy_dataset --device cuda --max_iters 200
tokenizer_config.json: 100%|███████████████████████████| 26.0/26.0 [00:00<00:00, 2.07kB/s]
vocab.json: 100%|████████████████████████████████████| 1.04M/1.04M [00:00<00:00, 1.10MB/s]
merges.txt: 100%|███████████████████████████████████████| 456k/456k [00:00<00:00, 637kB/s]
tokenizer.json: 100%|████████████████████████████████| 1.36M/1.36M [00:01<00:00, 1.16MB/s]
config.json: 100%|████████████████████████████████████████| 665/665 [00:00<00:00, 407kB/s]
/home/ye/miniforge3/envs/yanmtt/lib/python3.9/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Tokenizing: 100%|██████████████████████████████████| 8000/8000 [00:00<00:00, 22657.20it/s]
test_dataset:  63913
train_dataset:  63913
number of parameters: 12.52M
running on device cuda
wandb: (1) Create a W&B account
wandb: (2) Use an existing W&B account
wandb: (3) Don't visualize my results
wandb: Enter your choice: 3
wandb: You chose "Don't visualize my results"
wandb: Tracking run with wandb version 0.17.9
wandb: W&B syncing is set to `offline` in this directory.
wandb: Run `wandb online` or set WANDB_MODE=online to enable cloud syncing.
iter_dt 0.00ms; iter 0: train loss 10.85172
====================
EVAL
====================
train loss: 10.59
test loss: 10.59
train_loss:  tensor(10.5905)
train_perplexity:  tensor(1541.8542)
train_f1:  tensor(0.1219)
train_precision:  tensor(0.1219)
train_recall:  tensor(0.1219)
train_cross_entropy:  tensor(10.5904)
test_loss:  tensor(10.5905)
test_perplexity:  tensor(1541.8542)
test_f1:  tensor(0.1219)
test_precision:  tensor(0.1219)
test_recall:  tensor(0.1219)
test_cross_entropy:  tensor(10.5904)
====================
iter_dt 399.15ms; iter 100: train loss 5.93943
====================
EVAL
====================
train loss: 5.92
test loss: 5.92
train_loss:  tensor(5.9160)
train_perplexity:  tensor(60.3784)
train_f1:  tensor(0.1219)
train_precision:  tensor(0.1219)
train_recall:  tensor(0.1219)
train_cross_entropy:  tensor(5.9160)
test_loss:  tensor(5.9160)
test_perplexity:  tensor(60.3784)
test_f1:  tensor(0.1219)
test_precision:  tensor(0.1219)
test_recall:  tensor(0.1219)
test_cross_entropy:  tensor(5.9160)
====================
Model saved: weights/model_20240908-204157.pth
wandb:
wandb:
wandb: Run history:
wandb:  test_cross_entropy █▁
wandb:             test_f1 ▁▁
wandb:           test_loss █▁
wandb:     test_perplexity █▁
wandb:      test_precision ▁▁
wandb:         test_recall ▁▁
wandb: train_cross_entropy █▁
wandb:            train_f1 ▁▁
wandb:          train_loss █▁
wandb:    train_perplexity █▁
wandb:     train_precision ▁▁
wandb:        train_recall ▁▁
wandb:
wandb: Run summary:
wandb:  test_cross_entropy 5.91595
wandb:             test_f1 0.12188
wandb:           test_loss 5.91595
wandb:     test_perplexity 60.37837
wandb:      test_precision 0.12188
wandb:         test_recall 0.12188
wandb: train_cross_entropy 5.91595
wandb:            train_f1 0.12188
wandb:          train_loss 5.91595
wandb:    train_perplexity 60.37837
wandb:     train_precision 0.12188
wandb:        train_recall 0.12188
wandb:
wandb: You can sync this run to the cloud by running:
wandb: wandb sync /home/ye/exp/kan-gpt/wandb/offline-run-20240908_204022-8542v9ab
wandb: Find logs at: ./wandb/offline-run-20240908_204022-8542v9ab/logs
wandb: WARNING The new W&B backend becomes opt-out in version 0.18.0; try it out with `wandb.require("core")`! See https://wandb.me/wandb-core for more information.

real    2m36.009s
user    1m37.966s
sys     0m10.278s
(yanmtt) ye@lst-hpc3090:~/exp/kan-gpt$
(yanmtt) ye@lst-hpc3090:~/exp/kan-gpt$
(yanmtt) ye@lst-hpc3090:~/exp/kan-gpt$ time  /home/ye/miniforge3/envs/yanmtt/bin/python -m kan_gpt.train --architecture KAN --model_type gpt-mini --batch_size 3 --max_iters 400 --device cuda
/home/ye/miniforge3/envs/yanmtt/lib/python3.9/site-packages/transformers/tokenization_utils_base.py:1601: FutureWarning: `clean_up_tokenization_spaces` was not set. It will be set to `True` by default. This behavior will be depracted in transformers v4.45, and will be then set to `False` by default. For more details check this issue: https://github.com/huggingface/transformers/issues/31884
  warnings.warn(
Tokenizing: 100%|████████████████████████████████| 32000/32000 [00:01<00:00, 24196.84it/s]
test_dataset:  63913
train_dataset:  270018
number of parameters: 31.08M
running on device cuda
wandb: (1) Create a W&B account
wandb: (2) Use an existing W&B account
wandb: (3) Don't visualize my results
wandb: Enter your choice: 3
wandb: You chose "Don't visualize my results"
wandb: Tracking run with wandb version 0.17.9
wandb: W&B syncing is set to `offline` in this directory.
wandb: Run `wandb online` or set WANDB_MODE=online to enable cloud syncing.
iter_dt 0.00ms; iter 0: train loss 10.82080
====================
EVAL
====================
train loss: 9.66
test loss: 9.68
train_loss:  tensor(9.6616)
train_perplexity:  tensor(809.9176)
train_f1:  tensor(0.0127)
train_precision:  tensor(0.0127)
train_recall:  tensor(0.0127)
train_cross_entropy:  tensor(9.6616)
test_loss:  tensor(9.6820)
test_perplexity:  tensor(821.4366)
test_f1:  tensor(0.0098)
test_precision:  tensor(0.0098)
test_recall:  tensor(0.0098)
test_cross_entropy:  tensor(9.6820)
====================
iter_dt 6328.84ms; iter 100: train loss 6.42526
====================
EVAL
====================
train loss: 6.46
test loss: 6.77
train_loss:  tensor(6.4637)
train_perplexity:  tensor(88.2628)
train_f1:  tensor(0.1179)
train_precision:  tensor(0.1179)
train_recall:  tensor(0.1179)
train_cross_entropy:  tensor(6.4637)
test_loss:  tensor(6.7674)
test_perplexity:  tensor(108.9442)
test_f1:  tensor(0.1221)
test_precision:  tensor(0.1221)
test_recall:  tensor(0.1221)
test_cross_entropy:  tensor(6.7674)
====================
iter_dt 6318.93ms; iter 200: train loss 6.48428
====================
EVAL
====================
train loss: 6.54
test loss: 6.54
train_loss:  tensor(6.5401)
train_perplexity:  tensor(93.0158)
train_f1:  tensor(0.1179)
train_precision:  tensor(0.1179)
train_recall:  tensor(0.1179)
train_cross_entropy:  tensor(6.5394)
test_loss:  tensor(6.5423)
test_perplexity:  tensor(92.9093)
test_f1:  tensor(0.1221)
test_precision:  tensor(0.1221)
test_recall:  tensor(0.1221)
test_cross_entropy:  tensor(6.5377)
====================
iter_dt 6316.38ms; iter 300: train loss 6.45735
====================
EVAL
====================
train loss: 6.61
test loss: 6.61
train_loss:  tensor(6.6053)
train_perplexity:  tensor(97.2359)
train_f1:  tensor(0.1179)
train_precision:  tensor(0.1179)
train_recall:  tensor(0.1179)
train_cross_entropy:  tensor(6.6034)
test_loss:  tensor(6.6066)
test_perplexity:  tensor(96.7679)
test_f1:  tensor(0.1221)
test_precision:  tensor(0.1221)
test_recall:  tensor(0.1221)
test_cross_entropy:  tensor(6.5965)
====================
Model saved: weights/model_20240908-213227.pth
wandb:
wandb:
wandb: Run history:
wandb:  test_cross_entropy █▂▁▁
wandb:             test_f1 ▁███
wandb:           test_loss █▂▁▁
wandb:     test_perplexity █▁▁▁
wandb:      test_precision ▁███
wandb:         test_recall ▁███
wandb: train_cross_entropy █▁▁▁
wandb:            train_f1 ▁███
wandb:          train_loss █▁▁▁
wandb:    train_perplexity █▁▁▁
wandb:     train_precision ▁███
wandb:        train_recall ▁███
wandb:
wandb: Run summary:
wandb:  test_cross_entropy 6.59645
wandb:             test_f1 0.12214
wandb:           test_loss 6.60661
wandb:     test_perplexity 96.7679
wandb:      test_precision 0.12214
wandb:         test_recall 0.12214
wandb: train_cross_entropy 6.60341
wandb:            train_f1 0.1179
wandb:          train_loss 6.60526
wandb:    train_perplexity 97.23593
wandb:     train_precision 0.1179
wandb:        train_recall 0.1179
wandb:
wandb: You can sync this run to the cloud by running:
wandb: wandb sync /home/ye/exp/kan-gpt/wandb/offline-run-20240908_204752-tqb3c29w
wandb: Find logs at: ./wandb/offline-run-20240908_204752-tqb3c29w/logs
wandb: WARNING The new W&B backend becomes opt-out in version 0.18.0; try it out with `wandb.require("core")`! See https://wandb.me/wandb-core for more information.

real    47m45.411s
user    28m55.130s
sys     16m23.502s
(yanmtt) ye@lst-hpc3090:~/exp/kan-gpt$
```

GPU နဲ့ Lab server မှာ run လို့ရတယ်ဆိုတာကို confirm လုပ်ပြီးသွားပြီ။  
