# Haggingface Exp for myPOEM Generation

ဒေါက်တာတန်းကျောင်းသူ ခိုင်ဆုဝေ (Okayama Prefecture Univ., Japan) က ပြင်ပေးထားတဲ့ မြန်မာကဗျာဒေတာကို သုံးပြီး LM generation experiment လုပ်ဖို့အတွက် ပြင်စဉ်က log ဖိုင်ပါ။  

## Create a New Conda Env

```
(base) ye@:/media/ye/project2/exp/myPoem$ conda info --envs
# conda environments:
#
base                  *  /home/ye/anaconda3
NCRF++                   /home/ye/anaconda3/envs/NCRF++
NeMo                     /home/ye/anaconda3/envs/NeMo
align-linguistic         /home/ye/anaconda3/envs/align-linguistic
bilingual-emb            /home/ye/anaconda3/envs/bilingual-emb
joey                     /home/ye/anaconda3/envs/joey
multiTask                /home/ye/anaconda3/envs/multiTask
paraphrase1              /home/ye/anaconda3/envs/paraphrase1
paraphrase2              /home/ye/anaconda3/envs/paraphrase2
postedit                 /home/ye/anaconda3/envs/postedit
py2.7env                 /home/ye/anaconda3/envs/py2.7env
py3.6env                 /home/ye/anaconda3/envs/py3.6env
py3.9env                 /home/ye/anaconda3/envs/py3.9env
rl-joey                  /home/ye/anaconda3/envs/rl-joey
simple-nmt               /home/ye/anaconda3/envs/simple-nmt
```

```
(base) ye@:/media/ye/project2/exp/myPoem$ conda create -n haggingface python
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##

  environment location: /home/ye/anaconda3/envs/haggingface

  added / updated specs:
    - python


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2022.3.29  |       h06a4308_0         117 KB
    openssl-1.1.1n             |       h7f8727e_0         2.5 MB
    python-3.10.4              |       h12debd9_0        24.2 MB
    setuptools-61.2.0          |  py310h06a4308_0        1019 KB
    sqlite-3.38.2              |       hc218d9a_0         1.0 MB
    tzdata-2022a               |       hda174b7_0         109 KB
    zlib-1.2.12                |       h7f8727e_1         111 KB
    ------------------------------------------------------------
                                           Total:        29.0 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-4.5-1_gnu
  bzip2              pkgs/main/linux-64::bzip2-1.0.8-h7b6447c_0
  ca-certificates    pkgs/main/linux-64::ca-certificates-2022.3.29-h06a4308_0
  certifi            pkgs/main/noarch::certifi-2020.6.20-pyhd3eb1b0_3
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.35.1-h7274673_9
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.3.0-h5101ec6_17
  libgomp            pkgs/main/linux-64::libgomp-9.3.0-h5101ec6_17
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.3.0-hd4cf53a_17
  libuuid            pkgs/main/linux-64::libuuid-1.0.3-h7f8727e_2
  ncurses            pkgs/main/linux-64::ncurses-6.3-h7f8727e_2
  openssl            pkgs/main/linux-64::openssl-1.1.1n-h7f8727e_0
  pip                pkgs/main/linux-64::pip-21.2.4-py310h06a4308_0
  python             pkgs/main/linux-64::python-3.10.4-h12debd9_0
  readline           pkgs/main/linux-64::readline-8.1.2-h7f8727e_1
  setuptools         pkgs/main/linux-64::setuptools-61.2.0-py310h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.38.2-hc218d9a_0
  tk                 pkgs/main/linux-64::tk-8.6.11-h1ccaba5_0
  tzdata             pkgs/main/noarch::tzdata-2022a-hda174b7_0
  wheel              pkgs/main/noarch::wheel-0.37.1-pyhd3eb1b0_0
  xz                 pkgs/main/linux-64::xz-5.2.5-h7b6447c_0
  zlib               pkgs/main/linux-64::zlib-1.2.12-h7f8727e_1


Proceed ([y]/n)? y


Downloading and Extracting Packages
setuptools-61.2.0    | 1019 KB   | ############################################################################################################# | 100% 
sqlite-3.38.2        | 1.0 MB    | ############################################################################################################# | 100% 
zlib-1.2.12          | 111 KB    | ############################################################################################################# | 100% 
openssl-1.1.1n       | 2.5 MB    | ############################################################################################################# | 100% 
tzdata-2022a         | 109 KB    | ############################################################################################################# | 100% 
python-3.10.4        | 24.2 MB   | ############################################################################################################# | 100% 
ca-certificates-2022 | 117 KB    | ############################################################################################################# | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate haggingface
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@:/media/ye/project2/exp/myPoem$ conda activate haggingface
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

အသစ်ဆောက်ထားတဲ့ conda environment ထဲကို ဝင်မယ်...  

```
(base) ye@:/media/ye/project2/exp/myPoem$ conda activate haggingface
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

## Transformers Installation

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ pip install transformers
Collecting transformers
  Downloading transformers-4.18.0-py3-none-any.whl (4.0 MB)
     |████████████████████████████████| 4.0 MB 1.9 MB/s 
Collecting tqdm>=4.27
  Downloading tqdm-4.64.0-py2.py3-none-any.whl (78 kB)
     |████████████████████████████████| 78 kB 7.0 MB/s 
Collecting numpy>=1.17
  Downloading numpy-1.22.3-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (16.8 MB)
     |████████████████████████████████| 16.8 MB 42.7 MB/s 
Collecting requests
  Using cached requests-2.27.1-py2.py3-none-any.whl (63 kB)
Collecting sacremoses
  Downloading sacremoses-0.0.49-py3-none-any.whl (895 kB)
     |████████████████████████████████| 895 kB 98.8 MB/s 
Collecting huggingface-hub<1.0,>=0.1.0
  Downloading huggingface_hub-0.5.1-py3-none-any.whl (77 kB)
     |████████████████████████████████| 77 kB 8.7 MB/s 
Collecting pyyaml>=5.1
  Downloading PyYAML-6.0-cp310-cp310-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_12_x86_64.manylinux2010_x86_64.whl (682 kB)
     |████████████████████████████████| 682 kB 101.3 MB/s 
Collecting filelock
  Downloading filelock-3.6.0-py3-none-any.whl (10.0 kB)
Collecting regex!=2019.12.17
  Downloading regex-2022.3.15-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (763 kB)
     |████████████████████████████████| 763 kB 25.9 MB/s 
Collecting tokenizers!=0.11.3,<0.13,>=0.11.1
  Downloading tokenizers-0.12.1-cp310-cp310-manylinux_2_12_x86_64.manylinux2010_x86_64.whl (6.6 MB)
     |████████████████████████████████| 6.6 MB 26.9 MB/s 
Collecting packaging>=20.0
  Using cached packaging-21.3-py3-none-any.whl (40 kB)
