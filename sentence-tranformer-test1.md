# Testing Sentence Tansformer

## Installation

```
pip install -U sentence-transformers
...
...
...
huggingface-hub>=0.4.0->sentence-transformers) (3.0.12)
Requirement already satisfied: packaging>=20.9 in ./.local/lib/python3.7/site-packages (from huggingface-hub>=0.4.0->sentence-transformers) (21.3)
Requirement already satisfied: tokenizers!=0.11.3,<0.14,>=0.11.1 in ./.local/lib/python3.7/site-packages (from transformers<5.0.0,>=4.6.0->sentence-transformers) (0.13.1)
Requirement already satisfied: regex!=2019.12.17 in ./.local/lib/python3.7/site-packages (from transformers<5.0.0,>=4.6.0->sentence-transformers) (2022.9.13)
Requirement already satisfied: six in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from nltk->sentence-transformers) (1.14.0)
Requirement already satisfied: joblib>=0.11 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from scikit-learn->sentence-transformers) (0.14.1)
Requirement already satisfied: pillow!=8.3.*,>=5.3.0 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from torchvision->sentence-transformers) (7.0.0)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from packaging>=20.9->huggingface-hub>=0.4.0->sentence-transformers) (2.4.6)
Requirement already satisfied: zipp>=0.5 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from importlib-metadata->huggingface-hub>=0.4.0->sentence-transformers) (2.2.0)
Requirement already satisfied: chardet<5,>=3.0.2 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers) (3.0.4)
Requirement already satisfied: idna<3,>=2.5 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers) (2.8)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers) (1.25.8)
Requirement already satisfied: certifi>=2017.4.17 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers) (2019.11.28)
WARNING: You are using pip version 21.3.1; however, version 22.3 is available.
You should consider upgrading via the '/opt/anaconda/anaconda3/bin/python -m pip install --upgrade pip' command.
(sentence-transformer) yekyaw.thu@gpu:~$ 
```

Updating pip ...  

```
(sentence-transformer) yekyaw.thu@gpu:~$ pip install --upgrade pip
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: pip in /opt/anaconda/anaconda3/lib/python3.7/site-packages (21.3.1)
Collecting pip
  Downloading pip-22.3-py3-none-any.whl (2.1 MB)
     |████████████████████████████████| 2.1 MB 528 kB/s            
Installing collected packages: pip
  WARNING: The scripts pip, pip3, pip3.10 and pip3.7 are installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed pip-22.3
WARNING: You are using pip version 21.3.1; however, version 22.3 is available.
You should consider upgrading via the '/opt/anaconda/anaconda3/bin/python -m pip install --upgrade pip' command.
(sentence-transformer) yekyaw.thu@gpu:~$
```

## Test Run

When I got test run, I got following error:  

```
(sentence-transformer) yekyaw.thu@gpu:~/exp/kh-polar/sentence-transformer$ time python tst.py
...
...
...
y", line 3, in <module>
    from .ParallelSentencesDataset import ParallelSentencesDataset
  File "/home/yekyaw.thu/.local/lib/python3.7/site-packages/sentence_transformers/datasets/ParallelSentencesDataset.py", line 4, in <module>
    from .. import SentenceTransformer
  File "/home/yekyaw.thu/.local/lib/python3.7/site-packages/sentence_transformers/SentenceTransformer.py", line 27, in <module>
    from .models import Transformer, Pooling, Dense
  File "/home/yekyaw.thu/.local/lib/python3.7/site-packages/sentence_transformers/models/__init__.py", line 1, in <module>
    from .Transformer import Transformer
  File "/home/yekyaw.thu/.local/lib/python3.7/site-packages/sentence_transformers/models/Transformer.py", line 2, in <module>
    from transformers import AutoModel, AutoTokenizer, AutoConfig, T5Config
  File "<frozen importlib._bootstrap>", line 1032, in _handle_fromlist
  File "/home/yekyaw.thu/.local/lib/python3.7/site-packages/transformers/utils/import_utils.py", line 1053, in __getattr__
    module = self._get_module(self._class_to_module[name])
  File "/home/yekyaw.thu/.local/lib/python3.7/site-packages/transformers/utils/import_utils.py", line 1068, in _get_module
    ) from e
RuntimeError: Failed to import transformers.models.auto because of the following error (look up to see its traceback):
cannot import name 'AddedToken' from 'tokenizers' (unknown location)
```

## Make Installation from Source

```
(sentence-transformer) yekyaw.thu@gpu:~/tool$ git clone https://github.com/UKPLab/sentence-transformers
Cloning into 'sentence-transformers'...
remote: Enumerating objects: 6923, done.
remote: Total 6923 (delta 0), reused 0 (delta 0), pack-reused 6923
Receiving objects: 100% (6923/6923), 16.87 MiB | 12.24 MiB/s, done.
Resolving deltas: 100% (4754/4754), done.
(sentence-transformer) yekyaw.thu@gpu:~/tool$
```

