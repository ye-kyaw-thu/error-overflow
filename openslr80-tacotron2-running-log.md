# Note for preparing quick TTS with OpenSLR-80 dataset

## Data Format

```
metadata.txt
audio1|This is my sentence.
audio2|This is maybe my sentence.
audio3|This is certainly my sentence.
audio4|Let this be your sentence.
...
```

In details:  

```
DUMMY/LJ022-0023.wav|The overwhelming majority of people in this country know how to sift the wheat from the chaff in what they hear and what they read.
DUMMY/LJ043-0030.wav|If somebody did that to me, a lousy trick like that, to take my wife away, and all the furniture, I would be mad as hell, too.
DUMMY/LJ005-0201.wav|as is shown by the report of the Commissioners to inquire into the state of the municipal corporations in eighteen thirty-five.
```

We have to prepare following folder structure:  

```
/MyTTSDataset
      |
      | -> metadata.txt
      | -> /wavs
              | -> audio1.wav
              | -> audio2.wav
              | ...
```

## Git Clone

```
git clone https://github.com/NVIDIA/tacotron2.git  

root@7a5711b4fb3e:/home/ye/exp/tts/tacotron2# ls
Dockerfile           data_utils.py   hparams.py       loss_function.py  plotting_utils.py  text
LICENSE              demo.wav        inference.ipynb  loss_scaler.py    requirements.txt   train.py
README.md            distributed.py  layers.py        model.py          stft.py            utils.py
audio_processing.py  filelists       logger.py        multiproc.py      tensorboard.png    waveglow
root@7a5711b4fb3e:/home/ye/exp/tts/tacotron2#
```

## Initialize Submodule

```
root@7a5711b4fb3e:/home/ye/exp/tts/tacotron2# git submodule init; git submodule update
Submodule 'waveglow' (https://github.com/NVIDIA/waveglow) registered for path 'waveglow'
Cloning into '/home/ye/exp/tts/tacotron2/waveglow'...
Submodule path 'waveglow': checked out '5bc2a53e20b3b533362f974cfa1ea0267ae1c2b1'
root@7a5711b4fb3e:/home/ye/exp/tts/tacotron2#
```

## Updating .wav Paths

If you are using LJSpeech dataset:  

```
sed -i -- 's,DUMMY,ljs_dataset_folder/wavs,g' filelists/*.txt 
```