Collecting typing-extensions>=3.7.4.3
  Downloading typing_extensions-4.2.0-py3-none-any.whl (24 kB)
Collecting pyparsing!=3.0.5,>=2.0.2
  Downloading pyparsing-3.0.8-py3-none-any.whl (98 kB)
     |████████████████████████████████| 98 kB 8.9 MB/s 
Collecting urllib3<1.27,>=1.21.1
  Downloading urllib3-1.26.9-py2.py3-none-any.whl (138 kB)
     |████████████████████████████████| 138 kB 32.8 MB/s 
Collecting idna<4,>=2.5
  Using cached idna-3.3-py3-none-any.whl (61 kB)
Collecting charset-normalizer~=2.0.0
  Using cached charset_normalizer-2.0.12-py3-none-any.whl (39 kB)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests->transformers) (2020.6.20)
Collecting joblib
  Using cached joblib-1.1.0-py2.py3-none-any.whl (306 kB)
Collecting six
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Collecting click
  Downloading click-8.1.2-py3-none-any.whl (96 kB)
     |████████████████████████████████| 96 kB 6.5 MB/s 
Installing collected packages: urllib3, pyparsing, idna, charset-normalizer, typing-extensions, tqdm, six, requests, regex, pyyaml, packaging, joblib, filelock, click, tokenizers, sacremoses, numpy, huggingface-hub, transformers
Successfully installed charset-normalizer-2.0.12 click-8.1.2 filelock-3.6.0 huggingface-hub-0.5.1 idna-3.3 joblib-1.1.0 numpy-1.22.3 packaging-21.3 pyparsing-3.0.8 pyyaml-6.0 regex-2022.3.15 requests-2.27.1 sacremoses-0.0.49 six-1.16.0 tokenizers-0.12.1 tqdm-4.64.0 transformers-4.18.0 typing-extensions-4.2.0 urllib3-1.26.9
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

## pytest Installation

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ pip install pytest
Collecting pytest
  Downloading pytest-7.1.1-py3-none-any.whl (297 kB)
     |████████████████████████████████| 297 kB 1.9 MB/s 
Collecting py>=1.8.2
  Downloading py-1.11.0-py2.py3-none-any.whl (98 kB)
     |████████████████████████████████| 98 kB 9.3 MB/s 
Collecting pluggy<2.0,>=0.12
  Downloading pluggy-1.0.0-py2.py3-none-any.whl (13 kB)
Collecting attrs>=19.2.0
  Downloading attrs-21.4.0-py2.py3-none-any.whl (60 kB)
     |████████████████████████████████| 60 kB 8.4 MB/s 
Requirement already satisfied: packaging in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from pytest) (21.3)
Collecting iniconfig
  Using cached iniconfig-1.1.1-py2.py3-none-any.whl (5.0 kB)
Collecting tomli>=1.0.0
  Downloading tomli-2.0.1-py3-none-any.whl (12 kB)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from packaging->pytest) (3.0.8)
Installing collected packages: tomli, py, pluggy, iniconfig, attrs, pytest
Successfully installed attrs-21.4.0 iniconfig-1.1.1 pluggy-1.0.0 py-1.11.0 pytest-7.1.1 tomli-2.0.1
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

## Check Transformers Path

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ python -c "import transformers as _; print(_.__path__)"
None of PyTorch, TensorFlow >= 2.0, or Flax have been found. Models won't be available and only tokenizers, configuration and file/data utilities can be used.
['/home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages/transformers']
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ ls /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages/transformers
activations.py                                  feature_extraction_utils.py        modeling_flax_outputs.py        sagemaker
activations_tf.py                               file_utils.py                      modeling_flax_pytorch_utils.py  testing_utils.py
benchmark                                       generation_beam_constraints.py     modeling_flax_utils.py          tf_utils.py
commands                                        generation_beam_search.py          modeling_outputs.py             tokenization_utils_base.py
configuration_utils.py                          generation_flax_logits_process.py  modeling_tf_outputs.py          tokenization_utils_fast.py
convert_graph_to_onnx.py                        generation_flax_utils.py           modeling_tf_pytorch_utils.py    tokenization_utils.py
convert_pytorch_checkpoint_to_tf2.py            generation_logits_process.py       modeling_tf_utils.py            trainer_callback.py
convert_slow_tokenizer.py                       generation_stopping_criteria.py    modeling_utils.py               trainer_pt_utils.py
convert_slow_tokenizers_checkpoints_to_fast.py  generation_tf_logits_process.py    models                          trainer.py
convert_tf_hub_seq_to_seq_bert_to_pytorch.py    generation_tf_utils.py             onnx                            trainer_seq2seq.py
data                                            generation_utils.py                optimization.py                 trainer_tf.py
debug_utils.py                                  hf_argparser.py                    optimization_tf.py              trainer_utils.py
deepspeed.py                                    image_utils.py                     pipelines                       training_args.py
dependency_versions_check.py                    __init__.py                        processing_utils.py             training_args_seq2seq.py
dependency_versions_table.py                    integrations.py                    __pycache__                     training_args_tf.py
dynamic_module_utils.py                         keras_callbacks.py                 pytorch_utils.py                utils
feature_extraction_sequence_utils.py            modelcard.py                       py.typed
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ ls /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages/transformers/models/
albert            byt5                  distilbert       hubert       mbart50        prophetnet              speech_to_text            visual_bert
auto              camembert             dit              ibert        megatron_bert  __pycache__             speech_to_text_2          vit
bart              canine                dpr              imagegpt     megatron_gpt2  qdqbert                 splinter                  vit_mae
barthez           clip                  dpt              __init__.py  mluke          rag                     squeezebert               wav2vec2
bartpho           convbert              electra          layoutlm     mmbt           realm                   swin                      wav2vec2_phoneme
beit              convnext              encoder_decoder  layoutlmv2   mobilebert     reformer                t5                        wav2vec2_with_lm
bert              cpm                   flaubert         layoutxlm    mpnet          rembert                 tapas                     wavlm
bert_generation   ctrl                  fnet             led          mt5            resnet                  transfo_xl                xglm
bert_japanese     data2vec              fsmt             longformer   nystromformer  retribert               trocr                     xlm
bertweet          deberta               funnel           luke         openai         roberta                 unispeech                 xlm_prophetnet
big_bird          deberta_v2            glpn             lxmert       pegasus        roformer                unispeech_sat             xlm_roberta
bigbird_pegasus   decision_transformer  gpt2             m2m_100      perceiver      segformer               van                       xlm_roberta_xl
blenderbot        deit                  gptj             marian       phobert        sew                     vilt                      xlnet
blenderbot_small  detr                  gpt_neo          maskformer   plbart         sew_d                   vision_encoder_decoder    yoso
bort              dialogpt              herbert          mbart        poolformer     speech_encoder_decoder  vision_text_dual_encoder
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ pip install spacy ftfy==4.4.3
Collecting spacy
  Downloading spacy-3.2.4-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (6.1 MB)
     |████████████████████████████████| 6.1 MB 1.9 MB/s 