```
(sentence-transformer) yekyaw.thu@gpu:~/tool/sentence-transformers$ pip install -e .
...
...
...
es (from transformers<5.0.0,>=4.6.0->sentence-transformers==2.2.2) (2022.9.13)
Requirement already satisfied: tokenizers!=0.11.3,<0.14,>=0.11.1 in /home/yekyaw.thu/.local/lib/python3.7/site-packages (from transformers<5.0.0,>=4.6.0->sentence-transformers==2.2.2) (0.13.1)
Requirement already satisfied: six in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from nltk->sentence-transformers==2.2.2) (1.14.0)
Requirement already satisfied: joblib>=0.11 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from scikit-learn->sentence-transformers==2.2.2) (0.14.1)
Requirement already satisfied: pillow!=8.3.*,>=5.3.0 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from torchvision->sentence-transformers==2.2.2) (7.0.0)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from packaging>=20.9->huggingface-hub>=0.4.0->sentence-transformers==2.2.2) (2.4.6)
Requirement already satisfied: zipp>=0.5 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from importlib-metadata->huggingface-hub>=0.4.0->sentence-transformers==2.2.2) (2.2.0)
Requirement already satisfied: idna<3,>=2.5 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers==2.2.2) (2.8)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers==2.2.2) (1.25.8)
Requirement already satisfied: certifi>=2017.4.17 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers==2.2.2) (2019.11.28)
Requirement already satisfied: chardet<5,>=3.0.2 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->huggingface-hub>=0.4.0->sentence-transformers==2.2.2) (3.0.4)
Installing collected packages: sentence-transformers
  Attempting uninstall: sentence-transformers
    Found existing installation: sentence-transformers 2.2.2
    Uninstalling sentence-transformers-2.2.2:
      Successfully uninstalled sentence-transformers-2.2.2
  Running setup.py develop for sentence-transformers
Successfully installed sentence-transformers
```

When I try to import tokenizers, it looks OK.  

```
(sentence-transformer) yekyaw.thu@gpu:~/exp/kh-polar/sentence-transformer$ python
Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
[GCC 7.3.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import tokenizers
```

## Installation of Transformers

I think, I need to install Transformers ...  

```
(sentence-transformer) yekyaw.thu@gpu:~/tool$ git clone https://github.com/huggingface/transformers
Cloning into 'transformers'...
remote: Enumerating objects: 112685, done.
remote: Counting objects: 100% (197/197), done.
remote: Compressing objects: 100% (145/145), done.
remote: Total 112685 (delta 79), reused 122 (delta 37), pack-reused 112488
Receiving objects: 100% (112685/112685), 106.24 MiB | 13.67 MiB/s, done.
Resolving deltas: 100% (83641/83641), done.
(sentence-transformer) yekyaw.thu@gpu:~/tool$
```

```
(sentence-transformer) yekyaw.thu@gpu:~/tool/transformers$ pip install .
...
...
...
-packages (from packaging>=20.0->transformers==4.24.0.dev0) (2.4.6)
Requirement already satisfied: zipp>=0.5 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from importlib-metadata->transformers==4.24.0.dev0) (2.2.0)
Requirement already satisfied: idna<3,>=2.5 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->transformers==4.24.0.dev0) (2.8)
Requirement already satisfied: chardet<5,>=3.0.2 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->transformers==4.24.0.dev0) (3.0.4)
Requirement already satisfied: certifi>=2017.4.17 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->transformers==4.24.0.dev0) (2019.11.28)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /opt/anaconda/anaconda3/lib/python3.7/site-packages (from requests->transformers==4.24.0.dev0) (1.25.8)
Building wheels for collected packages: transformers
  Building wheel for transformers (pyproject.toml) ... done
  Created wheel for transformers: filename=transformers-4.24.0.dev0-py3-none-any.whl size=5426778 sha256=991ca58d95453e3967586ea511f81427571312c3a15e3940da245a684c7a4c4a
  Stored in directory: /tmp/pip-ephem-wheel-cache-ym4z_a3w/wheels/1a/3d/4b/a9307de3a7b41a2264a45216a868980393403baf9b5cbe5d96
Successfully built transformers
Installing collected packages: transformers
  Attempting uninstall: transformers
    Found existing installation: transformers 4.23.1
    Uninstalling transformers-4.23.1:
      Successfully uninstalled transformers-4.23.1
  WARNING: The script transformers-cli is installed in '/home/yekyaw.thu/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed transformers-4.24.0.dev0
```

## Try Test-Run Again

I still got the same error ...  
Why?!  

When I tried to install tokenizer:  

```
(sentence-transformer) yekyaw.thu@gpu:~/exp/kh-polar/sentence-transformer$ pip install tokenizers
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: tokenizers in /home/yekyaw.thu/.local/lib/python3.7/site-packages (0.13.1)
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