```
The `sed` command is a stream editor for filtering and transforming text. Here is a breakdown of the command you provided:  

- `sed`: This invokes the stream editor utility.
- `-i`: This option means "in-place", i.e., it will edit files in place (makes backup if an extension is supplied).
- `--`: This is an "end of options" indicator. This is useful when file names start with a "-" and could be mistaken for options.
- `'s,DUMMY,ljs_dataset_folder/wavs,g'`: This is the script that `sed` will run. The `s` character indicates a substitution command. The `/` character is often used as the delimiter for the arguments of this command, but in this case, the `,` character is used instead for readability (because the replacement text contains `/`). The `DUMMY` is the pattern that `sed` will look for, and `ljs_dataset_folder/wavs` is the text that will replace the pattern. The `g` after the final `,` is a flag that tells `sed` to apply the substitution globally in each line (without the `g`, only the first match on each line would be replaced).
- `filelists/*.txt`: This is the set of files that `sed` will operate on. It will apply the provided script to every `.txt` file in the `filelists` directory.

So, in short, this command replaces every occurrence of the word "DUMMY" with "ljs_dataset_folder/wavs" in all the `.txt` files located in the `filelists` directory. The changes are done in-place, meaning the original files are modified.

Or Alternatively, 

Set load_mel_from_disk=True in hparams.py and update mel-spectrogram paths.
```

## Check hparams.py

We need to update following parts:  

```

        ################################
        # Data Parameters             #
        ################################
        load_mel_from_disk=False,
        training_files='filelists/ljs_audio_text_train_filelist.txt',
        validation_files='filelists/ljs_audio_text_val_filelist.txt',
        text_cleaners=['english_cleaners'],
```

## Example Training/Val/Test

```
root@500e9f8181d8:/home/ye/exp/tts/tacotron2/filelists# wc *
    500    8494   60834 ljs_audio_text_test_filelist.txt
  12500  212377 1524164 ljs_audio_text_train_filelist.txt
    100    1653   11911 ljs_audio_text_val_filelist.txt
  13100  222524 1596909 total
```

For me, I will use 5% of the OpenSLR-80 data for 1st time Tacotron2 TTS model building as follows:  

```
t@500e9f8181d8:/home/ye/exp/speech_data# wc line_index_female.txt
  2530   2531 541101 line_index_female.txt
```

Training Data:  

```
root@500e9f8181d8:/home/ye/exp/speech_data# head -n 2303 ./line_index_female.txt > openslr80_train.txt
```

Test Data:  

```
root@500e9f8181d8:/home/ye/exp/speech_data# tail -n 127 ./line_index_female.txt > openslr80_test.txt
```

Validation Data:  

```
root@500e9f8181d8:/home/ye/exp/speech_data# head -n 2403 ./line_index_female.txt | tail -n 100 > openslr80_val.txt
```

Rechecking:  

```
root@500e9f8181d8:/home/ye/exp/speech_data# wc openslr80_*
   127    127  27143 openslr80_test.txt
  2303   2304 493421 openslr80_train.txt
   100    100  20537 openslr80_val.txt
  2530   2531 541101 total
```

## Folder Structure for Myanmar Data

```
/home/ye/exp/speech_data/MyanmarSpeech/
.
|-- openslr80_test.txt
|-- openslr80_train.txt
|-- openslr80_val.txt
`-- wavs
    |-- my_0366_0045318711.wav
    |-- my_0366_0096392289.wav
    |-- my_0366_0178258874.wav
    |-- my_0366_0235517782.wav
    |-- my_0366_0432235369.wav
    |-- my_0366_0445549145.wav 
```

## Format of Sample Transcriptions

```
root@500e9f8181d8:/home/ye/exp/tts/tacotron2/filelists# ls
ljs_audio_text_test_filelist.txt  ljs_audio_text_train_filelist.txt  ljs_audio_text_val_filelist.txt
root@500e9f8181d8:/home/ye/exp/tts/tacotron2/filelists# head -n 3 ljs_audio_text_*.txt
==> ljs_audio_text_test_filelist.txt <==
DUMMY/LJ045-0096.wav|Mrs. De Mohrenschildt thought that Oswald,
DUMMY/LJ049-0022.wav|The Secret Service believed that it was very doubtful that any President would ride regularly in a vehicle with a fixed top, even though transparent.
DUMMY/LJ033-0042.wav|Between the hours of eight and nine p.m. they were occupied with the children in the bedrooms located at the extreme east end of the house.

==> ljs_audio_text_train_filelist.txt <==
DUMMY/LJ050-0234.wav|It has used other Treasury law enforcement agents on special experiments in building and route surveys in places to which the President frequently travels.
DUMMY/LJ019-0373.wav|to avail himself of his powers, as it was difficult to bring home the derelictions of duties and evasion of the acts. Too much was left to the inspectors.
DUMMY/LJ050-0207.wav|Although Chief Rowley does not complain about the pay scale for Secret Service agents,

==> ljs_audio_text_val_filelist.txt <==
DUMMY/LJ022-0023.wav|The overwhelming majority of people in this country know how to sift the wheat from the chaff in what they hear and what they read.
DUMMY/LJ043-0030.wav|If somebody did that to me, a lousy trick like that, to take my wife away, and all the furniture, I would be mad as hell, too.
DUMMY/LJ005-0201.wav|as is shown by the report of the Commissioners to inquire into the state of the municipal corporations in eighteen thirty-five.
root@500e9f8181d8:/home/ye/exp/tts/tacotron2/filelists#
```

## Preparing Transcription Files for OpenSLR-80 Data

```
root@500e9f8181d8:/home/ye/exp/speech_data/MyanmarSpeech# sed -i -- 's,^,/home/ye/exp/speech_data/MyanmarSpeech/wavs/,g' *.txt
root@500e9f8181d8:/home/ye/exp/speech_data/MyanmarSpeech# head -n 3 *.txt
==> openslr80_test.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7447_7747402294 အောင်မြင်နနဲ့ လုပ်ငန်း တစ်ခု ကကို ရရှိလနိုင်မှာ ဖြစ်တယ် လလိလို့ မခခိုင်လွင်ခြူး က ပြောပါတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_3187293861 ဖုန်း နနဲ့တော့ အလှအပလေးတွေ ရရိုက်ဖြစ်ပါတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_1311639034 ကုန်းပွဲ ဆဆိုတာက သံဃာတော်တွေ ကကို ဆွမ်း လောင်းလှူ ပြီး ဇာတ်သဘင်တွေ နနဲ့ ကျင်းပတာပါ

==> openslr80_train.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7865_1250917969 ပြီးတော့ တရုတ် နနဲ့လည်း ချစ်ကြည်ရင်းနှီတဲ့ ဆက်ဆံရေး ရှိတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_8698_6883351313 အအဲ့ဒီ ဝေဖန်မှုတွေ နနဲ့ ပတ်သက် လလိလို့ ဘယ်လလို တတုတုံ့ပြန်ချင်ပါသလဲ
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_3260_8853590661 မမီ မွေးဖွားနေတတဲ့ အချိန် မှာတော့ ဘုရားဂုဏ်တော် ကကိုပဲ တောက်လျှောက် ရွတ်နေခခဲ့ပါတယ်

==> openslr80_val.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_5153800262 ယခု လတ်တလော တွင် အာရှ စိမ်းလန်းမှု ဖွွံ့ဖြြိုးရေး ဘဏ် လီမိတက် ၏ ငွေအပ်နှံသူများ ကြား ဂယက် ရရိုက်ခတ်မှုများ ရှိနေသည်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_6118_4929981963 မြြိြို့လယ်ခေါင် ကတ္တရာ လမ်းမကြီး ပေါ် ဗြစ် ဆဆိုပြီး ဒီအတတိုင်း ထွေးချလလိုက်တာ ပါ
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_4632_8001334672 ဒီ ပစ္စည်းလေး တစ်ခု ထဲ မှာ သက်ဝင်နေတတဲ့ မေတ္တာတရားတွေ က အများကြီး ပဲ
root@500e9f8181d8:/home/ye/exp/speech_data/MyanmarSpeech#
```
 
I need to make search and replace for TAB:  

```
root@500e9f8181d8:/home/ye/exp/speech_data/MyanmarSpeech# sed -i "s/$(echo '\t')/.wav\|/g" *.txt
```

Checking:  

```
root@500e9f8181d8:/home/ye/exp/speech_data/MyanmarSpeech# head -n 2 *.txt
==> openslr80_test.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7447_7747402294.wav|အောင်မြင်နနဲ့ လုပ်ငန်း တစ်ခု ကကို ရှိလာနနိုင်မှာ ဖြစ်တယ် လလိလို့ မခခိုင်လွင်ခြူး က ပြောပါတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_3187293861.wav|ဖုန်း နနဲ့တော့ အလှအပလေးတွေ ရရိုက်ဖြစ်ပါတယ်

==> openslr80_train.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7865_1250917969.wav|ပြီးတော့ တရုတ် နနဲ့လည်း ချစ်ကြည်ရင်းနှီးတတဲ့ ဆက်ဆံရေး ရှိတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_8698_6883351313.wav|အအဲ့ဒီ ဝေဖန်မှုတွေ နနဲ့ ပတ်သက် လလိလို့ ဘယ်လလို တတုတုံ့ပြန်ချင်ပါသလဲ

==> openslr80_val.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_5153800262.wav|ယခု လတ်တလော တွင် အာရှ စိမ်းလန်းမှု ွံ့ဖြြိုးရေး ဘဏ် လီမိတက် ၏ ငွေအပ်နှံသူများ ကြား ဂယက် ရရိုက်ခတ်မှုများ ရှိနေသည်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_6118_4929981963.wav|မြြိြို့လယ်ခေါင် ကတ္တရာ လမ်းမကြီး ပေါ် ဗြစ် ဆ                                                                                                ဆိ                                                                                                       ဆို                                                                                                      ဆိုပြီး ဒီအတတိုင်း ထွေးချလလိုက်တာ ပါ
root@500e9f8181d8:/home/ye/exp/speech_data/MyanmarSpeech#
```

## Updated

```
        ################################
        # Data Parameters             #
        ################################
        load_mel_from_disk=False,
        training_files='/home/ye/exp/speech_data/MyanmarSpeech/openslr80_train.txt',
        validation_files='/home/ye/exp/speech_data/MyanmarSpeech/openslr80_val.txt',
        text_cleaners=['basic_cleaners'],
```

## Updating the Symbols List 

At 1st, backup symbol file.  

```
root@500e9f8181d8:/home/ye/exp/tts/tacotron2/text# ls
LICENSE  __init__.py  cleaners.py  cmudict.py  numbers.py  symbols.py
root@500e9f8181d8:/home/ye/exp/tts/tacotron2/text# mkdir backup
root@500e9f8181d8:/home/ye/exp/tts/tacotron2/text# cp symbols.py ./backup/
```

The following is the original symbols.py file:  

```python
""" from https://github.com/keithito/tacotron """

'''
Defines the set of symbols used in text input to the model.

The default is a set of ASCII characters that works well for English or text that has been run through U>
from text import cmudict

_pad        = '_'
_punctuation = '!\'(),.:;? '
_special = '-'
_letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz'

# Prepend "@" to ARPAbet symbols to ensure uniqueness (some are the same as uppercase letters):
_arpabet = ['@' + s for s in cmudict.valid_symbols]

# Export all symbols:
symbols = [_pad] + list(_special) + list(_punctuation) + list(_letters) + _arpabet
```

Then I updated as follows:  

```python
_pad        = '_'
_punctuation = '၊။!\'(),.:;? '
_special = '-'
_letters = 'ကခဂဃငစဆဇဈဉညဋဌဍဎဏတထဒဓနပဖဗဘမယရလဝသဟဠအဣဤဥဦဧဩဪါာိီုူေဲံး္်ျြှဿ၌၍၎၏'
```

## Creating a New Conda Environment

```
conda create --name tacotron2 python=3.8
conda activate tacotron2
```

```
pip install -r requirements.txt
```

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2/backup# cat requirements.txt
#matplotlib==2.1.0
#numpy==1.13.3
inflect==0.2.5
librosa==0.6.0
scipy==1.0.0
Unidecode==1.0.22
pillow
```
ငါက original requirements.txt မှာပါတဲ့ tensorflow ကို မလိုဘူးထင်လို့ ဖြုတ်ထားခဲ့တာ။ ဘာကြောင့်လဲ ဆိုတော့ Tacotron2 က Pytorch ကို သုံးတာမို့လို့။ သို့သော် တကယ်တမ်းက tensorflow ကိုလည်း installation လုပ်ဖို့ လိုအပ်တယ်။ hyperparameter စတာတွေကို setting လုပ်ထားတဲ့ config ဖိုင်ကို ဖတ်တာက tensorflow library ကို သုံးပြီးဖတ်ဖို့ ရေးထားတာမို့လို့ ...  

I have to install matplotlib separately.  

Pytorch Installation:  

```
conda install mkl mkl-include
```

Check the cuda version:  

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2/backup# nvcc --version
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2022 NVIDIA Corporation
Built on Wed_Jun__8_16:49:14_PDT_2022
Cuda compilation tools, release 11.7, V11.7.99
Build cuda_11.7.r11.7/compiler.31442593_0
```

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2/backup# conda install -c pytorch magma-cuda110
...
...
...
The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    intel-openmp-2020.2        |              254         947 KB
    magma-cuda110-2.5.2        |                1        65.2 MB  pytorch
    ------------------------------------------------------------
                                           Total:        66.2 MB

The following NEW packages will be INSTALLED:

    magma-cuda110: 2.5.2-1                pytorch

The following packages will be DOWNGRADED:

    intel-openmp:  2022.0.1-h06a4308_3633         --> 2020.2-254

Proceed ([y]/n)? y


Downloading and Extracting Packages
intel-openmp-2020.2  | 947 KB    | ############################################################## | 100%
magma-cuda110-2.5.2  | 65.2 MB   | ############################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
```

Reference:
https://github.com/pytorch/pytorch#installation  

## Pytorch Installation

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts# pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu117

...
...
...

Collecting urllib3<3,>=1.21.1 (from requests->torchvision)
  Downloading urllib3-2.0.3-py3-none-any.whl (123 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 123.6/123.6 kB 8.3 MB/s eta 0:00:00
Collecting certifi>=2017.4.17 (from requests->torchvision)
  Downloading certifi-2023.5.7-py3-none-any.whl (156 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 157.0/157.0 kB 11.1 MB/s eta 0:00:00
Collecting mpmath>=0.19 (from sympy->torch)
  Downloading mpmath-1.3.0-py3-none-any.whl (536 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 536.2/536.2 kB 30.0 MB/s eta 0:00:00
Building wheels for collected packages: lit
  Building wheel for lit (pyproject.toml) ... done
  Created wheel for lit: filename=lit-16.0.6-py3-none-any.whl size=93582 sha256=1d73dee1a709bfca0d63abd169609911d8070fc442779e49fe9da3ac1c6ad080
  Stored in directory: /root/.cache/pip/wheels/05/ab/f1/0102fea49a41c753f0e79a1a4012417d5d7ef0f93224694472
Successfully built lit
Installing collected packages: mpmath, lit, cmake, urllib3, typing-extensions, sympy, networkx, MarkupSafe, idna, filelock, charset-normalizer, certifi, requests, jinja2, triton, torch, torchvision, torchaudio
Successfully installed MarkupSafe-2.1.3 certifi-2023.5.7 charset-normalizer-3.1.0 cmake-3.26.4 filelock-3.12.2 idna-3.4 jinja2-3.1.2 lit-16.0.6 mpmath-1.3.0 networkx-3.1 requests-2.31.0 sympy-1.12 torch-2.0.1+cu117 torchaudio-2.0.2+cu117 torchvision-0.15.2+cu117 triton-2.0.0 typing-extensions-4.7.0 urllib3-2.0.3
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
```

Check ...   

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/apex# python
Python 3.8.13 (default, Mar 28 2022, 11:38:47)
[GCC 7.5.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> print(torch.__version__)
2.0.1+cu117
```

Reference:   
https://www.scaler.com/topics/pytorch/install-pytorch/  

## Apex Installation

```
git clone https://github.com/NVIDIA/apex
```

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/apex# pip install -v --disable-pip-version-check --no-cache-dir --no-build-isolation --config-settings "--build-option=--cpp_ext" --config-settings "--build-option=--cuda_ext" ./
...
...
...
  adding 'apex/transformer/testing/standalone_bert.py'
  adding 'apex/transformer/testing/standalone_gpt.py'
  adding 'apex/transformer/testing/standalone_transformer_lm.py'
  adding 'apex-0.1.dist-info/LICENSE'
  adding 'apex-0.1.dist-info/METADATA'
  adding 'apex-0.1.dist-info/WHEEL'
  adding 'apex-0.1.dist-info/top_level.txt'
  adding 'apex-0.1.dist-info/RECORD'
  removing build/bdist.linux-x86_64/wheel
  /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/utils/cpp_extension.py:476: UserWarning: Attempted to use ninja as the BuildExtension backend but we could not find ninja.. Falling back to using the slow distutils backend.
    warnings.warn(msg.format('we could not find ninja.'))
  Building wheel for apex (pyproject.toml) ... done
  Created wheel for apex: filename=apex-0.1-cp38-cp38-linux_x86_64.whl size=31942705 sha256=4f3571c6967162f5a5096585fffcfadec6501971f17aa92e7ec21506e2759099
  Stored in directory: /tmp/pip-ephem-wheel-cache-nxs4pio1/wheels/01/ae/5b/2b9fc704bb07e41050655d70dc7a9cdaf33e2be193958c2357
Successfully built apex
Installing collected packages: apex
Successfully installed apex-0.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
```

Reference:  
https://github.com/nvidia/apex   

## Installation of Librosa Library

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# pip install librosa
...
...
...

Collecting threadpoolctl>=2.0.0 (from scikit-learn>=0.20.0->librosa)
  Using cached threadpoolctl-3.1.0-py3-none-any.whl (14 kB)
Collecting cffi>=1.0 (from soundfile>=0.12.1->librosa)
  Downloading cffi-1.15.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (442 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 442.7/442.7 kB 29.7 MB/s eta 0:00:00
Collecting pycparser (from cffi>=1.0->soundfile>=0.12.1->librosa)
  Downloading pycparser-2.21-py2.py3-none-any.whl (118 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 118.7/118.7 kB 23.7 MB/s eta 0:00:00
Requirement already satisfied: charset-normalizer<4,>=2 in /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages (from requests>=2.19.0->pooch<1.7,>=1.0->librosa) (3.1.0)
Requirement already satisfied: idna<4,>=2.5 in /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages (from requests>=2.19.0->pooch<1.7,>=1.0->librosa) (3.4)
Requirement already satisfied: urllib3<3,>=1.21.1 in /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages (from requests>=2.19.0->pooch<1.7,>=1.0->librosa) (2.0.3)
Requirement already satisfied: certifi>=2017.4.17 in /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages (from requests>=2.19.0->pooch<1.7,>=1.0->librosa) (2023.5.7)
Requirement already satisfied: zipp>=0.5 in /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages (from importlib-metadata->numba>=0.51.0->librosa) (3.15.0)
Installing collected packages: msgpack, appdirs, threadpoolctl, soxr, pycparser, llvmlite, lazy-loader, joblib, importlib-metadata, decorator, audioread, scikit-learn, pooch, numba, cffi, soundfile, librosa
Successfully installed appdirs-1.4.4 audioread-3.0.0 cffi-1.15.1 decorator-5.1.1 importlib-metadata-6.7.0 joblib-1.3.1 lazy-loader-0.3 librosa-0.10.0.post2 llvmlite-0.40.1 msgpack-1.0.5 numba-0.57.1 pooch-1.6.0 pycparser-2.21 scikit-learn-1.3.0 soundfile-0.12.1 soxr-0.3.5 threadpoolctl-3.1.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
```

## Installation of unidecode

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# pip install unidecode
Collecting unidecode
  Downloading Unidecode-1.3.6-py3-none-any.whl (235 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 235.9/235.9 kB 2.6 MB/s eta 0:00:00
Installing collected packages: unidecode
Successfully installed unidecode-1.3.6
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#
```

## Installation of inflact

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# pip install inflect
Collecting inflect
  Downloading inflect-6.0.4-py3-none-any.whl (34 kB)
Collecting pydantic>=1.9.1 (from inflect)
  Downloading pydantic-2.0-py3-none-any.whl (355 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 355.6/355.6 kB 4.3 MB/s eta 0:00:00
Collecting annotated-types>=0.4.0 (from pydantic>=1.9.1->inflect)
  Downloading annotated_types-0.5.0-py3-none-any.whl (11 kB)
Collecting pydantic-core==2.0.1 (from pydantic>=1.9.1->inflect)
  Downloading pydantic_core-2.0.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.5 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.5/1.5 MB 19.2 MB/s eta 0:00:00
Requirement already satisfied: typing-extensions>=4.6.1 in /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages (from pydantic>=1.9.1->inflect) (4.7.0)
Installing collected packages: pydantic-core, annotated-types, pydantic, inflect
Successfully installed annotated-types-0.5.0 inflect-6.0.4 pydantic-2.0 pydantic-core-2.0.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#
```

## Installation of Tensorboard

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# conda install -c anaconda tensorboardw
```

## Installation of Tensorflow

According to the GitHub source, requirement, when I tried to install specific version, I got following error:  

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# pip install tensorflow==1.15.2
ERROR: Could not find a version that satisfies the requirement tensorflow==1.15.2 (from versions: 2.2.0, 2.2.1, 2.2.2, 2.2.3, 2.3.0, 2.3.1, 2.3.2, 2.3.3, 2.3.4, 2.4.0, 2.4.1, 2.4.2, 2.4.3, 2.4.4, 2.5.0, 2.5.1, 2.5.2, 2.5.3, 2.6.0rc0, 2.6.0rc1, 2.6.0rc2, 2.6.0, 2.6.1, 2.6.2, 2.6.3, 2.6.4, 2.6.5, 2.7.0rc0, 2.7.0rc1, 2.7.0, 2.7.1, 2.7.2, 2.7.3, 2.7.4, 2.8.0rc0, 2.8.0rc1, 2.8.0, 2.8.1, 2.8.2, 2.8.3, 2.8.4, 2.9.0rc0, 2.9.0rc1, 2.9.0rc2, 2.9.0, 2.9.1, 2.9.2, 2.9.3, 2.10.0rc0, 2.10.0rc1, 2.10.0rc2, 2.10.0rc3, 2.10.0, 2.10.1, 2.11.0rc0, 2.11.0rc1, 2.11.0rc2, 2.11.0, 2.11.1, 2.12.0rc0, 2.12.0rc1, 2.12.0, 2.13.0rc0, 2.13.0rc1, 2.13.0rc2)
ERROR: No matching distribution found for tensorflow==1.15.2
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#
```

So, try installation again without version information as follows:   

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# pip install tensorflown
...
...
...

# Trainisting installation: protobuf 3.20.1
    Uninstalling protobuf-3.20.1:
      Successfully uninstalled protobuf-3.20.1
  Attempting uninstall: grpcio
    Found existing installation: grpcio 1.42.0
    Uninstalling grpcio-1.42.0:
      Successfully uninstalled grpcio-1.42.0
  Attempting uninstall: google-auth
    Found existing installation: google-auth 2.6.0
    Uninstalling google-auth-2.6.0:
      Successfully uninstalled google-auth-2.6.0
  Attempting uninstall: google-auth-oauthlib
    Found existing installation: google-auth-oauthlib 0.4.4
    Uninstalling google-auth-oauthlib-0.4.4:
      Successfully uninstalled google-auth-oauthlib-0.4.4
  Attempting uninstall: tensorboard
    Found existing installation: tensorboard 2.10.0
    Uninstalling tensorboard-2.10.0:
      Successfully uninstalled tensorboard-2.10.0
Successfully installed astunparse-1.6.3 flatbuffers-23.5.26 gast-0.4.0 google-auth-2.21.0 google-auth-oauthlib-1.0.0 google-pasta-0.2.0 grpcio-1.56.0 h5py-3.9.0 jax-0.4.13 keras-2.12.0 libclang-16.0.0 ml-dtypes-0.2.0 opt-einsum-3.3.0 protobuf-4.23.3 tensorboard-2.12.3 tensorboard-data-server-0.7.1 tensorflow-2.12.0 tensorflow-estimator-2.12.0 tensorflow-io-gcs-filesystem-0.32.0 termcolor-2.3.0 wrapt-1.14.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
```

## 1st Time Training

--help  of the train.py  

```
usage: train.py [-h] [-o OUTPUT_DIRECTORY] [-l LOG_DIRECTORY] [-c CHECKPOINT_PATH] [--warm_start]
                [--n_gpus N_GPUS] [--rank RANK] [--group_name GROUP_NAME] [--hparams HPARAMS]

optional arguments:
  -h, --help            show this help message and exit
  -o OUTPUT_DIRECTORY, --output_directory OUTPUT_DIRECTORY
                        directory to save checkpoints
  -l LOG_DIRECTORY, --log_directory LOG_DIRECTORY
                        directory to save tensorboard logs
  -c CHECKPOINT_PATH, --checkpoint_path CHECKPOINT_PATH
                        checkpoint path
  --warm_start          load model weights only, ignore specified layers
  --n_gpus N_GPUS       number of gpus
  --rank RANK           rank of current gpu
  --group_name GROUP_NAME
                        Distributed group name
  --hparams HPARAMS
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts
```

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log
...
...
...
Train loss 7082 0.412546 Grad Norm 1.326766 1.15s/it
Train loss 7083 0.442348 Grad Norm 0.439335 1.29s/it
Train loss 7084 0.502699 Grad Norm 1.721761 0.94s/it
Train loss 7085 0.430646 Grad Norm 0.431681 1.17s/it
Train loss 7086 0.489362 Grad Norm 1.545038 1.07s/it
Train loss 7087 0.468387 Grad Norm 0.601807 1.07s/it
Train loss 7088 0.412929 Grad Norm 0.800758 1.20s/it
Train loss 7089 0.394863 Grad Norm 1.007312 1.21s/it
Train loss 7090 0.459458 Grad Norm 0.487108 1.14s/it
Validation loss 7090:  0.495267
Saving model and optimizer state at iteration 7090 to openslr80/checkpoint_7090
Train loss 7091 0.466869 Grad Norm 1.237727 1.19s/it
Train loss 7092 0.439850 Grad Norm 0.593846 1.15s/it
Train loss 7093 0.557422 Grad Norm 0.915906 0.98s/it
Train loss 7094 0.472237 Grad Norm 1.514263 1.12s/it
Train loss 7095 0.429938 Grad Norm 0.493557 1.40s/it
Train loss 7096 0.466173 Grad Norm 2.209361 1.21s/it
Train loss 7097 0.498106 Grad Norm 1.305454 1.14s/it
Train loss 7098 0.459905 Grad Norm 2.490438 1.03s/it
Train loss 7099 0.476446 Grad Norm 2.249540 1.12s/it

real    192m24.442s
user    307m19.798s
sys     362m3.455s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#
```

Tacotron2 ကို OpenSLR-80 ဒေတာနည်းနည်းနဲ့ 100 epochs training လုပ်တာတော့ အောင်အောင်မြင်မြင်နဲ့ ပြီးစီးသွားခဲ့တယ်။  

## Checing Checkpoints

```
checkpoint_1830  checkpoint_2900  checkpoint_3980  checkpoint_5040  checkpoint_6110  checkpoint_800
checkpoint_1840  checkpoint_2910  checkpoint_3990  checkpoint_5050  checkpoint_6120  checkpoint_810
checkpoint_1850  checkpoint_2920  checkpoint_40    checkpoint_5060  checkpoint_6130  checkpoint_820
checkpoint_1860  checkpoint_2930  checkpoint_400   checkpoint_5070  checkpoint_6140  checkpoint_830
checkpoint_1870  checkpoint_2940  checkpoint_4000  checkpoint_5080  checkpoint_6150  checkpoint_840
checkpoint_1880  checkpoint_2950  checkpoint_4010  checkpoint_5090  checkpoint_6160  checkpoint_850
checkpoint_1890  checkpoint_2960  checkpoint_4020  checkpoint_510   checkpoint_6170  checkpoint_860
checkpoint_190   checkpoint_2970  checkpoint_4030  checkpoint_5100  checkpoint_6180  checkpoint_870
checkpoint_1900  checkpoint_2980  checkpoint_4040  checkpoint_5110  checkpoint_6190  checkpoint_880
checkpoint_1910  checkpoint_2990  checkpoint_4050  checkpoint_5120  checkpoint_620   checkpoint_890
checkpoint_1920  checkpoint_30    checkpoint_4060  checkpoint_5130  checkpoint_6200  checkpoint_90
checkpoint_1930  checkpoint_300   checkpoint_4070  checkpoint_5140  checkpoint_6210  checkpoint_900
checkpoint_1940  checkpoint_3000  checkpoint_4080  checkpoint_5150  checkpoint_6220  checkpoint_910
checkpoint_1950  checkpoint_3010  checkpoint_4090  checkpoint_5160  checkpoint_6230  checkpoint_920
checkpoint_1960  checkpoint_3020  checkpoint_410   checkpoint_5170  checkpoint_6240  checkpoint_930
checkpoint_1970  checkpoint_3030  checkpoint_4100  checkpoint_5180  checkpoint_6250  checkpoint_940
checkpoint_1980  checkpoint_3040  checkpoint_4110  checkpoint_5190  checkpoint_6260  checkpoint_950
checkpoint_1990  checkpoint_3050  checkpoint_4120  checkpoint_520   checkpoint_6270  checkpoint_960
checkpoint_20    checkpoint_3060  checkpoint_4130  checkpoint_5200  checkpoint_6280  checkpoint_970
checkpoint_200   checkpoint_3070  checkpoint_4140  checkpoint_5210  checkpoint_6290  checkpoint_980
checkpoint_2000  checkpoint_3080  checkpoint_4150  checkpoint_5220  checkpoint_630   checkpoint_990
checkpoint_2010  checkpoint_3090  checkpoint_4160  checkpoint_5230  checkpoint_6300  openslr80_log
checkpoint_2020  checkpoint_310   checkpoint_4170  checkpoint_5240  checkpoint_6310
checkpoint_2030  checkpoint_3100  checkpoint_4180  checkpoint_5250  checkpoint_6320
checkpoint_2040  checkpoint_3110  checkpoint_4190  checkpoint_5260  checkpoint_6330
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2/openslr80# ls
```


## Checking Logs

```
n2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2/openslr80/openslr80_log# ls
events.out.tfevents.1688288713.500e9f8181d8.7074.0  events.out.tfevents.1688290682.500e9f8181d8.7484.0
events.out.tfevents.1688288779.500e9f8181d8.7192.0  events.out.tfevents.1688294164.500e9f8181d8.7983.0
events.out.tfevents.1688288927.500e9f8181d8.7309.0
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2/openslr80/openslr80_log#
```

## Disk Usage

```
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# du ./openslr80/ -h
461M    ./openslr80/openslr80_log
225G    ./openslr80/
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#
```

HDD size ကတော့ တော်တော်ယူတယ်။  
အဲဒါကြောင့် checkpoint ကို အများကြီး မသိမ်းအောင် setting လုပ်မယ်။  

## Testing

Still got error in output wavefiles ...  

## Training (for 500 epochs)

Testing လုပ်ကြည့်ဖို့အတွက်က Jupyter notebook နဲ့ ပြထားတာကော၊ ပြီးတော့ အဲဒီ notebook မှာ သုံးထားတဲ့ library တွေရဲ့ ပိုင်သွန်ဗားရှင်းတွေက မတူတာကောကြောင့် testing.py ဆိုပြီး script ကို အစအဆုံးလိုလို ပြန်ရေးခဲ့ရတယ်။ သို့သော် tesging လုပ်ပြီးတော့ ရလာတဲ့ output wave file တွေမှာ ပြဿနာရှိနေသေးတယ်။ အဲဒါနဲ့ ကျောင်းသူ နှစ်ယောက်ရဲ့ ဒေတာနဲ့ training လုပ်မယ်ဆိုရင်လည်း ဘယ်လောက်ကြာမလဲဆိုတာကိုလည်း ပိုအတိအကျ ခန့်မှန်းနိုင်အောင်လို့ openslr ဒေတာနဲ့ပဲ epoch 500 အထိ training နောက်တစ်ခေါက် လုပ်ကြည့်ခဲ့တယ်။  

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log2
...
...
...
Train loss 35479 0.290018 Grad Norm 0.304541 1.17s/it
Train loss 35480 0.303260 Grad Norm 0.784043 1.22s/it
Train loss 35481 0.303583 Grad Norm 0.335501 1.05s/it
Train loss 35482 0.292122 Grad Norm 0.830861 1.28s/it
Train loss 35483 0.296945 Grad Norm 0.697048 1.09s/it
Train loss 35484 0.269489 Grad Norm 0.199639 1.44s/it
Train loss 35485 0.295312 Grad Norm 0.532426 1.14s/it
Train loss 35486 0.296445 Grad Norm 1.264659 1.16s/it
Train loss 35487 0.289710 Grad Norm 0.346991 1.09s/it
Train loss 35488 0.282089 Grad Norm 0.859849 1.30s/it
Train loss 35489 0.309729 Grad Norm 0.553891 1.14s/it
Train loss 35490 0.244908 Grad Norm 0.227702 1.24s/it
Train loss 35491 0.250027 Grad Norm 0.494088 1.13s/it
Train loss 35492 0.268798 Grad Norm 0.349192 1.24s/it
Train loss 35493 0.291858 Grad Norm 0.588458 1.13s/it
Train loss 35494 0.292340 Grad Norm 0.548000 1.12s/it
Train loss 35495 0.307799 Grad Norm 0.288330 1.08s/it
Train loss 35496 0.278712 Grad Norm 0.288818 1.20s/it
Train loss 35497 0.282973 Grad Norm 0.378105 1.17s/it
Train loss 35498 0.287030 Grad Norm 0.547096 1.14s/it
Train loss 35499 0.321029 Grad Norm 0.804215 1.01s/it

real    745m39.197s
user    936m6.811s
sys     451m30.500s

## Testing











## Training Error FYI

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log
Traceback (most recent call last):
  File "train.py", line 14, in <module>
    from data_utils import TextMelLoader, TextMelCollate
  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 8, in <module>
    from text import text_to_sequence
  File "/home/ye/exp/tts/tacotron2/text/__init__.py", line 3, in <module>
    from text import cleaners
  File "/home/ye/exp/tts/tacotron2/text/cleaners.py", line 17, in <module>
    from .numbers import normalize_numbers
  File "/home/ye/exp/tts/tacotron2/text/numbers.py", line 3, in <module>
    import inflect
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/inflect/__init__.py", line 77, in <module>
    from pydantic.typing import Annotated
ImportError: cannot import name 'Annotated' from 'pydantic.typing' (/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/pydantic/typing.py)

real    0m1.278s
user    0m2.041s
sys     0m2.861s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

----------

For the above error, I reinstall as follows:

mkl_random-1.1.1     | 394 KB    | ############################################################## | 100%
pytorch-2.0.1        | 86.0 MB   | ############################################################## | 100%
charset-normalizer-2 | 33 KB     | ############################################################## | 100%
six-1.16.0           | 19 KB     | ############################################################## | 100%
cffi-1.15.0          | 226 KB    | ############################################################## | 100%
mkl-service-2.3.0    | 68 KB     | ############################################################## | 100%
markupsafe-2.1.1     | 22 KB     | ############################################################## | 100%
numpy-base-1.19.2    | 5.3 MB    | ############################################################## | 100%
giflib-5.2.1         | 82 KB     | ############################################################## | 100%
libiconv-1.16        | 1.4 MB    | ############################################################## | 100%
libcusolver-11.4.0.1 | 78.7 MB   | ############################################################## | 100%
networkx-2.8.4       | 2.7 MB    | ############################################################## | 100%
openh264-2.1.1       | 1.5 MB    | ############################################################## | 100%
libtiff-4.2.0        | 579 KB    | ############################################################## | 100%
cuda-cudart-11.7.99  | 194 KB    | ############################################################## | 100%
cuda-cupti-11.7.101  | 22.9 MB   | ############################################################## | 100%
typing_extensions-4. | 54 KB     | ############################################################## | 100%
pytorch-mutex-1.0    | 3 KB      | ############################################################## | 100%
jinja2-3.1.2         | 207 KB    | ############################################################## | 100%
freetype-2.11.0      | 943 KB    | ############################################################## | 100%
libpng-1.6.37        | 364 KB    | ############################################################## | 100%
cuda-nvtx-11.7.91    | 57 KB     | ############################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# conda install pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia

---------

After above installation, I got following error:

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log
/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/scipy/__init__.py:143: UserWarning: A NumPy version >=1.19.5 and <1.27.0 is required for this version of SciPy (detected version 1.19.2)
  warnings.warn(f"A NumPy version >={np_minversion} and <{np_maxversion}"
Traceback (most recent call last):
  File "train.py", line 13, in <module>
    from model import Tacotron2
  File "/home/ye/exp/tts/tacotron2/model.py", line 6, in <module>
    from layers import ConvNorm, LinearNorm
  File "/home/ye/exp/tts/tacotron2/layers.py", line 2, in <module>
    from librosa.filters import mel as librosa_mel_fn
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/librosa/filters.py", line 52, in <module>
    from numba import jit
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/numba/__init__.py", line 55, in <module>
    _ensure_critical_deps()
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/numba/__init__.py", line 40, in _ensure_critical_deps
    raise ImportError(msg)
ImportError: Numba needs NumPy 1.21 or greater. Got NumPy 1.19.

real    0m0.910s
user    0m1.353s
sys     0m2.108s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

---------

For the above error, I installed numpy with conda as follows:  


The following packages will be UPDATED:

    intel-openmp: 2020.2-254            --> 2021.4.0-h06a4308_3561
    mkl:          2020.2-256            --> 2021.4.0-h06a4308_640
    mkl-service:  2.3.0-py38he904b0f_0  --> 2.4.0-py38h7f8727e_0
    mkl_fft:      1.3.0-py38h54f3939_0  --> 1.3.1-py38hd3c417c_0
    mkl_random:   1.1.1-py38h0573a6f_0  --> 1.2.2-py38h51133e4_0
    numpy:        1.19.2-py38h54aff64_0 --> 1.22.3-py38he7a7128_0
    numpy-base:   1.19.2-py38hfa32c7d_0 --> 1.22.3-py38hf524024_0

Proceed ([y]/n)? y


Downloading and Extracting Packages
mkl_random-1.2.2     | 341 KB    | ############################################################## | 100%
intel-openmp-2021.4. | 8.8 MB    | ############################################################## | 100%
numpy-1.22.3         | 10 KB     | ############################################################## | 100%
mkl_fft-1.3.1        | 200 KB    | ############################################################## | 100%
mkl-2021.4.0         | 219.1 MB  | ############################################################## | 100%
numpy-base-1.22.3    | 6.8 MB    | ############################################################## | 100%
mkl-service-2.4.0    | 62 KB     | ############################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# conda install numpy

------------

After I installed numpy as above, when I tried to train again and I got following error:  

"../note.txt" 555L, 31456B written
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log
Traceback (most recent call last):
  File "train.py", line 14, in <module>
    from data_utils import TextMelLoader, TextMelCollate
  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 8, in <module>
    from text import text_to_sequence
  File "/home/ye/exp/tts/tacotron2/text/__init__.py", line 3, in <module>
    from text import cleaners
  File "/home/ye/exp/tts/tacotron2/text/cleaners.py", line 17, in <module>
    from .numbers import normalize_numbers
  File "/home/ye/exp/tts/tacotron2/text/numbers.py", line 3, in <module>
    import inflect
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/inflect/__init__.py", line 77, in <module>
    from pydantic.typing import Annotated
ImportError: cannot import name 'Annotated' from 'pydantic.typing' (/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/pydantic/typing.py)

real    0m1.269s
user    0m1.676s
sys     0m2.145s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log

------------

For the above error, I uninstall inflect with following command:

pip uninstall inflect

Then, I did installation with inflect as follows:  

  environment location: /root/anaconda3/envs/tacotron2

  added / updated specs:
    - inflect


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    inflect-5.3.0              |   py38h06a4308_1          59 KB

The following NEW packages will be INSTALLED:

    inflect: 5.3.0-py38h06a4308_1

Proceed ([y]/n)? y


Downloading and Extracting Packages
inflect-5.3.0        | 59 KB     | ############################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# conda install inflect

--------------

After I installed all the required Python library packages, run training and got following errors:

    from tensorflow.python.distribute.failure_handling import failure_handling_util
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/tensorflow/python/distribute/failure_handling/failure_handling_util.py", line 19, in <module>
    import requests
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/requests/__init__.py", line 45, in <module>
    from .exceptions import RequestsDependencyWarning
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/requests/exceptions.py", line 9, in <module>
    from .compat import JSONDecodeError as CompatJSONDecodeError
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/requests/compat.py", line 13, in <module>
    import charset_normalizer as chardet
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/charset_normalizer/__init__.py", line 23, in <module>
    from charset_normalizer.api import from_fp, from_path, from_bytes, normalize
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/charset_normalizer/api.py", line 10, in <module>
    from charset_normalizer.md import mess_ratio
AttributeError: partially initialized module 'charset_normalizer' has no attribute 'md__mypyc' (most likely due to a circular import)

real    0m2.065s
user    0m2.429s
sys     0m2.182s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log

-----------

For the above error, I tried to solve with followings:

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# pip install --force-reinstall charset-normalizer==3.1.0
Collecting charset-normalizer==3.1.0
  Using cached charset_normalizer-3.1.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (195 kB)
Installing collected packages: charset-normalizer
  Attempting uninstall: charset-normalizer
    Found existing installation: charset-normalizer 2.0.4
    Uninstalling charset-normalizer-2.0.4:
      Successfully uninstalled charset-normalizer-2.0.4
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
aiohttp 3.8.1 requires charset-normalizer<3.0,>=2.0, but you have charset-normalizer 3.1.0 which is incompatible.
Successfully installed charset-normalizer-3.1.0
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

------------


(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log
2023-07-01 19:34:41.834082: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2023-07-01 19:34:41.857042: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-07-01 19:34:42.173095: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
Traceback (most recent call last):
  File "train.py", line 278, in <module>
    hparams = create_hparams(args.hparams)
  File "/home/ye/exp/tts/tacotron2/hparams.py", line 8, in create_hparams
    hparams = tf.contrib.training.HParams(
AttributeError: module 'tensorflow' has no attribute 'contrib'

real    0m2.350s
user    0m2.713s
sys     0m2.188s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

-----------

For the above error, I tried to solve with following command:  

pip install tensorflow_probability==0.17.0

-----------

With the above command I still got ... tensorflow has no attribute 'contrib' ERROR ...

Try to solve with following command:  


pip install tensorflow_probability==0.12.2

-------------

I faced this error for several minutes ...  

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log
2023-07-01 19:50:27.031016: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2023-07-01 19:50:27.053666: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-07-01 19:50:27.367862: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
Traceback (most recent call last):
  File "train.py", line 278, in <module>
    hparams = create_hparams(args.hparams)
  File "/home/ye/exp/tts/tacotron2/hparams.py", line 8, in create_hparams
    hparams = tf.contrib.training.HParams(
AttributeError: module 'tensorflow' has no attribute 'contrib'

real    0m2.317s
user    0m2.649s
sys     0m2.219s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

----------

Solution for the above ERROR:  


I updated the hparams.py file as follows:   


  1 import tensorflow as tf
  2 from text import symbols
  3
  4
  5 def create_hparams(hparams_string=None, verbose=False):
  6     """Create model hyperparameters. Parse nondefault from given string."""
  7
  8     hparams = tf.contrib.training.HParams(
  
  
      #hparams = tf.contrib.training.HParams(
    hparams = tf.compat.v1.estimator.training.HParams(

------------

After I updated the above hparams.py file, I got the following new error:  

2023-07-01 19:57:52.885551: I tensorflow/core/util/port.cc:110] oneDNN custom operations are on. You may see slightly different numerical results due to floating-point round-off errors from different computation orders. To turn them off, set the environment variable `TF_ENABLE_ONEDNN_OPTS=0`.
2023-07-01 19:57:52.908263: I tensorflow/core/platform/cpu_feature_guard.cc:182] This TensorFlow binary is optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-07-01 19:57:53.223187: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
Traceback (most recent call last):
  File "train.py", line 278, in <module>
    hparams = create_hparams(args.hparams)
  File "/home/ye/exp/tts/tacotron2/hparams.py", line 9, in create_hparams
    hparams = tf.compat.v1.estimator.training.HParams(
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/tensorflow/python/util/lazy_loader.py", line 59, in __getattr__
    return getattr(module, item)
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/tensorflow/python/util/module_wrapper.py", line 232, in _getattr
    attr = getattr(self._tfmw_wrapped_module, name)
AttributeError: module 'tensorflow_estimator.python.estimator.api._v1.estimator' has no attribute 'training'

real    0m2.365s
user    0m2.705s
sys     0m2.211s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

-------------

Downloading and Extracting Packages
astor-0.8.1          | 45 KB     | ############################################################## | 100%
cudatoolkit-10.1.243 | 513.2 MB  | ############################################################## | 100%
google-pasta-0.2.0   | 43 KB     | ############################################################## | 100%
termcolor-2.1.0      | 11 KB     | ############################################################## | 100%
keras-preprocessing- | 35 KB     | ############################################################## | 100%
gast-0.4.0           | 12 KB     | ############################################################## | 100%
scipy-1.6.2          | 20.2 MB   | ############################################################## | 100%
wrapt-1.13.3         | 52 KB     | ############################################################## | 100%
opt_einsum-3.3.0     | 57 KB     | ############################################################## | 100%
tensorflow-base-2.4. | 424.1 MB  | ############################################################## | 100%
cudnn-7.6.5          | 250.6 MB  | ############################################################## | 100%
cupti-10.1.168       | 1.7 MB    | ############################################################## | 100%
python-flatbuffers-2 | 31 KB     | ############################################################## | 100%
astunparse-1.6.3     | 17 KB     | ############################################################## | 100%
tensorflow-estimator | 288 KB    | ############################################################## | 100%
h5py-2.10.0          | 1.1 MB    | ############################################################## | 100%
hdf5-1.10.6          | 4.8 MB    | ############################################################## | 100%
tensorflow-gpu-2.4.1 | 2 KB      | ############################################################## | 100%
tensorflow-2.4.1     | 3 KB      | ############################################################## | 100%
_tflow_select-2.1.0  | 2 KB      | ############################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# conda install tensorflow-gpu

------------

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# pip install tensorflow==2.12.*

-------------

Solution:

https://github.com/NVIDIA/tacotron2/issues/278


I need to change the hparams.py with following file:

class AttrDict(dict):
    def __init__(self, *args, **kwargs):
        super(AttrDict, self).__init__(*args, **kwargs)
        self.__dict__ = self


def create_hparams(hparams_string=None, verbose=False):
    """Create model hyperparameters. Parse nondefault from given string."""

    hparams = AttrDict({
        ################################
        # Experiment Parameters        #
        ################################
        "epochs":1500,
        "iters_per_checkpoint":1000,
        "seed":1234,
        "dynamic_loss_scaling":True,
        "fp16_run":False,
        "distributed_run":False,
        "dist_backend":"nccl",
        "dist_url":"tcp://localhost:14897",
        "cudnn_enabled":True,
        "cudnn_benchmark":False,
        "ignore_layers":['embedding.weight'],
        # freeze_layers":['encoder'], # Freeze tacotron2 layer for finetuning

        ################################
        # Data Parameters             #
        ################################
        "load_mel_from_disk":False,
        "load_phone_from_disk":True,

        "training_files":'',
        "validation_files":'',

        "text_cleaners":['english_cleaners'],

        ################################
        # Audio Parameters             #
        ################################
        "max_wav_value":32768.0,
        "sampling_rate":22050,
        "filter_length":1024,
        "hop_length":256,
        "win_length":1024,
        "n_mel_channels":80,
        "mel_fmin":0.0,
        "mel_fmax":8000.0,

        ################################
        # Model Parameters             #
        ################################
        "n_symbols": 313,
        "symbols_embedding_dim":512,
        "alignloss": "L2",
        "attention": "StepwiseMonotonicAttention",

        # Encoder parameters
        "encoder_kernel_size":5,
        "encoder_n_convolutions":3,
        "encoder_embedding_dim":512,

        # Decoder parameters
        "n_frames_per_step":1,  # currently only 1 is supported
        "decoder_rnn_dim":1024,
        "prenet_dim":256,
        "max_decoder_steps":1000,
        "gate_threshold":0.001,
        "p_attention_dropout":0.1,
        "p_decoder_dropout":0.1,

        # Attention parameters
        "attention_rnn_dim":1024,
        "attention_dim":128,

        # Location Layer parameters
        "attention_location_n_filters":32,
        "attention_location_kernel_size":31,

        # Mel-post processing network parameters
        "postnet_embedding_dim":512,
        "postnet_kernel_size":5,
        "postnet_n_convolutions":5,

        ################################
        # Optimization Hyperparameters #
        ################################
        "use_saved_learning_rate":True,
        "learning_rate":1e-3,
        "weight_decay":1e-6,
        "grad_clip_thresh":1.0,
        "batch_size":32, # each gpus
        "mask_padding":True  # set model's padded outputs to padded values
    })

    if hparams_string:
        hps = hparams_string[1:-2].split("-")
        for hp in hps:
            k,v = hp.split(":")
            if k in hparams:
                hparams[k] = v
                print("Set hparam: " + k + " to " + v)

    return hparams

-----------

And inside the train.py file, I need to update as follows:  

parser.add_argument('--hparams', type=str)
hparams = create_hparams(args.hparams)

---------------

Hey! I got new error! :)

  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/nn/modules/module.py", line 905, in cuda
    return self._apply(lambda t: t.cuda(device))
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/nn/modules/module.py", line 797, in _apply
    module._apply(fn)
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/nn/modules/module.py", line 820, in _apply
    param_applied = fn(param)
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/nn/modules/module.py", line 905, in <lambda>
    return self._apply(lambda t: t.cuda(device))
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/cuda/__init__.py", line 239, in _lazy_init
    raise AssertionError("Torch not compiled with CUDA enabled")
AssertionError: Torch not compiled with CUDA enabled

real    0m2.379s
user    0m2.165s
sys     0m0.212s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

-------------

s optimized to use available CPU instructions in performance-critical operations.
To enable the following instructions: AVX2 AVX_VNNI FMA, in other operations, rebuild TensorFlow with the appropriate compiler flags.
2023-07-01 21:44:43.365408: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
FP16 Run: False
Dynamic Loss Scaling: True
Distributed Run: False
cuDNN Enabled: True
cuDNN Benchmark: False
Traceback (most recent call last):
  File "train.py", line 290, in <module>
    train(args.output_directory, args.log_directory, args.checkpoint_path,
  File "train.py", line 186, in train
    train_loader, valset, collate_fn = prepare_dataloaders(hparams)
  File "train.py", line 44, in prepare_dataloaders
    trainset = TextMelLoader(hparams.training_files, hparams)
  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 18, in __init__
    self.audiopaths_and_text = load_filepaths_and_text(audiopaths_and_text)
  File "/home/ye/exp/tts/tacotron2/utils.py", line 19, in load_filepaths_and_text
    with open(filename, encoding='utf-8') as f:
FileNotFoundError: [Errno 2] No such file or directory: ''

real    0m3.232s
user    0m3.288s
sys     0m2.880s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

-------------

2023-07-01 21:51:42.537003: W tensorflow/compiler/tf2tensorrt/utils/py_utils.cc:38] TF-TRT Warning: Could not find TensorRT
FP16 Run: False
Dynamic Loss Scaling: True
Distributed Run: False
cuDNN Enabled: True
cuDNN Benchmark: False
Traceback (most recent call last):
  File "train.py", line 290, in <module>
    train(args.output_directory, args.log_directory, args.checkpoint_path,
  File "train.py", line 186, in train
    train_loader, valset, collate_fn = prepare_dataloaders(hparams)
  File "train.py", line 44, in prepare_dataloaders
    trainset = TextMelLoader(hparams.training_files, hparams)
  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 23, in __init__
    self.stft = layers.TacotronSTFT(
  File "/home/ye/exp/tts/tacotron2/layers.py", line 49, in __init__
    self.stft_fn = STFT(filter_length, hop_length, win_length)
  File "/home/ye/exp/tts/tacotron2/stft.py", line 67, in __init__
    fft_window = pad_center(fft_window, filter_length)
TypeError: pad_center() takes 1 positional argument but 2 were given

real    0m3.478s
user    0m5.381s
sys     0m7.207s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log

----------

I also checked the library: 

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# vi /root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/librosa/util/utils.py

def pad_center(
    data: np.ndarray, *, size: int, axis: int = -1, **kwargs: Any
) -> np.ndarray:
    """Pad an array to a target length along a target axis.

    This differs from `np.pad` by centering the data prior to padding,
    analogous to `str.center`

    Examples
    --------
    >>> # Generate a vector
	
---------

For that pad_center error, the solution is I need to install the lower version of the librosa as follows:

pip install librosa==0.9.2

---------

Now, I can run, However, I got a new error as follows:

  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 39, in get_mel
    audio, sampling_rate = load_wav_to_torch(filename)
  File "/home/ye/exp/tts/tacotron2/utils.py", line 14, in load_wav_to_torch
    sampling_rate, data = read(full_path)
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/scipy/io/wavfile.py", line 647, in read
    fid = open(filename, 'rb')
FileNotFoundError: [Errno 2] No such file or directory: '/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7447_8963294415.wav'


real    0m3.731s
user    0m8.629s
sys     0m9.446s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log

----------

Yes, when I tried to find that file, I couldn't find it as follows:  

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# ls /home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7447_8963294415.wav
ls: cannot access '/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7447_8963294415.wav': No such file or directory
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2#

---------

I found the Error, all the filename inside the index file is given with "bur", actual filename are given with "my" :)

==> openslr80_test.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7447_7747402294.wav|အောင်မြင်နနဲ့ လုပ်ငန်း တစ်ခု ကကို ရှိလာနနိုင်မှာ ဖြစ်တယ် လလိလို့ မခခိုင်လွင်ခြူး က ပြောပါတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_3187293861.wav|ဖုန်း နနဲ့တော့ အလှအပလေးတွေ ရရိုက်ဖြစ်ပါတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_1311639034.wav|ကုန်းပွဲ ဆဆိုတာက သံဃာတော်တွေ ကကို ဆွမ်း လောင်းလှူ ပြီး ဇာတ်သဘင်တွေ နနဲ့ ကျင်းပတာပါ

==> openslr80_train.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_7865_1250917969.wav|ပြီးတော့ တရုတ် နနဲ့လည်း ချစ်ကြည်ရင်းနှီးတတဲ့ ဆက်ဆံရေး ရှိတယ်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_8698_6883351313.wav|အအဲ့ဒီ ဝေဖန်မှုတွေ နနဲ့ ပတ်သက် လလိလို့ ဘယ်လလို တတုတုံ့ပြန်ချင်ပါသလဲ
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_3260_8853590661.wav|မမီ မွေးဖွားနေတတဲ့ အချိန် မှာတော့ ဘုရား ဂုဏ်တော် ကကိုပဲ တောက်လျှောက် ရွတ်နေခခဲ့ပါတယ်

==> openslr80_val.txt <==
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_5903_5153800262.wav|ယခု လတ်တလော တွင် အာရှ စိမ်းလန်းမှု ွံ့ဖြြိုးရေး ဘဏ် လီမိတက် ၏ ငွေအပ်နှံသူများ ကြား ဂယက် ရရိုက်ခတ်မှုများ ရှိနေသည်
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_6118_4929981963.wav|မြြိြို့လယ်ခေါင် ကတ္တရာ လမ်းမကြီး ပေါ် ဗြစ် ဆ                                                                                                ဆိ                                                                                                       ဆို                                                                                                      ဆိုပြီး ဒီအတတိုင်း ထွေးချလလိုက်တာ ပါ
/home/ye/exp/speech_data/MyanmarSpeech/wavs/bur_4632_8001334672.wav|ဒီ ပစ္စည်းလေး တစ်ခု ထဲ မှာ သက်ဝင်နေတဲ့ မေတ္တာတရားတွေ က အများကြီး ပဲ
(tacotron2) root@500e9f8181d8:/home/ye/exp/speech_data/MyanmarSpeech# head -n 3 *.txt

--------

Actual filenames are as follows:

my_4632_9495500399.wav  my_5903_9369989352.wav  my_7712_3368744988.wav  my_9762_8707374487.wav
my_4632_9522852394.wav  my_5903_9375761703.wav  my_7712_3392078386.wav  my_9762_8795987377.wav
my_4632_9542462968.wav  my_5903_9417118955.wav  my_7712_3418589576.wav  my_9762_9405098622.wav
my_4632_9565802903.wav  my_5903_9436547514.wav  my_7712_3446032073.wav  my_9762_9422349053.wav
my_4632_9717931743.wav  my_5903_9443761519.wav  my_7712_3460582233.wav  my_9762_9780826656.wav
my_4632_9855570937.wav  my_5903_9447519791.wav  my_7712_3469400326.wav  my_9762_9943594974.wav
my_5189_0063084676.wav  my_5903_9449006158.wav  my_7712_3549314186.wav
my_5189_0099616035.wav  my_5903_9464622753.wav  my_7712_3554231345.wav

-----------

I makde search and replace with sed command:

(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# cat ../../speech_data/MyanmarSpeech/search_replace.sh
#!/bin/bash

sed -i 's/bur_/my_/g' openslr80_test.txt
sed -i 's/bur_/my_/g' openslr80_train.txt
sed -i 's/bur_/my_/g' openslr80_val.txt

-----------

After finishing search and replace and train again, I got a following new error message:

  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/_utils.py", line 644, in reraise
    raise exception
IndexError: Caught IndexError in DataLoader worker process 0.
Original Traceback (most recent call last):
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/utils/data/_utils/worker.py", line 308, in _worker_loop
    data = fetcher.fetch(index)
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/utils/data/_utils/fetch.py", line 51, in fetch
    data = [self.dataset[idx] for idx in possibly_batched_index]
  File "/root/anaconda3/envs/tacotron2/lib/python3.8/site-packages/torch/utils/data/_utils/fetch.py", line 51, in <listcomp>
    data = [self.dataset[idx] for idx in possibly_batched_index]
  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 61, in __getitem__
    return self.get_mel_text_pair(self.audiopaths_and_text[index])
  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 34, in get_mel_text_pair
    mel = self.get_mel(audiopath)
  File "/home/ye/exp/tts/tacotron2/data_utils.py", line 41, in get_mel
    raise ValueError("{} {} SR doesn't match target {} SR".format(
IndexError: Replacement index 2 out of range for positional args tuple


real    0m3.879s
user    0m9.804s
sys     0m10.780s
(tacotron2) root@500e9f8181d8:/home/ye/exp/tts/tacotron2# time python train.py --output_directory=openslr80 --log_directory=openslr80_log

---------

Above error is coming from the data_utils.py and when I checked the code, I found followings:

    def get_mel(self, filename):
        if not self.load_mel_from_disk:
            audio, sampling_rate = load_wav_to_torch(filename)
            if sampling_rate != self.stft.sampling_rate:
                raise ValueError("{} {} SR doesn't match target {} SR".format(
                    sampling_rate, self.stft.sampling_rate))
            audio_norm = audio / self.max_wav_value
            audio_norm = audio_norm.unsqueeze(0)
            audio_norm = torch.autograd.Variable(audio_norm, requires_grad=False)
            melspec = self.stft.mel_spectrogram(audio_norm)
            melspec = torch.squeeze(melspec, 0)
        else:
		
--------------

When I checked the Sampling rate of the OpenSLR-80 data, I found as follows:

Input File     : 'my_0366_0045318711.wav'
Channels       : 1
Sample Rate    : 48000
Precision      : 16-bit
Duration       : 00:00:05.38 = 258048 samples ~ 403.2 CDDA sectors
File Size      : 516k
Bit Rate       : 768k
Sample Encoding: 16-bit Signed Integer PCM


Input File     : 'my_0366_0096392289.wav'
Channels       : 1
Sample Rate    : 48000
Precision      : 16-bit
Duration       : 00:00:04.10 = 196608 samples ~ 307.2 CDDA sectors
File Size      : 393k
Bit Rate       : 768k
Sample Encoding: 16-bit Signed Integer PCM

--------------------



## Reference

1. https://github.com/NVIDIA/tacotron2/issues/321  
2. https://tts.readthedocs.io/en/latest/models/tacotron1-2.html
3. https://keithito.com/LJ-Speech-Dataset/  

Quick Start:  

[https://github.com/keithito/tacotron](https://github.com/keithito/tacotron)  

Paper:  

TACOTRON: TOWARDS END-TO-END SPEECH SYNTHESIS:  
[https://arxiv.org/pdf/1703.10135.pdf](https://arxiv.org/pdf/1703.10135.pdf)  

Tacotron2:  
[1712.05884.pdf](https://arxiv.org/pdf/1712.05884.pdf)

For tts testing reference:  

1. https://tts.readthedocs.io/en/latest/inference.html#synthesizing-speech
2. https://tts.readthedocs.io/en/latest/tutorial_for_nervous_beginners.html
3. https://tts.readthedocs.io/en/latest/faq.html
4. https://github.com/r9y9/tacotron_pytorch/blob/master/notebooks/Test%20Tacotron.ipynb
5. https://medium.com/nectec/tacotron2-thai-tts-b5d26a015465
6. https://colab.research.google.com/gist/sayakmisra/2bf6e72fb9eed2f8cfb2fb47143726b6/-e2e-tts.ipynb#scrollTo=3lMJyJcLCsd4

Waveglow downloaded link:

https://drive.google.com/u/0/uc?id=1rpK8CzAAirq9sWZhe9nlfvxMF1dRgFbF&export=download