Collecting ftfy==4.4.3
  Downloading ftfy-4.4.3.tar.gz (50 kB)
     |████████████████████████████████| 50 kB 7.3 MB/s 
Collecting html5lib
  Downloading html5lib-1.1-py2.py3-none-any.whl (112 kB)
     |████████████████████████████████| 112 kB 148.5 MB/s 
Collecting wcwidth
  Using cached wcwidth-0.2.5-py2.py3-none-any.whl (30 kB)
Collecting langcodes<4.0.0,>=3.2.0
  Downloading langcodes-3.3.0-py3-none-any.whl (181 kB)
     |████████████████████████████████| 181 kB 163.0 MB/s 
Collecting thinc<8.1.0,>=8.0.12
  Downloading thinc-8.0.15-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (663 kB)
     |████████████████████████████████| 663 kB 129.5 MB/s 
Collecting pydantic!=1.8,!=1.8.1,<1.9.0,>=1.7.4
  Downloading pydantic-1.8.2-py3-none-any.whl (126 kB)
     |████████████████████████████████| 126 kB 29.5 MB/s 
Collecting srsly<3.0.0,>=2.4.1
  Downloading srsly-2.4.3-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (457 kB)
     |████████████████████████████████| 457 kB 129.9 MB/s 
Collecting typer<0.5.0,>=0.3.0
  Downloading typer-0.4.1-py3-none-any.whl (27 kB)
Collecting wasabi<1.1.0,>=0.8.1
  Downloading wasabi-0.9.1-py3-none-any.whl (26 kB)
Collecting spacy-loggers<2.0.0,>=1.0.0
  Downloading spacy_loggers-1.0.2-py3-none-any.whl (7.2 kB)
Collecting blis<0.8.0,>=0.4.0
  Downloading blis-0.7.7-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (9.9 MB)
     |████████████████████████████████| 9.9 MB 2.7 MB/s 
Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy) (4.64.0)
Collecting cymem<2.1.0,>=2.0.2
  Downloading cymem-2.0.6-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (35 kB)
Requirement already satisfied: packaging>=20.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy) (21.3)
Collecting catalogue<2.1.0,>=2.0.6
  Downloading catalogue-2.0.7-py3-none-any.whl (17 kB)
Collecting jinja2
  Downloading Jinja2-3.1.1-py3-none-any.whl (132 kB)
     |████████████████████████████████| 132 kB 30.6 MB/s 
Requirement already satisfied: numpy>=1.15.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy) (1.22.3)
Collecting click<8.1.0
  Using cached click-8.0.4-py3-none-any.whl (97 kB)
Collecting pathy>=0.3.5
  Downloading pathy-0.6.1-py3-none-any.whl (42 kB)
     |████████████████████████████████| 42 kB 1.6 MB/s 
Collecting spacy-legacy<3.1.0,>=3.0.8
  Downloading spacy_legacy-3.0.9-py2.py3-none-any.whl (20 kB)
Requirement already satisfied: requests<3.0.0,>=2.13.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy) (2.27.1)
Collecting murmurhash<1.1.0,>=0.28.0
  Downloading murmurhash-1.0.6-cp310-cp310-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (21 kB)
Collecting preshed<3.1.0,>=3.0.2
  Downloading preshed-3.0.6-cp310-cp310-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (128 kB)
     |████████████████████████████████| 128 kB 30.9 MB/s 
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy) (61.2.0)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from packaging>=20.0->spacy) (3.0.8)
Collecting smart-open<6.0.0,>=5.0.0
  Using cached smart_open-5.2.1-py3-none-any.whl (58 kB)
Requirement already satisfied: typing-extensions>=3.7.4.3 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from pydantic!=1.8,!=1.8.1,<1.9.0,>=1.7.4->spacy) (4.2.0)
Requirement already satisfied: charset-normalizer~=2.0.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2.0.12)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy) (2020.6.20)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy) (1.26.9)
Requirement already satisfied: idna<4,>=2.5 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy) (3.3)
Requirement already satisfied: six>=1.9 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from html5lib->ftfy==4.4.3) (1.16.0)
Collecting webencodings
  Using cached webencodings-0.5.1-py2.py3-none-any.whl (11 kB)
Collecting MarkupSafe>=2.0
  Downloading MarkupSafe-2.1.1-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Building wheels for collected packages: ftfy
  Building wheel for ftfy (setup.py) ... done
  Created wheel for ftfy: filename=ftfy-4.4.3-py3-none-any.whl size=41085 sha256=40bc0268566895f36e4b7a8c38d34dc2a9983b4d41d03d775340faa9006e8b24
  Stored in directory: /home/ye/.cache/pip/wheels/ff/17/af/513573c0a8a561878536d1cd7d8c0c355095f5ac7d0c335305
Successfully built ftfy
Installing collected packages: murmurhash, cymem, click, catalogue, webencodings, wasabi, typer, srsly, smart-open, pydantic, preshed, MarkupSafe, blis, wcwidth, thinc, spacy-loggers, spacy-legacy, pathy, langcodes, jinja2, html5lib, spacy, ftfy
  Attempting uninstall: click
    Found existing installation: click 8.1.2
    Uninstalling click-8.1.2:
      Successfully uninstalled click-8.1.2
Successfully installed MarkupSafe-2.1.1 blis-0.7.7 catalogue-2.0.7 click-8.0.4 cymem-2.0.6 ftfy-4.4.3 html5lib-1.1 jinja2-3.1.1 langcodes-3.3.0 murmurhash-1.0.6 pathy-0.6.1 preshed-3.0.6 pydantic-1.8.2 smart-open-5.2.1 spacy-3.2.4 spacy-legacy-3.0.9 spacy-loggers-1.0.2 srsly-2.4.3 thinc-8.0.15 typer-0.4.1 wasabi-0.9.1 wcwidth-0.2.5 webencodings-0.5.1
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ python -m spacy download en
⚠ As of spaCy v3.0, shortcuts like 'en' are deprecated. Please use the
full pipeline package name 'en_core_web_sm' instead.
Collecting en-core-web-sm==3.2.0
  Downloading https://github.com/explosion/spacy-models/releases/download/en_core_web_sm-3.2.0/en_core_web_sm-3.2.0-py3-none-any.whl (13.9 MB)
     |████████████████████████████████| 13.9 MB 1.1 MB/s 
