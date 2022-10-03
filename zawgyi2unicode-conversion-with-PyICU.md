## Install PyICU

```
(base) ye@ykt-pro:/media/ye/project1/4github/zawgyi2unicode$ pip install PyICU
Collecting PyICU
  Downloading PyICU-2.9.tar.gz (305 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 305.2/305.2 kB 515.9 kB/s eta 0:00:00
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Building wheels for collected packages: PyICU
  Building wheel for PyICU (pyproject.toml) ... done
  Created wheel for PyICU: filename=PyICU-2.9-cp37-cp37m-linux_x86_64.whl size=1584265 sha256=28da90d6e43ba4ec5da8b414e881868b7edc53b33bd5d061ea72ea70c6ae7335
  Stored in directory: /home/ye/.cache/pip/wheels/28/88/93/6c1b06361e4cbd4e7f793fb456729f69798f9aa3fc2a791cd7
Successfully built PyICU
Installing collected packages: PyICU
Successfully installed PyICU-2.9
(base) ye@ykt-pro:/media/ye/project1/4github/zawgyi2unicode$
```

## Writing Python Code


```python
from icu import Transliterator
import sys

# Written by Ye Kyaw Thu, Affiliate Professor, IDRI, CADT, Cambodia
# Converting Zawgyi to Unicode Encoding
# Last updated: 1 Oct 2022
# How to run:
# If you don't have icu library, do installation: "pip install PyICU"
# $ python ./zawgyi2unicode.py ./eg-corpus-zawgyi.txt
#
# References
# https://github.com/google/myanmar-tools/blob/master/clients/python/README.rst

with open(sys.argv[1]) as f:
    corpus = []
    for line in f:
        corpus.append(line.rstrip())
#print(corpus)

for zawgyi_line in corpus:
   converter = Transliterator.createInstance('Zawgyi-my')
   uni_line = converter.transliterate(zawgyi_line)
   print(uni_line)


```

## Prepare a Small Corpus

```
(base) ye@ykt-pro:/media/ye/project1/4github/zawgyi2unicode$ cat ./eg-corpus-zawgyi.txt 
ေနေကာင္း တယ္ ေနာ္
အခု ဘာ လုပ္ ေန သလဲ
ေနေကာင္း ေအာင္ ေန ပါ ေနာ္
အခု အလုပ္ လုပ္ ေန တယ္
(base) ye@ykt-pro:/media/ye/project1/4github/zawgyi2unicode$ 
```

## Test Conversion

```
(base) ye@ykt-pro:/media/ye/project1/4github/zawgyi2unicode$ python ./zawgyi2unicode.py ./eg-corpus-zawgyi.txt 
နေကောင်း တယ် နော်
အခု ဘာ လုပ် နေ သလဲ
နေကောင်း အောင် နေ ပါ နော်
အခု အလုပ် လုပ် နေ တယ်
(base) ye@ykt-pro:/media/ye/project1/4github/zawgyi2unicode$
```


