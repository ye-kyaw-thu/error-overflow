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