Requirement already satisfied: spacy<3.3.0,>=3.2.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from en-core-web-sm==3.2.0) (3.2.4)
Requirement already satisfied: spacy-legacy<3.1.0,>=3.0.8 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (3.0.9)
Requirement already satisfied: thinc<8.1.0,>=8.0.12 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (8.0.15)
Requirement already satisfied: spacy-loggers<2.0.0,>=1.0.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (1.0.2)
Requirement already satisfied: pydantic!=1.8,!=1.8.1,<1.9.0,>=1.7.4 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (1.8.2)
Requirement already satisfied: packaging>=20.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (21.3)
Requirement already satisfied: murmurhash<1.1.0,>=0.28.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (1.0.6)
Requirement already satisfied: setuptools in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (61.2.0)
Requirement already satisfied: preshed<3.1.0,>=3.0.2 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (3.0.6)
Requirement already satisfied: tqdm<5.0.0,>=4.38.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (4.64.0)
Requirement already satisfied: catalogue<2.1.0,>=2.0.6 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (2.0.7)
Requirement already satisfied: cymem<2.1.0,>=2.0.2 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (2.0.6)
Requirement already satisfied: langcodes<4.0.0,>=3.2.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (3.3.0)
Requirement already satisfied: blis<0.8.0,>=0.4.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (0.7.7)
Requirement already satisfied: typer<0.5.0,>=0.3.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (0.4.1)
Requirement already satisfied: click<8.1.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (8.0.4)
Requirement already satisfied: requests<3.0.0,>=2.13.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (2.27.1)
Requirement already satisfied: srsly<3.0.0,>=2.4.1 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (2.4.3)
Requirement already satisfied: pathy>=0.3.5 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (0.6.1)
Requirement already satisfied: jinja2 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (3.1.1)
Requirement already satisfied: wasabi<1.1.0,>=0.8.1 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (0.9.1)
Requirement already satisfied: numpy>=1.15.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (1.22.3)
Requirement already satisfied: pyparsing!=3.0.5,>=2.0.2 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from packaging>=20.0->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (3.0.8)
Requirement already satisfied: smart-open<6.0.0,>=5.0.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from pathy>=0.3.5->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (5.2.1)
Requirement already satisfied: typing-extensions>=3.7.4.3 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from pydantic!=1.8,!=1.8.1,<1.9.0,>=1.7.4->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (4.2.0)
Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (1.26.9)
Requirement already satisfied: idna<4,>=2.5 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (3.3)
Requirement already satisfied: charset-normalizer~=2.0.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (2.0.12)
Requirement already satisfied: certifi>=2017.4.17 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from requests<3.0.0,>=2.13.0->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (2020.6.20)
Requirement already satisfied: MarkupSafe>=2.0 in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from jinja2->spacy<3.3.0,>=3.2.0->en-core-web-sm==3.2.0) (2.1.1)
Installing collected packages: en-core-web-sm
Successfully installed en-core-web-sm-3.2.0
✔ Download and installation successful
You can now load the package via spacy.load('en_core_web_sm')
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

## Pytorch Installation

``
(haggingface) ye@:/media/ye/project2/exp/myPoem$ python ./bert-eg1.py 
Traceback (most recent call last):
  File "/media/ye/project2/exp/myPoem/./bert-eg1.py", line 1, in <module>
    import torch
ModuleNotFoundError: No module named 'torch'
```

pytorch ကို လက်ရှိ enviroment မှာ installation လုပ်ဖို့ လိုအပ်တယ်။  

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ pip install torch
Collecting torch
  Downloading torch-1.11.0-cp310-cp310-manylinux1_x86_64.whl (750.6 MB)
     |████████████████████████████████| 750.6 MB 9.5 kB/s 
Requirement already satisfied: typing-extensions in /home/ye/anaconda3/envs/haggingface/lib/python3.10/site-packages (from torch) (4.2.0)
Installing collected packages: torch
Successfully installed torch-1.11.0
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

test run လုပ်ကြည့်ခဲ့...  

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ python ./bert-eg1.py 
Downloading: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████| 226k/226k [00:01<00:00, 225kB/s]
Downloading: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████| 28.0/28.0 [00:00<00:00, 13.6kB/s]
Downloading: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 570/570 [00:00<00:00, 274kB/s]
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

လိုအပ်တာတွေ download လုပ်ပြီး အဆင်ပြေပြေနဲ့ run သွားတဲ့ ပုံရှိတယ်။ output တွေကို ပြဖို့ မရေးထားလို့ ဝင်ရေးလိုက်တယ်။  

```python
(haggingface) ye@:/media/ye/project2/exp/myPoem$ cat ./bert-eg1.py 
import torch
from transformers import BertTokenizer, BertModel, BertForMaskedLM

# OPTIONAL: if you want to have more information on what's happening under the hood, activate the logger as follows
import logging
logging.basicConfig(level=logging.INFO)

# Load pre-trained model tokenizer (vocabulary)
tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')

# Tokenize input
text = "[CLS] Who was Jim Henson ? [SEP] Jim Henson was a puppeteer [SEP]"
tokenized_text = tokenizer.tokenize(text)
print("input text: ", text)
print("tokenized text: ", tokenized_text)

# Mask a token that we will try to predict back with `BertForMaskedLM`
masked_index = 8
tokenized_text[masked_index] = '[MASK]'
assert tokenized_text == ['[CLS]', 'who', 'was', 'jim', 'henson', '?', '[SEP]', 'jim', '[MASK]', 'was', 'a', 'puppet', '##eer', '[SEP]']
print("masked tokenized_text: ", tokenized_text)

# Convert token to vocabulary indices
indexed_tokens = tokenizer.convert_tokens_to_ids(tokenized_text)
print("indexed_tokens: ", indexed_tokens)

# Define sentence A and B indices associated to 1st and 2nd sentences (see paper)
segments_ids = [0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1]

# Convert inputs to PyTorch tensors
tokens_tensor = torch.tensor([indexed_tokens])
segments_tensors = torch.tensor([segments_ids])

print("tokens_tensor: ", tokens_tensor)
print("segments_tensors: ", segments_tensors)

(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

နောက်တစ်ခေါက် ထပ် run ကြည့်ခဲ့တယ်။  

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ python ./bert-eg1.py 
input text:  [CLS] Who was Jim Henson ? [SEP] Jim Henson was a puppeteer [SEP]
tokenized text:  ['[CLS]', 'who', 'was', 'jim', 'henson', '?', '[SEP]', 'jim', 'henson', 'was', 'a', 'puppet', '##eer', '[SEP]']
masked tokenized_text:  ['[CLS]', 'who', 'was', 'jim', 'henson', '?', '[SEP]', 'jim', '[MASK]', 'was', 'a', 'puppet', '##eer', '[SEP]']
indexed_tokens:  [101, 2040, 2001, 3958, 27227, 1029, 102, 3958, 103, 2001, 1037, 13997, 11510, 102]
tokens_tensor:  tensor([[  101,  2040,  2001,  3958, 27227,  1029,   102,  3958,   103,  2001,
          1037, 13997, 11510,   102]])
segments_tensors:  tensor([[0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1]])
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

bert-eg1.py ပရိုဂရမ်မှာ ဆက်ပြထားတဲ့ example အပိုင်းကို ထပ်ဖြည့်လိုက်တယ်။  

```python
(haggingface) ye@:/media/ye/project2/exp/myPoem$ cat ./bert-eg1.py 
import torch
from transformers import BertTokenizer, BertModel, BertForMaskedLM

# OPTIONAL: if you want to have more information on what's happening under the hood, activate the logger as follows
import logging
logging.basicConfig(level=logging.INFO)

# Load pre-trained model tokenizer (vocabulary)
tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')

# Tokenize input
text = "[CLS] Who was Jim Henson ? [SEP] Jim Henson was a puppeteer [SEP]"
tokenized_text = tokenizer.tokenize(text)
print("input text: ", text)
print("tokenized text: ", tokenized_text)

# Mask a token that we will try to predict back with `BertForMaskedLM`
masked_index = 8
tokenized_text[masked_index] = '[MASK]'
assert tokenized_text == ['[CLS]', 'who', 'was', 'jim', 'henson', '?', '[SEP]', 'jim', '[MASK]', 'was', 'a', 'puppet', '##eer', '[SEP]']
print("masked tokenized_text: ", tokenized_text)

# Convert token to vocabulary indices
indexed_tokens = tokenizer.convert_tokens_to_ids(tokenized_text)
print("indexed_tokens: ", indexed_tokens)

# Define sentence A and B indices associated to 1st and 2nd sentences (see paper)
segments_ids = [0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1]

# Convert inputs to PyTorch tensors
tokens_tensor = torch.tensor([indexed_tokens])
segments_tensors = torch.tensor([segments_ids])

print("tokens_tensor: ", tokens_tensor)
print("segments_tensors: ", segments_tensors)

# Load pre-trained model (weights)
model = BertModel.from_pretrained('bert-base-uncased')

# Set the model in evaluation mode to desactivate the DropOut modules
# This is IMPORTANT to have reproductible results during evaluation!
model.eval()

# If you have a GPU, put everything on cuda
tokens_tensor = tokens_tensor.to('cuda')
segments_tensors = segments_tensors.to('cuda')
model.to('cuda')

# Predict hidden states features for each layer
with torch.no_grad():
    # See the models docstrings for the detail of the inputs
    outputs = model(tokens_tensor, token_type_ids=segments_tensors)
    # Transformers models always output tuples.
    # See the models docstrings for the detail of all the outputs
    # In our case, the first element is the hidden state of the last layer of the Bert model
    encoded_layers = outputs[0]
# We have encoded our input sequence in a FloatTensor of shape (batch size, sequence length, model hidden dimension)
assert tuple(encoded_layers.shape) == (1, len(indexed_tokens), model.config.hidden_size)

# Load pre-trained model (weights)
model = BertForMaskedLM.from_pretrained('bert-base-uncased')
print(model.eval())

# If you have a GPU, put everything on cuda
tokens_tensor = tokens_tensor.to('cuda')
segments_tensors = segments_tensors.to('cuda')
model.to('cuda')

print("tokens_tensor: ", tokens_tensor)
print("segments_tensors: ", segments_tensors)

# Predict all tokens
with torch.no_grad():
    outputs = model(tokens_tensor, token_type_ids=segments_tensors)
    predictions = outputs[0]

# confirm we were able to predict 'henson'
predicted_index = torch.argmax(predictions[0, masked_index]).item()
predicted_token = tokenizer.convert_ids_to_tokens([predicted_index])[0]
assert predicted_token == 'henson'

print("predicted_index: ", predicted_index)
print("predicted_token :", predicted_token)
```

updated python ပရိုဂရမ်ကို run ကြည့်တော့ အောက်ပါအတိုင်း output ပေတယ်။  

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ python ./bert-eg1.py 
input text:  [CLS] Who was Jim Henson ? [SEP] Jim Henson was a puppeteer [SEP]
tokenized text:  ['[CLS]', 'who', 'was', 'jim', 'henson', '?', '[SEP]', 'jim', 'henson', 'was', 'a', 'puppet', '##eer', '[SEP]']
masked tokenized_text:  ['[CLS]', 'who', 'was', 'jim', 'henson', '?', '[SEP]', 'jim', '[MASK]', 'was', 'a', 'puppet', '##eer', '[SEP]']
indexed_tokens:  [101, 2040, 2001, 3958, 27227, 1029, 102, 3958, 103, 2001, 1037, 13997, 11510, 102]
tokens_tensor:  tensor([[  101,  2040,  2001,  3958, 27227,  1029,   102,  3958,   103,  2001,
          1037, 13997, 11510,   102]])
segments_tensors:  tensor([[0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1]])
Downloading: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████| 420M/420M [00:07<00:00, 57.4MB/s]
Some weights of the model checkpoint at bert-base-uncased were not used when initializing BertModel: ['cls.predictions.bias', 'cls.predictions.transform.LayerNorm.weight', 'cls.predictions.transform.LayerNorm.bias', 'cls.predictions.transform.dense.bias', 'cls.predictions.decoder.weight', 'cls.predictions.transform.dense.weight', 'cls.seq_relationship.bias', 'cls.seq_relationship.weight']
- This IS expected if you are initializing BertModel from the checkpoint of a model trained on another task or with another architecture (e.g. initializing a BertForSequenceClassification model from a BertForPreTraining model).
- This IS NOT expected if you are initializing BertModel from the checkpoint of a model that you expect to be exactly identical (initializing a BertForSequenceClassification model from a BertForSequenceClassification model).
Some weights of the model checkpoint at bert-base-uncased were not used when initializing BertForMaskedLM: ['cls.seq_relationship.weight', 'cls.seq_relationship.bias']
- This IS expected if you are initializing BertForMaskedLM from the checkpoint of a model trained on another task or with another architecture (e.g. initializing a BertForSequenceClassification model from a BertForPreTraining model).
- This IS NOT expected if you are initializing BertForMaskedLM from the checkpoint of a model that you expect to be exactly identical (initializing a BertForSequenceClassification model from a BertForSequenceClassification model).
BertForMaskedLM(
  (bert): BertModel(
    (embeddings): BertEmbeddings(
      (word_embeddings): Embedding(30522, 768, padding_idx=0)
      (position_embeddings): Embedding(512, 768)
      (token_type_embeddings): Embedding(2, 768)
      (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
      (dropout): Dropout(p=0.1, inplace=False)
    )
    (encoder): BertEncoder(
      (layer): ModuleList(
        (0): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (1): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (2): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (3): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (4): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (5): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (6): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (7): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (8): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (9): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (10): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
        (11): BertLayer(
          (attention): BertAttention(
            (self): BertSelfAttention(
              (query): Linear(in_features=768, out_features=768, bias=True)
              (key): Linear(in_features=768, out_features=768, bias=True)
              (value): Linear(in_features=768, out_features=768, bias=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
            (output): BertSelfOutput(
              (dense): Linear(in_features=768, out_features=768, bias=True)
              (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
              (dropout): Dropout(p=0.1, inplace=False)
            )
          )
          (intermediate): BertIntermediate(
            (dense): Linear(in_features=768, out_features=3072, bias=True)
            (intermediate_act_fn): GELUActivation()
          )
          (output): BertOutput(
            (dense): Linear(in_features=3072, out_features=768, bias=True)
            (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
            (dropout): Dropout(p=0.1, inplace=False)
          )
        )
      )
    )
  )
  (cls): BertOnlyMLMHead(
    (predictions): BertLMPredictionHead(
      (transform): BertPredictionHeadTransform(
        (dense): Linear(in_features=768, out_features=768, bias=True)
        (transform_act_fn): GELUActivation()
        (LayerNorm): LayerNorm((768,), eps=1e-12, elementwise_affine=True)
      )
      (decoder): Linear(in_features=768, out_features=30522, bias=True)
    )
  )
)
tokens_tensor:  tensor([[  101,  2040,  2001,  3958, 27227,  1029,   102,  3958,   103,  2001,
          1037, 13997, 11510,   102]], device='cuda:0')
segments_tensors:  tensor([[0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1]], device='cuda:0')
predicted_index:  27227
predicted_token : henson
(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

## Testing OpenAI GPT-2

OpenAI GPT-2 အပိုင်းကိုလည်း ကိုယ့်စက်ထဲမှာ ဆက်စမ်းကြည့်ခဲ့တယ်။  
print line တွေထပ်ဖြည့်ထားတဲ့ python ပရိုဂရမ်က အောက်ပါအတိုင်း...  

```python
(haggingface) ye@:/media/ye/project2/exp/myPoem$ cat gpt2tokenizer.py 
import torch
from transformers import GPT2Tokenizer, GPT2LMHeadModel

# OPTIONAL: if you want to have more information on what's happening, activate the logger as follows
import logging
logging.basicConfig(level=logging.INFO)

# Load pre-trained model tokenizer (vocabulary)
tokenizer = GPT2Tokenizer.from_pretrained('gpt2')

# Encode a text inputs
text = "Who was Jim Henson ? Jim Henson was a"
indexed_tokens = tokenizer.encode(text)

print("text: ", text)
print("indexed_tokens: ", indexed_tokens)

# Convert indexed tokens in a PyTorch tensor
tokens_tensor = torch.tensor([indexed_tokens])
print("tokens_tensor: ", tokens_tensor) 

# Load pre-trained model (weights)
model = GPT2LMHeadModel.from_pretrained('gpt2')

# Set the model in evaluation mode to desactivate the DropOut modules
# This is IMPORTANT to have reproductible results during evaluation!
model.eval()

print("model.eval(): ", model.eval())

# If you have a GPU, put everything on cuda
tokens_tensor = tokens_tensor.to('cuda')
model.to('cuda')

# Predict all tokens
with torch.no_grad():
    outputs = model(tokens_tensor)
    predictions = outputs[0]

# get the predicted next sub-word (in our case, the word 'man')
predicted_index = torch.argmax(predictions[0, -1, :]).item()
predicted_text = tokenizer.decode(indexed_tokens + [predicted_index])
assert predicted_text == 'Who was Jim Henson? Jim Henson was a man'

print("predicted_index: ", predicted_index)
print("predicted_text: ", predicted_text)

(haggingface) ye@:/media/ye/project2/exp/myPoem$
```

အောက်ပါအတိုင်း run ခဲ့တယ်။  

```
(haggingface) ye@:/media/ye/project2/exp/myPoem$ python gpt2tokenizer.py 
Downloading: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████| 0.99M/0.99M [00:01<00:00, 661kB/s]
Downloading: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████| 446k/446k [00:01<00:00, 362kB/s]
Downloading: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 665/665 [00:00<00:00, 320kB/s]
text:  Who was Jim Henson ? Jim Henson was a
indexed_tokens:  [8241, 373, 5395, 367, 19069, 5633, 5395, 367, 19069, 373, 257]
tokens_tensor:  tensor([[ 8241,   373,  5395,   367, 19069,  5633,  5395,   367, 19069,   373,
           257]])
Downloading: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████| 523M/523M [00:10<00:00, 51.5MB/s]
model.eval():  GPT2LMHeadModel(
  (transformer): GPT2Model(
    (wte): Embedding(50257, 768)
    (wpe): Embedding(1024, 768)
    (drop): Dropout(p=0.1, inplace=False)
    (h): ModuleList(
      (0): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (1): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (2): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (3): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (4): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (5): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (6): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (7): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (8): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (9): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (10): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
      (11): GPT2Block(
        (ln_1): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (attn): GPT2Attention(
          (c_attn): Conv1D()
          (c_proj): Conv1D()
          (attn_dropout): Dropout(p=0.1, inplace=False)
          (resid_dropout): Dropout(p=0.1, inplace=False)
        )
        (ln_2): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
        (mlp): GPT2MLP(
          (c_fc): Conv1D()
          (c_proj): Conv1D()
          (act): NewGELUActivation()
          (dropout): Dropout(p=0.1, inplace=False)
        )
      )
    )
    (ln_f): LayerNorm((768,), eps=1e-05, elementwise_affine=True)
  )
  (lm_head): Linear(in_features=768, out_features=50257, bias=False)
)
predicted_index:  582
predicted_text:  Who was Jim Henson? Jim Henson was a man
(haggingface) ye@:/media/ye/project2/exp/myPoem$ 
```

အဆင်ပြေပြေနဲ့ predict လုပ်ပေးသွားတာကို တွေ့ရတယ်။  

## Pretrained Model for Our Experiment

[https://huggingface.co/transformers/v2.0.0/pretrained_models.html](https://huggingface.co/transformers/v2.0.0/pretrained_models.html) link မှာ ရှင်းပြထားတဲ့ မော်ဒယ်တွေကို ဝင်ကြည့်တော့ မြန်မာစာအတွက် အသုံးဝင်နိုင်မယ့် မော်ဒယ် နှစ်ခုကို အောက်ပါအတိုင်း တွေ့ခဲ့ရ...  


| Architecture | Shortcut Names | Details of the Model |
|:------------|:------------|:--------------|
| BERT | bert-base-multilingual-uncased | (Original, not recommended) 12-layer, 768-hidden, 12-heads, 110M parameters. Trained on lower-cased text in the top 102 languages with the largest Wikipedias. |
| BERT | bert-base-multilingual-cased | (New, recommended) 12-layer, 768-hidden, 12-heads, 110M parameters. Trained on cased text in the top 104 languages with the largest Wikipedias. |

အထက်ပါ မော်ဒယ်နှစ်ခုနဲ့ ပတ်သက်ပြီး အသေးစိတ်က [https://github.com/google-research/bert/blob/master/multilingual.md](https://github.com/google-research/bert/blob/master/multilingual.md) link မှာ ရှာဖတ်ပါ။ အဲဒီ link မှာ recommend လုပ်ထားတဲ့ Multilingual Cased (New) ကိုပဲ သုံးကြည့်ဖို့ ဆုံးဖြတ်ခဲ့တယ်။ ဘာကြောင့်လဲ ဆိုတော့ အဲဒီ link မှာ အောက်ပါအတိုင်း ရှင်းပြထားလို့...  

The Multilingual Cased (New) model also fixes normalization issues in many languages, so it is recommended in languages with non-Latin alphabets (and is often better for most languages with Latin alphabets). When using this model, make sure to pass --do_lower_case=false to run_pretraining.py and other scripts.  

အဲဒီ page ရဲ့ အောက်ဆုံးမှာ ရှင်းပြထားတဲ့အတိုင်းဆိုရင် Thai နဲ့ Mongolian ဘာသာစကားတွေအတွက်က ပထမ release လုပ်ခဲ့တဲ့ အော်ရဂျင်နယ် ဗားရှင်းမှာ မပါပဲ (New) ဆိုတဲ့ ဗားရှင်းမှာမှ ပါလာတဲ့ ပုံရှိတယ်။  

## Prepare myPoem Data

အသစ်ထပ်ရိုက်ထားတာလည်း ရှိသေးပေမဲ့ လောလောဆယ် Jan 7 ထိ ဒေတာကိုပဲ သုံးဖို့ ပြင်မယ်။  

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ wc ./myPoem_all.txt 
  59006  108409 4126908 ./myPoem_all.txt
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ head ./myPoem_all.txt 
ကြက်ဖ သာလျှင်
အာရုဏ်ရောင်လှဝင်းဝါကြ၏ 
ဥဩ သာလျှင်
ရာသီနွေလဖူးပွင့်ကြ၏ 
ဖားငယ် သာလျှင်
အာကာမိုးကမိုးရွာကြ၏ 
တက်လူ သာလျှင်
မြန်မာပြည်လှအားသစ်ရ၍
ဇေယျအောင်လံ ထူမည်တည်း 
ဤနေရာတွင်
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ tail ./myPoem_all.txt 
ဥပမာ ကဗျာဘယ်ကလာသလဲ ဆိုတာမျိုး
ဆိုပါတော့ ငါမင်းကို လွမ်းနေတယ်ဆိုတာမျိုး
ကမာ္ဘက သူ့အတိုင်းရိှတယ်
ငါမရယ်ချင်ဘူး
မင်းမရယ်တော့ဘူးလို့ ငါသိတယ်
၆ ဒဿမ ၈ ပဲ
ငလျင်လှုပ်တယ်
ငါပြိုကျတယ်
မင်းကလေးအကောင်းအတိုင်း ရိှနေရဲ့ မဟုတ်လား
ကမာ္ဘကိုက ရူးခဲ့တာပါကွယ်။
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ shuf ./myPoem_all.txt | head
ကောင်းစွာ လုပ်ကျွေး ပြုစုပေး 
မီးလောင်နေတဲ့ 

ဆက်ဆက် ကြည့်နေပါ
အကြိုက်တွေ့လေပဲ
ရွာလယ်ခေါင်မှာ ပျော်တော်ဆက်
ခင်မင်မှုကို လုံးချေလွှင့်ပစ်လိုက်ပါ မိတ်ဆွေ 
သွေးမတိတ်နိုင်တဲ့
ငါ၏ဝလုံးအ သုံးလုံးတို့
မှုန်းချေအပြတ်ရှင်းပစ်စို့လေး
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ shuf ./myPoem_all.txt | tail

သမုဒယပုံပြင်
မင်းလည်းပါသကိုး နေ့များ။
ပြိုပျက်ယိုင်လဲ ဒုက္ခယှဉ်တွဲ
ရေထဲ ပစ်ချနေတယ်
သခင်ခွဲမယ့် ကာလမှာ
ကျဆုံးပေးဆပ်သွားတဲ့ သားမောင်ရှင်အမေတွေအတွက်
တောလုံးပွင့်အန် မြို့ပွင့်လျှံဝေ
နုပျိုဖွံ့ထွားမေ့ချစ်သား
လယ်သမားတို့ ဖွံ့ထွားချမ်းသာ
```

ထုံးစံအတိုင်း မြန်စာဒေတာမှာက စာလုံးပေါင်းအမှား၊ typing order အမှားနဲ့ ဇော်ဂျီကနေ Myanmar3 ဖောင့်ကို ပြောင်းတဲ့အခါမှာ ဖြစ်တတ်တဲ့ encoding အမှားတွေရှိနေတယ်။ အချိန်ရသလောက် ဒေတာကို cleaning လုပ်မယ်။  

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ wget https://raw.githubusercontent.com/ye-kyaw-thu/sylbreak/master/perl/sylbreak.pl
--2022-04-20 12:36:55--  https://raw.githubusercontent.com/ye-kyaw-thu/sylbreak/master/perl/sylbreak.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.110.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 2189 (2.1K) [text/plain]
Saving to: ‘sylbreak.pl’

sylbreak.pl                           100%[=========================================================================>]   2.14K  --.-KB/s    in 0s      

2022-04-20 12:36:55 (20.2 MB/s) - ‘sylbreak.pl’ saved [2189/2189]

(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ 
```

အထက်မှာ download လုပ်ထားတဲ့ sylbreak perl script ကို သုံးပြီး syllable ဖြတ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ perl ./sylbreak.pl -i ./myPoem_all.txt -s " " > ./myPoem_all.syl
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ head ./myPoem_all.syl 
 ကြက် ဖ   သာ လျှင်
 အာ ရုဏ် ရောင် လှ ဝင်း ဝါ ကြ ၏  
 ဥ ဩ   သာ လျှင်
 ရာ သီ နွေ လ ဖူး ပွ င့် ကြ ၏  
 ဖား ငယ်   သာ လျှင်
 အာ ကာ မိုး က မိုး ရွာ ကြ ၏  
 တက် လူ   သာ လျှင်
 မြန် မာ ပြည် လှ အား သစ် ရ ၍
 ဇေ ယျ အောင် လံ   ထူ မည် တည်း  
 ဤ နေ ရာ တွင်
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ tail ./myPoem_all.syl 
 ဥ ပ မာ   က ဗျာ ဘယ် က လာ သ လဲ   ဆို တာ မျိုး
 ဆို ပါ တော့   ငါ မင်း ကို   လွမ်း နေ တယ် ဆို တာ မျိုး
 က မာ္ဘ က   သူ့ အ တိုင်း ရိှ တယ်
 ငါ မ ရယ် ချင် ဘူး
 မင်း မ ရယ် တော့ ဘူး လို့   ငါ သိ တယ်
 ၆   ဒ ဿ မ   ၈   ပဲ
 င လျင် လှုပ် တယ်
 ငါ ပြို ကျ တယ်
 မင်း က လေး အ ကောင်း အ တိုင်း   ရိှ နေ ရဲ့   မ ဟုတ် လား
 က မာ္ဘ ကို က   ရူး ခဲ့ တာ ပါ ကွယ် ။
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$
```

space cleaning လည်း လုပ်ရလိမ့်မယ်။ double space တို့ TAB တို့ ပါနေတဲ့ ကိစ္စမျိုးတွေ....  

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ wget https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/clean-space.pl
--2022-04-20 12:43:47--  https://raw.githubusercontent.com/ye-kyaw-thu/tools/master/perl/clean-space.pl
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.110.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 686 [text/plain]
Saving to: ‘clean-space.pl’

clean-space.pl                        100%[=========================================================================>]     686  --.-KB/s    in 0s      

2022-04-20 12:43:48 (97.2 MB/s) - ‘clean-space.pl’ saved [686/686]
```

space တွေကို ရှင်းခဲ့...  

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ perl ./clean-space.pl ./myPoem_all.syl > ./myPoem_all.syl.clean
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ head ./myPoem_all.syl.clean 
ကြက် ဖ သာ လျှင်
အာ ရုဏ် ရောင် လှ ဝင်း ဝါ ကြ ၏
ဥ ဩ သာ လျှင်
ရာ သီ နွေ လ ဖူး ပွ င့် ကြ ၏
ဖား ငယ် သာ လျှင်
အာ ကာ မိုး က မိုး ရွာ ကြ ၏
တက် လူ သာ လျှင်
မြန် မာ ပြည် လှ အား သစ် ရ ၍
ဇေ ယျ အောင် လံ ထူ မည် တည်း
ဤ နေ ရာ တွင်
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ tail ./myPoem_all.syl.clean 
ဥ ပ မာ က ဗျာ ဘယ် က လာ သ လဲ ဆို တာ မျိုး
ဆို ပါ တော့ ငါ မင်း ကို လွမ်း နေ တယ် ဆို တာ မျိုး
က မာ္ဘ က သူ့ အ တိုင်း ရိှ တယ်
ငါ မ ရယ် ချင် ဘူး
မင်း မ ရယ် တော့ ဘူး လို့ ငါ သိ တယ်
၆ ဒ ဿ မ ၈ ပဲ
င လျင် လှုပ် တယ်
ငါ ပြို ကျ တယ်
မင်း က လေး အ ကောင်း အ တိုင်း ရိှ နေ ရဲ့ မ ဟုတ် လား
က မာ္ဘ ကို က ရူး ခဲ့ တာ ပါ ကွယ် ။
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ shuf ./myPoem_all.syl.clean | head
အစ္စ က ရာ သည် မ ယိမ်း မ ယိုင် အ စမ်း သပ် ခံ သံ ခဲ တင် ခံ
စု ဖွဲ့ ပေး လတ် ရေး သတ် မှတ် ၏
ဖဲ ကြိုး နီ နီ လေး ကို
အ နန္တော တည့် သွား ရော ဂါ ဘက်
လွန် ပါ ရော
တိမ် ရောင် စုံ ကွက် မ ကန်း
တိုင်း ဧ ရာ ဝယ် သာ ပေါင်း မြို့ နယ်
ရယ် သံ လေး တွေ ကို အ စ အ ဆုံး ကြိုး သီ လို့ သူ့ မှာ
မ ချစ် သူ နှင့် အ တူ သာ
လျှောက် နိုင် ခဲ့ ပြီး လား
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ shuf ./myPoem_all.syl.clean | tail
ပြည် ရွာ ကောင်း မှု လုပ် အား မှန်
ဝင့် မော် ရွှင် ပျ သု ခု မ ဟု
ဘာ ကို လို လို ဆို ဦး စို့
ကြမ်း တမ်း ဒုက္ခ ခက် ခဲ လှ လည်း
အ သည်း နှ လုံး လေး က တော့
သို့ တ မူ လည်း နွဲ့ လျ ကြည်း ကား
ဖြေ မ ဆည် ဇာတ် စုံ ကျင်း သော် ကြော င့်
ဘယ် ဇာတ် တော် လေ မှန်း သိ
ချမ်း ချမ်း ဖွေး ဖွေး ပါ ပဲ
ရွှေ ခဲ တို့ နောင် ဝိဇ္ဇာ မောင် သည်
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$
```

ကဗျာဒေတာဖိုင်ထဲကနေ syllable list ကို ဆွဲထုတ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ time cat ./myPoem_all.syl.clean | sed "s/ /\n/g;" | sort | uniq > ./myPoem_all.uniq

real	0m8.966s
user	0m8.988s
sys	0m0.037s
```

ဆွဲထုတ်ပြီး ရလာတဲ့ syllable တွေ (တကယ်ကတော့ မြန်မာစာမှာက အင်္ဂလိပ်စာလုံးတွေ၊ သင်္ကေတတွေကိုလည်း ထည့်ရေးကြလို့ အင်္ဂလိပ်စာလုံးတွေနဲ့ "!" တို့ "," စတာတွေလည်း ပါ) ကို အကြမ်းစစ်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ head ./myPoem_all.uniq 



!
"
#
'
(
)
*
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ tail ./myPoem_all.uniq 



န်း
ေ
တ
တံ
တာ

၍့်
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ shuf ./myPoem_all.uniq | head -30
ထိမ်း
မှီ
ငွား
ဗုံ
လျှိုး
ခေါန်း
ဖြင့်
ရှောင်း
ကစ္ဆ
ချန့်
ချည်း
လျမ်း
ဒေါ်
လှာ
ဖြူး
ဆေး
ခါ
ဌေး
ချိန်
ခစ်
မေတ္တ
ဂျို
ရှောင်
အော့
ပြူး
တိုင်း
ပွက်
သတ္တာ
ဗြန်
တင်း
```

```
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$ shuf ./myPoem_all.uniq | head -30
တံ့
တန်
မျှော်
သဗ္ဗ
အူ
ချိုင်း​
ကျေ
ယက္ကန်း
သာဒ်
ရမ်
လှိ
ပြန့်
ရှူး
ဟန်
အတ္တုပ္ပ
ပျိူ
ဆယ်
တြာ
ညေ
မြန်
F
ဥတ္တ
ဖြိုင်
ထိ
ဝတ္တုံ
ကြူး
စူး
ကျောင်း
ရှော့ခ်
သမ္မာ
(base) ye@:/media/ye/project2/data/my-poem/khaing-hus-wai/ye-edit-20apr2022/syl-chk$
```

တကယ်က မမြင်ရတဲ့စာလုံးတွေ (invisible character) လည်း list ထဲမှာ ပါလာတတ်ပါတယ်။  


## Reference

- https://huggingface.co/transformers/v2.0.0/quickstart.html
- https://huggingface.co/transformers/v2.0.0/pretrained_models.html



