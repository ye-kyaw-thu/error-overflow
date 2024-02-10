# LMs for myNLP

At first, fasttext LM for similarity measurements ...  

## Preparing LM Conda Env

```
(base) yekyaw.thu@gpu:~/exp$ conda create --name LM python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/LM

  added / updated specs:
    - python=3.8


The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  _openmp_mutex      pkgs/main/linux-64::_openmp_mutex-5.1-1_gnu
  ca-certificates    pkgs/main/linux-64::ca-certificates-2023.12.12-h06a4308_0
  ld_impl_linux-64   pkgs/main/linux-64::ld_impl_linux-64-2.38-h1181459_1
  libffi             pkgs/main/linux-64::libffi-3.4.4-h6a678d5_0
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-11.2.0-h1234567_1
  libgomp            pkgs/main/linux-64::libgomp-11.2.0-h1234567_1
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-11.2.0-h1234567_1
  ncurses            pkgs/main/linux-64::ncurses-6.4-h6a678d5_0
  openssl            pkgs/main/linux-64::openssl-3.0.13-h7f8727e_0
  pip                pkgs/main/linux-64::pip-23.3.1-py38h06a4308_0
  python             pkgs/main/linux-64::python-3.8.18-h955ad1f_0
  readline           pkgs/main/linux-64::readline-8.2-h5eee18b_0
  setuptools         pkgs/main/linux-64::setuptools-68.2.2-py38h06a4308_0
  sqlite             pkgs/main/linux-64::sqlite-3.41.2-h5eee18b_0
  tk                 pkgs/main/linux-64::tk-8.6.12-h1ccaba5_0
  wheel              pkgs/main/linux-64::wheel-0.41.2-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.5-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate LM
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

```
(base) yekyaw.thu@gpu:~/exp$ conda activate LM
(LM) yekyaw.thu@gpu:~/exp$
```

## FastText Installation

pip install fasttext က g++ မရှိဘူးဆိုတဲ့ error ပေးတယ်။ ငါ ဒီ server မှာ sudo right လည်းမရှိတော့ conda နဲ့ ပြောင်းပြီး fasttext ကို install လုပ်ကြည့်ခဲ့တယ်။   

```
(LM) yekyaw.thu@gpu:~/exp$ conda install -c conda-forge fasttext
Collecting package metadata (current_repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - defaults/linux-64::openssl==3.0.13=h7f8727e_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/LM

  added / updated specs:
    - fasttext


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2024.2.2   |       hbcca054_0         152 KB  conda-forge
    fasttext-0.9.2             |   py38h43d8883_4         465 KB  conda-forge
    libblas-3.9.0              |15_linux64_openblas          12 KB  conda-forge
    libcblas-3.9.0             |15_linux64_openblas          12 KB  conda-forge
    libgfortran-ng-13.2.0      |       h69a702a_0          23 KB  conda-forge
    libgfortran5-13.2.0        |       ha4646dd_0         1.4 MB  conda-forge
    liblapack-3.9.0            |15_linux64_openblas          12 KB  conda-forge
    libopenblas-0.3.20         |pthreads_h78a6416_0        10.1 MB  conda-forge
    numpy-1.22.3               |   py38h99721a1_2         6.8 MB  conda-forge
    pybind11-2.6.1             |   py38h82cb98a_0         220 KB  conda-forge
    python_abi-3.8             |           2_cp38           4 KB  conda-forge
    ------------------------------------------------------------
                                           Total:        19.1 MB

The following NEW packages will be INSTALLED:

  fasttext           conda-forge/linux-64::fasttext-0.9.2-py38h43d8883_4
  libblas            conda-forge/linux-64::libblas-3.9.0-15_linux64_openblas
  libcblas           conda-forge/linux-64::libcblas-3.9.0-15_linux64_openblas
  libgfortran-ng     conda-forge/linux-64::libgfortran-ng-13.2.0-h69a702a_0
  libgfortran5       conda-forge/linux-64::libgfortran5-13.2.0-ha4646dd_0
  liblapack          conda-forge/linux-64::liblapack-3.9.0-15_linux64_openblas
  libopenblas        conda-forge/linux-64::libopenblas-0.3.20-pthreads_h78a6416_0
  numpy              conda-forge/linux-64::numpy-1.22.3-py38h99721a1_2
  pybind11           conda-forge/linux-64::pybind11-2.6.1-py38h82cb98a_0
  python_abi         conda-forge/linux-64::python_abi-3.8-2_cp38

The following packages will be UPDATED:

  ca-certificates    pkgs/main::ca-certificates-2023.12.12~ --> conda-forge::ca-certificates-2024.2.2-hbcca054_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libopenblas-0.3.20   | 10.1 MB   | ############################################### | 100%
libblas-3.9.0        | 12 KB     | ############################################### | 100%
fasttext-0.9.2       | 465 KB    | ############################################### | 100%
libgfortran-ng-13.2. | 23 KB     | ############################################### | 100%
libgfortran5-13.2.0  | 1.4 MB    | ############################################### | 100%
numpy-1.22.3         | 6.8 MB    | ############################################### | 100%
libcblas-3.9.0       | 12 KB     | ############################################### | 100%
ca-certificates-2024 | 152 KB    | ############################################### | 100%
pybind11-2.6.1       | 220 KB    | ############################################### | 100%
liblapack-3.9.0      | 12 KB     | ############################################### | 100%
python_abi-3.8       | 4 KB      | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(LM) yekyaw.thu@gpu:~/exp$
```

## Import fasttext

```
(LM) yekyaw.thu@gpu:~/exp$ python
Python 3.8.18 (default, Sep 11 2023, 13:40:15)
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import fasttext
>>> print(dir(fasttext))
['BOW', 'EOS', 'EOW', 'FastText', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__path__', '__spec__', 'absolute_import', 'cbow', 'division', 'load_model', 'print_function', 'skipgram', 'supervised', 'tokenize', 'train_supervised', 'train_unsupervised', 'unicode_literals']
>>>
```

## For Testing

The difference between word vector based testing and nearest neighbors based testing primarily lies in the purpose and outcome of each method when analyzing word embeddings or vectors, such as those produced by FastText models.  

### Word Vector Based Testing:

- **Purpose:** Word vector based testing is aimed at understanding the numerical representation (embedding) of a word within the vector space created by the model. It is focused on the specific properties of a single word's vector.
- **Outcome:** The outcome is the vector itself, which is a list of numbers (coordinates in the model's vector space). Each dimension of this vector captures some aspect of the word's meaning or usage based on the training data. This vector can be analyzed to understand the word's positioning in the semantic space relative to other words, but on its own, it provides a more abstract representation.
- **Usage:** These vectors can be used in further NLP tasks such as computing similarity between words, clustering, or as features in machine learning models for tasks like sentiment analysis or document classification.

### Nearest Neighbors Based Testing:

- **Purpose:** Nearest neighbors based testing is aimed at evaluating the semantic relationships captured by the model by finding the closest words (in terms of vector similarity) to a given target word. It's a way to see which words the model considers to be most similar to the target word.
- **Outcome:** The outcome is a list of words along with their similarity scores relative to the target word. This list shows which words are semantically closest to the target word in the model's vector space, effectively illustrating the contextual relationships learned by the model.
- **Usage:** This method is particularly useful for qualitative analysis of a word embedding model. By examining the nearest neighbors of a word, you can assess how well the model captures semantic and syntactic relationships, like synonyms, related concepts, or even analogies.

### Key Differences:

- **Conceptual Focus:** Word vector testing focuses on the representation of individual words in isolation, while nearest neighbors testing focuses on the relationships and contextual similarities between words.
- **Analytical Outcome:** The former provides a direct look at the word's embedding, useful for quantitative analysis or as input to other systems, whereas the latter provides a qualitative measure of the model's ability to capture semantic relationships.
- **Application:** Word vectors are more about leveraging the embedding for further NLP tasks, while nearest neighbors offer a way to validate or explore the semantic understanding encapsulated by the model.

In summary, word vector based testing gives you the raw building blocks of semantic representation, while nearest neighbors based testing shows you how those representations interact within the model's learned semantic space.

## Python Code Development

## Training

```
time python ./fasttext_lm.py train --input ./corpus/myWord_myPOS_myPara.merged.shuf --output ./model/fasttext.5gram.30ep.model --model_type skipgram --min_count 3 --max_ngram 5 --epochs 30

...
...
...
Progress:  98.6% words/sec/thread:   88647 lr:  0.000683 avg.loss:  1.797706 ETA:   0h 0m Progress:  98.7% words/sec/thread:   88647 lr:  0.000633 avg.loss:  1.797646 ETA:   0h 0m Progress:  98.8% words/sec/thread:   88647 lr:  0.000584 avg.loss:  1.797598 ETA:   0h 0m Progress:  98.9% words/sec/thread:   88644 lr:  0.000536 avg.loss:  1.797537 ETA:   0h 0m Progress:  99.0% words/sec/thread:   88640 lr:  0.000489 avg.loss:  1.797388 ETA:   0h 0m Progress:  99.1% words/sec/thread:   88638 lr:  0.000440 avg.loss:  1.797205 ETA:   0h 0m Progress:  99.2% words/sec/thread:   88637 lr:  0.000392 avg.loss:  1.797243 ETA:   0h 0m Progress:  99.3% words/sec/thread:   88635 lr:  0.000343 avg.loss:  1.797133 ETA:   0h 0m Progress:  99.4% words/sec/thread:   88632 lr:  0.000296 avg.loss:  1.796993 ETA:   0h 0m Progress:  99.5% words/sec/thread:   88631 lr:  0.000247 avg.loss:  1.796923 ETA:   0h 0m Progress:  99.6% words/sec/thread:   88630 lr:  0.000198 avg.loss:  1.796849 ETA:   0h 0m Progress:  99.7% words/sec/thread:   88628 lr:  0.000150 avg.loss:  1.796808 ETA:   0h 0m Progress:  99.8% words/sec/thread:   88625 lr:  0.000102 avg.loss:  1.796717 ETA:   0h 0m Progress:  99.9% words/sec/thread:   88622 lr:  0.000054 avg.loss:  1.796693 ETA:   0h 0m Progress: 100.0% words/sec/thread:   88621 lr:  0.000005 avg.loss:  1.796670 ETA:   0h 0m Progress: 100.0% words/sec/thread:   88544 lr: -0.000000 avg.loss:  1.796659 ETA:   0h 0m Progress: 100.0% words/sec/thread:   88544 lr:  0.000000 avg.loss:  1.796659 ETA:   0h 0m 0s

real    1m43.183s
user    37m48.646s
sys     0m5.276s
(LM) yekyaw.thu@gpu:~/exp/lm$
```

## Testing Word Vector

```
(LM) yekyaw.thu@gpu:~/exp/lm$ time python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
> --operation word_vector --word "အိပ်မက်"
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'အိပ်မက်':
[ 0.12031621 -0.52833927  0.48935744  0.06317406 -0.1501954   0.64546204
 -0.15353891  0.01870162  0.61063796  0.6109799   0.73419505  0.65103143
  0.88419914 -0.02869445  0.51289195  0.29153332  0.21679138  0.41199654
  0.16549039  0.10959838 -0.1117438  -0.597564    0.81038356 -0.48549145
  0.4267515   0.3132249  -0.25836775 -0.5588503   0.480795    0.28962284
 -0.12442717  0.04763784  0.03077638  0.30790713 -0.48313704 -0.31243306
 -0.46600592 -0.171712    0.03487121  0.63493305  0.21745388  0.43822077
  0.11850166  0.6815909  -0.2344277  -0.8672393   0.24471918 -0.31629938
 -0.29693434 -0.10546    -0.23418958  0.42033967  0.08946732  0.29462585
 -0.49498886 -0.3409233  -0.8459458  -0.10344138 -0.27136466 -0.32089743
  0.33643812 -0.2371353   0.8248619   0.39421898  0.79225594  0.50261456
 -0.27456722  0.60400057 -0.12840399 -0.19148935 -0.01404916 -0.34982163
 -0.69157416  0.31277627  0.04322456  0.1361411   0.28690267  0.20358531
  0.07332611  0.24729408  0.7870048   0.12728655  0.835099   -0.9541029
  0.39373282  0.07633176 -0.1857064  -0.81001735  0.5948403   0.10527749
 -0.09785659  0.08222029  0.19437683  0.30127054 -0.02300076  0.02820138
 -0.07213072  0.49658784 -0.24521522 -0.2817983 ]

real    0m0.614s
user    0m0.498s
sys     0m1.646s
(LM) yekyaw.thu@gpu:~/exp/lm$
```

## Testing Nearest Neighbors

```
time python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation nearest_neighbors --word "အိပ်မက်" --k 10
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ time python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
> --operation nearest_neighbors --word "အိပ်မက်" --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အိပ်မက်':
Score: 0.8173879981040955, Word: အိပ်မက်မက်
Score: 0.7190538048744202, Word: မက်
Score: 0.7111439108848572, Word: အိပ်မက်ဆိုး
Score: 0.70976722240448, Word: အိပ်မက်လေး
Score: 0.6560232043266296, Word: ကောသလ
Score: 0.5697650909423828, Word: မြင်မက်
Score: 0.5576037764549255, Word: အိမ်မက်
Score: 0.5479919910430908, Word: ည
Score: 0.5243688821792603, Word: အနမ်း
Score: 0.5148499011993408, Word: မြူနှင်း

real    0m0.690s
user    0m0.677s
sys     0m1.635s
(LM) yekyaw.thu@gpu:~/exp/lm$
```

## Some more testing

```
time python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation nearest_neighbors --word "အိပ်မက်" --k 10
```

အောက်ပါ စာလုံးတွေကို ဖိုင်တစ်ဖိုင်တည်းမှာ ထည့်ထားပြီး ...  

```
စိတ္တဇ  
ရည်းစား
အမေ
သာဓု
မုန့်ဟင်းခါး
အင်တာနက်
ရန်ကုန်
ဆီးသွား
ဇာတ်ပို့
တင်္ခဏုပ္ပတ္တိဉာဏ်
```

testing လုပ်ကြည့်ခဲ့တယ်။   

```
(LM) yekyaw.thu@gpu:~/exp/lm$ time python ./run_ftlm_nearest.py --input ./test1.txt --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --k 10
Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word စိတ္တဇ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'စိတ္တဇ':
Score: 0.6274799108505249, Word: စိတ္တ
Score: 0.5660890936851501, Word: စိတ္တဗေဒ
Score: 0.5629989504814148, Word: စိတ္တသုခ
Score: 0.503881573677063, Word: သမစိတ္တ
Score: 0.49321022629737854, Word: ဆောက်ရမ်း
Score: 0.4873538613319397, Word: ကဗျာမဆန်
Score: 0.4854658842086792, Word: ဝတ္ထုရေးဆရာ
Score: 0.48526516556739807, Word: ၂၀:၃၅
Score: 0.4847198724746704, Word: ပင်ကိုယ်
Score: 0.48286300897598267, Word: ထုံပေပေ

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ရည်းစား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ရည်းစား':
Score: 0.8086291551589966, Word: ရည်းစားစာ
Score: 0.747491717338562, Word: ရည်းစားဟောင်း
Score: 0.683797299861908, Word: တောဂေါ်လီ
Score: 0.6610469222068787, Word: သမီးရည်းစား
Score: 0.6367117166519165, Word: လရိပ်ချို
Score: 0.6155907511711121, Word: ချာတိတ်
Score: 0.6080843806266785, Word: ကောင်မလေး
Score: 0.5926311016082764, Word: တစ်ခုလပ်
Score: 0.5872882008552551, Word: အိမ်ထောင်သက်
Score: 0.5870575308799744, Word: ဒိတ်ဒိတ်ကျဲ

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အမေ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အမေ':
Score: 0.7647598385810852, Word: အဖေ
Score: 0.7415043115615845, Word: အမေ့
Score: 0.7178197503089905, Word: အမေ.အမေ
Score: 0.6854268312454224, Word: အမေစု
Score: 0.6626180410385132, Word: ကအမေ
Score: 0.6139482259750366, Word: ၁၃၄၄၈၈
Score: 0.6037358641624451, Word: အမေကြီး
Score: 0.5985614657402039, Word: နေနိုင်
Score: 0.5896837115287781, Word: 👩
Score: 0.5820728540420532, Word: သမီး

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word သာဓု --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'သာဓု':
Score: 0.8260522484779358, Word: သာဓုပါ
Score: 0.7169750928878784, Word: ကိုနေယံ
Score: 0.7009290456771851, Word: မွန်မြတ်
Score: 0.6904026865959167, Word: ဒါနအလှူ
Score: 0.6854469180107117, Word: လှူနိုင်
Score: 0.6821122765541077, Word: နေယံ
Score: 0.6801531314849854, Word: တန်ပိုး
Score: 0.6705238223075867, Word: ຂ້າພະເຈົ້າຕ້ອງການການຊ່ວຍເຫຼືອແລະການສະຫນັບສະຫນູນຂອງທັງຫມົດຂອງຫມູ່ເພື່ອນອ້າຍນ້ອງຂອງຂ້າພະເຈົ້າ,
Score: 0.6640245318412781, Word: ກະລຸນາບໍລິຈາກແລະການຊ່ວຍເຫຼືອປະຊາຊົນຜູ້ທີ່ມີບັນຫາໃນການ.
Score: 0.6582797765731812, Word: ແລະເອື້ອຍນ້ອງ.

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word မုန့်ဟင်းခါး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'မုန့်ဟင်းခါး':
Score: 0.8402343392372131, Word: ဟင်းခါး
Score: 0.75030118227005, Word: ကြက်ဟင်းခါး
Score: 0.6872884631156921, Word: မုန့်
Score: 0.6842033863067627, Word: လက်ဖက်သုပ်
Score: 0.6837508082389832, Word: ကြက်ဟင်းခါးသီး
Score: 0.6784169673919678, Word: မုန့်တီ
Score: 0.6722471714019775, Word: ဟင်းချို
Score: 0.660909116268158, Word: မုန့်ဟင်းခါး
Score: 0.640537679195404, Word: ရေခဲမုန့်
Score: 0.6360801458358765, Word: ဟင်းချိုရည်

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အင်တာနက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အင်တာနက်':
Score: 0.6853005290031433, Word: မြန်မာနက်
Score: 0.6841776967048645, Word: တာနကာ
Score: 0.6353737711906433, Word: ကွန်ရက်လိုင်း
Score: 0.6270014047622681, Word: အင်တာနာ
Score: 0.6264851093292236, Word: ကွန်နက်ရှင်
Score: 0.6204766631126404, Word: ဘောနက်
Score: 0.5882505178451538, Word: Travel
Score: 0.5878071188926697, Word: အွန်လိုင်း
Score: 0.5863449573516846, Word: လူမှုကွန်ရက်
Score: 0.5829287171363831, Word: မိုဘိုင်းဖုန်း

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ရန်ကုန် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ရန်ကုန်':
Score: 0.7634686231613159, Word: ရန်ကုန်၊
Score: 0.7200562357902527, Word: မန္တလေး
Score: 0.719448447227478, Word: ရန်ကုန်သား
Score: 0.6878668665885925, Word: ရန်ကုန်သူ
Score: 0.684624433517456, Word: မန္တလေး၊
Score: 0.6782560348510742, Word: မြို့
Score: 0.6690353751182556, Word: ဥက္ကလာပ၊
Score: 0.6620784401893616, Word: လှိုင်သာယာ
Score: 0.6593748927116394, Word: မင်္ဂလာဒုံ
Score: 0.6542323231697083, Word: တက္ကသိုလ်ရိပ်သာ

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ဆီးသွား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ဆီးသွား':
Score: 0.7601823210716248, Word: စီးသွား
Score: 0.6718794107437134, Word: ပြီးသွား
Score: 0.6695263385772705, Word: ဆီးသီး
Score: 0.6653700470924377, Word: Hand
Score: 0.632668673992157, Word: ဆီးသား
Score: 0.6321570873260498, Word: Gel
Score: 0.6146408915519714, Word: မုန့်ဖုတ်ဆော်ဒါ
Score: 0.6006069779396057, Word: ဗွက်ပေါက်
Score: 0.5987318754196167, Word: နို့မှုန့်
Score: 0.5933493375778198, Word: သွားပို့

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ဇာတ်ပို့ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ဇာတ်ပို့':
Score: 0.7372841238975525, Word: ဇာတ်ဆောင်ဆု
Score: 0.7113161087036133, Word: ဇာတ်ပျက်
Score: 0.7102020978927612, Word: ဇာတ်ဆောင်
Score: 0.6731088757514954, Word: အကယ်ဒမီ
Score: 0.6705248951911926, Word: ဇာတ်ပေါင်း
Score: 0.6635294556617737, Word: ဇာတ်ရှိန်
Score: 0.6617113947868347, Word: သရုပ်ဆောင်
Score: 0.6384515166282654, Word: ဇာတ်နာ
Score: 0.629841685295105, Word: ဇာတ်ကားလေး
Score: 0.6172637939453125, Word: ဇာတ်သမား

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word တင်္ခဏုပ္ပတ္တိဉာဏ် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'တင်္ခဏုပ္ပတ္တိဉာဏ်':
Score: 0.6706596612930298, Word: ကဗျာစာပေ
Score: 0.6554387211799622, Word: ဂုဏ်ကျေးဇူး
Score: 0.648225724697113, Word: ကဗျာစု
Score: 0.637607216835022, Word: ရင့်ကျက်
Score: 0.6257622838020325, Word: စဉ်းစားဉာဏ်
Score: 0.6175893545150757, Word: ခြွေရံသင်းပင်း
Score: 0.617182195186615, Word: ဥဿဟ
Score: 0.6155627369880676, Word: အရာထင်
Score: 0.6121906042098999, Word: စိတ်ကူးဉာဏ်
Score: 0.6096184849739075, Word: ရင့်သန်


real    0m6.734s
user    0m6.360s
sys     0m16.137s
(LM) yekyaw.thu@gpu:~/exp/lm$
```

## Update the Python Code

```python
import argparse
import fasttext

def train_model(args):
    # Train a FastText model based on the provided arguments
    model = fasttext.train_unsupervised(
        input=args.input,
        model=args.model_type,
        epoch=args.epochs,
        minCount=args.min_count,
        maxn=args.max_ngram,
        dim=args.dim
    )
    # Save the model
    model.save_model(args.output)

def test_model(args):
    # Load the trained FastText model
    model = fasttext.load_model(args.model)

    # Depending on the operation, perform the action
    if args.operation == 'word_vector':
        # Get the vector of a word
        word_vector = model.get_word_vector(args.word)
        print(f"Vector for '{args.word}':\n{word_vector}")
    elif args.operation == 'nearest_neighbors':
        # Find nearest neighbors of the word
        nearest_neighbors = model.get_nearest_neighbors(args.word, k=args.k)
        print(f"Nearest neighbors for '{args.word}':")
        for neighbor in nearest_neighbors:
            print(f"Score: {neighbor[0]}, Word: {neighbor[1]}")
    elif args.operation == 'word_analogies':
        # New functionality for word analogies
        if not args.analogy or len(args.analogy.split()) != 3:
            print("Error: Analogy query should be in the form 'A B C'")
            return
        a, b, c = args.analogy.split()
        print(f"Querying analogy for: {a} - {b} + {c}")
        analogies = model.get_analogies(a, b, c, k=args.k)
        print("Analogies result:")
        for analogy in analogies:
            print(f"Word: {analogy[1]}, Score: {analogy[0]}")

def main():
    parser = argparse.ArgumentParser(description="FastText Model Trainer and Tester")
    subparsers = parser.add_subparsers(help='Mode of operation', dest='mode')

    # Subparser for training
    parser_train = subparsers.add_parser('train', help='Train a model')
    parser_train.add_argument('--input', '-i', type=str, required=True, help='Input file path')
    parser_train.add_argument('--output', '-o', type=str, required=True, help='Output model filename')
    parser_train.add_argument('--model_type', type=str, choices=['cbow', 'skipgram'], default='skipgram', help='Model type')
    parser_train.add_argument('--epochs', type=int, default=5, help='Number of epochs')
    parser_train.add_argument('--min_count', type=int, default=5, help='Minimum number of word occurrences')
    parser_train.add_argument('--max_ngram', type=int, default=0, help='Maximum length of word ngram')
    parser_train.add_argument('--dim', type=int, default=100, help='Size of word vectors')

    # Subparser for testing
    parser_test = subparsers.add_parser('test', help='Test a model')
    parser_test.add_argument('--model', '-m', type=str, required=True, help='Model filename to load')
    parser_test.add_argument('--operation', '-op', type=str, choices=['word_vector', 'nearest_neighbors', 'word_analogies'], required=True, help='Operation to perform')
    parser_test.add_argument('--word', '-w', type=str, help='Word to analyze (required for word_vector and nearest_neighbors)')
    parser_test.add_argument('--analogy', '-a', type=str, help='Triplet for analogy query in the form "A B C" (required for word_analogies)')
    parser_test.add_argument('--k', type=int, default=10, help='Number of results to return')
	
    args = parser.parse_args()

    if args.mode == 'train':
        train_model(args)
    elif args.mode == 'test':
        test_model(args)
    else:
        parser.print_help()
		
if __name__ == '__main__':
    main()
```

## Called --help

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python ./fasttext_lm.py --help
usage: fasttext_lm.py [-h] {train,test} ...

FastText Model Trainer and Tester

positional arguments:
  {train,test}  Mode of operation
    train       Train a model
    test        Test a model

optional arguments:
  -h, --help    show this help message and exit
(LM) yekyaw.thu@gpu:~/exp/lm$
(LM) yekyaw.thu@gpu:~/exp/lm$ python ./fasttext_lm.py train --help
usage: fasttext_lm.py train [-h] --input INPUT --output OUTPUT
                            [--model_type {cbow,skipgram}] [--epochs EPOCHS]
                            [--min_count MIN_COUNT] [--max_ngram MAX_NGRAM] [--dim DIM]

optional arguments:
  -h, --help            show this help message and exit
  --input INPUT, -i INPUT
                        Input file path
  --output OUTPUT, -o OUTPUT
                        Output model filename
  --model_type {cbow,skipgram}
                        Model type
  --epochs EPOCHS       Number of epochs
  --min_count MIN_COUNT
                        Minimum number of word occurrences
  --max_ngram MAX_NGRAM
                        Maximum length of word ngram
  --dim DIM             Size of word vectors
(LM) yekyaw.thu@gpu:~/exp/lm$
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --help
usage: fasttext_lm.py test [-h] --model MODEL --operation
                           {word_vector,nearest_neighbors,word_analogies} [--word WORD]
                           [--analogy ANALOGY] [--k K]

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL, -m MODEL
                        Model filename to load
  --operation {word_vector,nearest_neighbors,word_analogies}, -op {word_vector,nearest_neighbors,word_analogies}
                        Operation to perform
  --word WORD, -w WORD  Word to analyze (required for word_vector and nearest_neighbors)
  --analogy ANALOGY, -a ANALOGY
                        Triplet for analogy query in the form "A B C" (required for
                        word_analogies)
  --k K                 Number of results to return
(LM) yekyaw.thu@gpu:~/exp/lm$
```

## Testing Mode Example (Nearest Neighbors)  

```
time python ./fasttext_lm.py test  ./model/fasttext.5gram.30ep.model \
--operation nearest_neighbors --word "အိပ်မက်" --k 10
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy "ရန်ကုန် မန္တလေး ပဲခူး" --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ရန်ကုန် - မန္တလေး + ပဲခူး
Analogies result:
Word: ကျွန်တော်ရထာ, Score: 0.5741937160491943
Word: သံဖြူရတု, Score: 0.5565491914749146
Word: ဇီးကွက်စိန်, Score: 0.5344916582107544
Word: အင်္ဂပူ, Score: 0.5179848074913025
Word: မဇီးကွက်စိန်, Score: 0.5133203864097595
Word: မြို့, Score: 0.5028249025344849
Word: ပန်းဘဲတန်း, Score: 0.4979149103164673
Word: သနပ်ပင်, Score: 0.4939956068992615
Word: တိုင်း, Score: 0.49334079027175903
Word: ဥက္ကလာပ၊, Score: 0.4922102093696594
(LM) yekyaw.thu@gpu:~/exp/lm$
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy "အချစ် အမုန်း စိတ်ဆိုး" --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အချစ် - အမုန်း + စိတ်ဆိုး
Analogies result:
Word: အချစ်ရူး, Score: 0.5550366640090942
Word: အစန်း, Score: 0.5549972057342529
Word: အချစ်ဦး, Score: 0.5440096855163574
Word: အိမ်ဆိုး, Score: 0.5289088487625122
Word: အချစ်စစ်, Score: 0.5178499221801758
Word: အချစ်ဆုံးကြီး, Score: 0.513029158115387
Word: စိတ်ဆိုးမာန်ဆိုး, Score: 0.5123149752616882
Word: ပူလောင်, Score: 0.5031462907791138
Word: စိတ်ကောက်, Score: 0.5015113949775696
Word: အချစ်ရေး, Score: 0.5004758834838867
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy "အဖိုး အဖွား အဖေ" --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အဖိုး - အဖွား + အဖေ
Analogies result:
Word: အဖေ့, Score: 0.5599979758262634
Word: အဘိုးလေး, Score: 0.5493155121803284
Word: ဖဲရိုက်, Score: 0.5227209329605103
Word: မောင်အောင်, Score: 0.5067982077598572
Word: အောင်အောင်, Score: 0.5045270919799805
Word: ခင်စိုးမောင်, Score: 0.5026957392692566
Word: ဂျိုး, Score: 0.4978669583797455
Word: မမမြ, Score: 0.4944083094596863
Word: မောင်အုန်းမောင်, Score: 0.49041005969047546
Word: ပဲဝက်, Score: 0.49010178446769714
(LM) yekyaw.thu@gpu:~/exp/lm$
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy "အရက် မိန်းမ လောင်းကစား" --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အရက် - မိန်းမ + လောင်းကစား
Analogies result:
Word: လောင်းကစားဝိုင်း, Score: 0.5526993870735168
Word: အရက်၊, Score: 0.47834888100624084
Word: ဆေးလုံး, Score: 0.46428897976875305
Word: စီးကရက်၊, Score: 0.4641990661621094
Word: ဆေးလိပ်, Score: 0.4641961455345154
Word: အရက်နာ, Score: 0.45736750960350037
Word: လောင်မီးပိုး, Score: 0.44072988629341125
Word: ဆေးလိပ်ဖိုး, Score: 0.440635085105896
Word: အရက်နာကျ, Score: 0.4390476942062378
Word: ရောင်းရငွေ, Score: 0.43038254976272583
(LM) yekyaw.thu@gpu:~/exp/lm$
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy "ဆိုင်ကယ် ကား ဆိုက်ကား" --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ဆိုင်ကယ် - ကား + ဆိုက်ကား
Analogies result:
Word: ဆိုက်ကားသမား, Score: 0.6044085025787354
Word: နင်း, Score: 0.5526857376098633
Word: ဆိုင်ကယ်သမား, Score: 0.5525379180908203
Word: ဆိုက္ကား, Score: 0.5500503778457642
Word: လီဗာ, Score: 0.5367855429649353
Word: မခင်ဘုန်း, Score: 0.5162790417671204
Word: ဆိုက်ကြီး, Score: 0.5128453969955444
Word: ဆိုင်ကယ်ကြီး, Score: 0.5095804929733276
Word: ဆိုင်ကယ်သံ, Score: 0.5038426518440247
Word: ခင်ဘုန်း, Score: 0.49523523449897766
(LM) yekyaw.thu@gpu:~/exp/lm$
```

## Updating the Python Script

I wanna add interactive mode for testing ...  

Current version:   

(LM) yekyaw.thu@gpu:~/exp/lm$ cat fasttext_lm.py   
 
 ```python
import argparse
import fasttext

def train_model(args):
    # Train a FastText model based on the provided arguments
    model = fasttext.train_unsupervised(
        input=args.input,
        model=args.model_type,
        epoch=args.epochs,
        minCount=args.min_count,
        maxn=args.max_ngram,
        dim=args.dim
    )
    # Save the model
    model.save_model(args.output)

def test_model(args):
    # Load the trained FastText model
    model = fasttext.load_model(args.model)

    # Depending on the operation, perform the action
    if args.operation == 'word_vector':
        # Get the vector of a word
        word_vector = model.get_word_vector(args.word)
        print(f"Vector for '{args.word}':\n{word_vector}")
    elif args.operation == 'nearest_neighbors':
        # Find nearest neighbors of the word
        nearest_neighbors = model.get_nearest_neighbors(args.word, k=args.k)
        print(f"Nearest neighbors for '{args.word}':")
        for neighbor in nearest_neighbors:
            print(f"Score: {neighbor[0]}, Word: {neighbor[1]}")
    elif args.operation == 'word_analogies':
        # New functionality for word analogies
        if not args.analogy or len(args.analogy.split()) != 3:
            print("Error: Analogy query should be in the form 'A B C'")
            return
        a, b, c = args.analogy.split()
        print(f"Querying analogy for: {a} - {b} + {c}")
        analogies = model.get_analogies(a, b, c, k=args.k)
        print("Analogies result:")
        for analogy in analogies:
            print(f"Word: {analogy[1]}, Score: {analogy[0]}")

def main():
    parser = argparse.ArgumentParser(description="FastText Model Trainer and Tester")
    subparsers = parser.add_subparsers(help='Mode of operation', dest='mode')

    # Subparser for training
    parser_train = subparsers.add_parser('train', help='Train a model')
    parser_train.add_argument('--input', '-i', type=str, required=True, help='Input file path')
    parser_train.add_argument('--output', '-o', type=str, required=True, help='Output model filename')
    parser_train.add_argument('--model_type', type=str, choices=['cbow', 'skipgram'], default='skipgram', help='Model type')
    parser_train.add_argument('--epochs', type=int, default=5, help='Number of epochs')
    parser_train.add_argument('--min_count', type=int, default=5, help='Minimum number of word occurrences')
    parser_train.add_argument('--max_ngram', type=int, default=0, help='Maximum length of word ngram')
    parser_train.add_argument('--dim', type=int, default=100, help='Size of word vectors')

    # Subparser for testing
    parser_test = subparsers.add_parser('test', help='Test a model')
    parser_test.add_argument('--model', '-m', type=str, required=True, help='Model filename to load')
    parser_test.add_argument('--operation', '-op', type=str, choices=['word_vector', 'nearest_neighbors', 'word_analogies'], required=True, help='Operation to perform')
    parser_test.add_argument('--word', '-w', type=str, help='Word to analyze (required for word_vector and nearest_neighbors)')
    parser_test.add_argument('--analogy', '-a', type=str, help='Triplet for analogy query in the form "A B C" (required for word_analogies)')
    parser_test.add_argument('--k', type=int, default=10, help='Number of results to return')

    args = parser.parse_args()

    if args.mode == 'train':
        train_model(args)
    elif args.mode == 'test':
        test_model(args)
    else:
        parser.print_help()

if __name__ == '__main__':
    main()

 ```

I updated as follows:  

(LM) yekyaw.thu@gpu:~/exp/lm$ cat fasttext_lm.py  

 ```
import argparse
import fasttext

def train_model(args):
    # Train a FastText model based on the provided arguments
    model = fasttext.train_unsupervised(
        input=args.input,
        model=args.model_type,
        epoch=args.epochs,
        minCount=args.min_count,
        maxn=args.max_ngram,
        dim=args.dim
    )
    # Save the model
    model.save_model(args.output)

def test_model(args):
    # Load the trained FastText model
    model = fasttext.load_model(args.model)

    # If interactive mode is selected
    if args.interactive:
        print("Entering interactive mode...")
        while True:
            user_input = input("Enter word or analogy (Ctrl+D or 'quit' to exit): ")
            if user_input.lower() == 'quit':
                print("Exiting interactive mode...")
                break
            if args.operation == 'word_vector':
                word_vector = model.get_word_vector(user_input)
                print(f"Vector for '{user_input}':\n{word_vector}")
            elif args.operation == 'nearest_neighbors':
                nearest_neighbors = model.get_nearest_neighbors(user_input, k=args.k)
                print(f"Nearest neighbors for '{user_input}':")
                for neighbor in nearest_neighbors:
                    print(f"Score: {neighbor[0]}, Word: {neighbor[1]}")
            elif args.operation == 'word_analogies':
                if len(user_input.split()) != 3:
                    print("Error: Analogy query should be in the form 'A B C'")
                    continue
                a, b, c = user_input.split()
                print(f"Querying analogy for: {a} - {b} + {c}")
                analogies = model.get_analogies(a, b, c, k=args.k)
                print("Analogies result:")
                for analogy in analogies:
                    print(f"Word: {analogy[1]}, Score: {analogy[0]}")
            elif args.operation == 'word_vector' or args.operation == 'nearest_neighbors':
                # Check if word is provided
                if not user_input:
                    print("Error: Word is required for word_vector or nearest_neighbors operation.")
                    continue
                if args.operation == 'word_vector':
                    word_vector = model.get_word_vector(user_input)
                    print(f"Vector for '{user_input}':\n{word_vector}")
                elif args.operation == 'nearest_neighbors':
                    nearest_neighbors = model.get_nearest_neighbors(user_input, k=args.k)
                    print(f"Nearest neighbors for '{user_input}':")
                    for neighbor in nearest_neighbors:
                        print(f"Score: {neighbor[0]}, Word: {neighbor[1]}")
            else:
                print("Error: Invalid operation specified.")
    else:
        # Perform the specific operation
        if args.operation == 'word_vector':
            word_vector = model.get_word_vector(args.word)
            print(f"Vector for '{args.word}':\n{word_vector}")
        elif args.operation == 'nearest_neighbors':
            nearest_neighbors = model.get_nearest_neighbors(args.word, k=args.k)
            print(f"Nearest neighbors for '{args.word}':")
            for neighbor in nearest_neighbors:
                print(f"Score: {neighbor[0]}, Word: {neighbor[1]}")
        elif args.operation == 'word_analogies':
            if not args.analogy or len(args.analogy.split()) != 3:
                print("Error: Analogy query should be in the form 'A B C'")
                return
            a, b, c = args.analogy.split()
            print(f"Querying analogy for: {a} - {b} + {c}")
            analogies = model.get_analogies(a, b, c, k=args.k)
            print("Analogies result:")
            for analogy in analogies:
                print(f"Word: {analogy[1]}, Score: {analogy[0]}")
        else:
            print("Error: Invalid operation specified.")

def main():
    parser = argparse.ArgumentParser(description="FastText Model Trainer and Tester")
    subparsers = parser.add_subparsers(help='Mode of operation', dest='mode')

    # Subparser for training
    parser_train = subparsers.add_parser('train', help='Train a model')
    parser_train.add_argument('--input', '-i', type=str, required=True, help='Input file path')
    parser_train.add_argument('--output', '-o', type=str, required=True, help='Output model filename')
    parser_train.add_argument('--model_type', type=str, choices=['cbow', 'skipgram'], default='skipgram', help='Model type')
    parser_train.add_argument('--epochs', type=int, default=5, help='Number of epochs')
    parser_train.add_argument('--min_count', type=int, default=5, help='Minimum number of word occurrences')
    parser_train.add_argument('--max_ngram', type=int, default=0, help='Maximum length of word ngram')
    parser_train.add_argument('--dim', type=int, default=100, help='Size of word vectors')

    # Subparser for testing
    parser_test = subparsers.add_parser('test', help='Test a model')
    parser_test.add_argument('--model', '-m', type=str, required=True, help='Model filename to load')
    parser_test.add_argument('--operation', '-op', type=str, choices=['word_vector', 'nearest_neighbors', 'word_analogies'], help='Operation to perform')
    parser_test.add_argument('--word', '-w', type=str, help='Word to analyze (required for word_vector and nearest_neighbors)')
    parser_test.add_argument('--analogy', '-a', type=str, help='Triplet for analogy query in the form "A B C" (required for word_analogies)')
    parser_test.add_argument('--k', type=int, default=10, help='Number of results to return')
    parser_test.add_argument('--interactive', action='store_true', help='Enable interactive mode')

    args = parser.parse_args()

    if args.mode == 'train':
        train_model(args)
    elif args.mode == 'test':
        test_model(args)
    else:
        parser.print_help()

if __name__ == '__main__':
    main()
 ```

## Train/Test Again

Prepared shell script as follows:    

(LM) yekyaw.thu@gpu:~/exp/lm$ cat ./run_ftlm.sh   

 ```bash
#!/bin/bash

set -x

# Training Mode:
#time python ./fasttext_lm.py train \
#--input ./corpus/myWord_myPOS_myPara_myNovelv1_wordseg.shuf \
#--output ./model/fasttext.5gram.30ep.model --model_type skipgram \
#--min_count 3 --max_ngram 5 --epochs 30

# Testing Mode Example (Word Vector):
time python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation word_vector --word "အိပ်မက်" --k 10

# Testing Mode Example (Nearest Neighbors):
time python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation nearest_neighbors --word "အိပ်မက်" --k 10

# Testing Mode Example (Word Analogy):
python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation word_analogies --analogy "အချစ် အမုန်း စိတ်ဆိုး" --k 10

set +x
 ```

The running result is as follows:    

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ ./run_ftlm.sh
+ python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word အိပ်မက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'အိပ်မက်':
[-0.32339147 -0.24345082  0.013641    0.00381868 -0.5152162   0.07852398
  0.09378184  0.1061763  -0.7437571   1.1673816   0.03308625 -0.7637368
  0.39179382  0.15719512 -0.42015293 -0.3354506  -0.00902283 -0.34560314
  0.41394794  0.38042507  0.09650397 -0.39613697 -0.05091747  0.01488579
 -0.20615518 -0.41393417  0.10988221 -0.0633272  -0.60385007  0.8232522
  0.10997569 -0.22061978  0.22577201 -0.00193948 -0.03870042  0.41159382
 -0.275526    0.2659175   0.4899396  -0.19320336  0.37592623  0.19700204
 -0.51530993 -0.50839186  0.24767765 -0.02406422  0.16876397 -0.33567995
 -0.13786504 -0.26064807 -0.54374874 -0.31017065 -0.23081654 -0.12507342
  0.36045313 -0.02969589 -0.1609194   0.11724221 -0.62486345  0.66902506
  0.01148518 -0.11793222  0.07267848 -0.5597016   0.1975448  -0.01815919
 -0.0851561   0.07272398  0.42399994  0.78658855 -1.0099938   0.12450463
  0.3220353  -0.7207977  -0.06542195 -0.33083636  0.9079614  -0.16433133
  0.37499797 -0.25025144 -0.27300858 -0.4700494  -0.19895194  0.5989566
  0.67933214 -0.5792831   0.30991998 -0.65864295 -0.07637522 -0.39732653
 -0.00231774  0.1434416  -0.042597    0.7733869   0.4282226  -0.2662088
  0.75148696  0.2018375  -0.4701276  -0.22571974]

real    0m0.554s
user    0m0.494s
sys     0m1.589s
+ python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အိပ်မက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အိပ်မက်':
Score: 0.7457765936851501, Word: အိပ်မက်ဆိုး
Score: 0.7424984574317932, Word: မက်
Score: 0.721375048160553, Word: အိပ်မက်လေး
Score: 0.7172493934631348, Word: အိပ်မက်မက်
Score: 0.6227003335952759, Word: မြင်မက်
Score: 0.6189436912536621, Word: ကောသလ
Score: 0.5356197357177734, Word: စိတ်ကူးယဉ်
Score: 0.5255365371704102, Word: ဧကဒသမ
Score: 0.5234008431434631, Word: အနမ်း
Score: 0.5156580805778503, Word: ည

real    0m0.683s
user    0m0.671s
sys     0m1.623s
+ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy 'အချစ် အမုန်း စိတ်ဆိုး' --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အချစ် - အမုန်း + စိတ်ဆိုး
Analogies result:
Word: အိမ်ဆိုး, Score: 0.548224687576294
Word: လွမ်းဆွေး, Score: 0.5089129209518433
Word: အိပ်မက်ဆိုး, Score: 0.5062306523323059
Word: မထိတထိ, Score: 0.5020098686218262
Word: အချစ်ရူး, Score: 0.5002419352531433
Word: အချစ်ဦး, Score: 0.495620995759964
Word: ငယ်ကျွမ်းဆွေ, Score: 0.4949243366718292
Word: ကိုအောင်ထက်, Score: 0.49073344469070435
Word: စိတ်ဆိုးမာန်ဆိုး, Score: 0.48897144198417664
Word: စကားနာထိုး, Score: 0.4858129024505615
+ set +x
(LM) yekyaw.thu@gpu:~/exp/lm$
 ```

## Testing Interactive Mode

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --interactive
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ကျား မ အထီး
Querying analogy for: ကျား - မ + အထီး
Analogies result:
Word: လင်းယုန်ငှက်, Score: 0.494272917509079
Word: သစ်ကုလားအုပ်, Score: 0.4917362630367279
Word: ကျားသစ်, Score: 0.49152112007141113
Word: ယုန်, Score: 0.4780251681804657
Word: ကျားကျား, Score: 0.47468894720077515
Word: ဥဗျိုင်း, Score: 0.4745984673500061
Word: ကြိုးကြာငှက်, Score: 0.4646100103855133
Word: ကုလားအုပ်, Score: 0.4639550447463989
Word: မြင်းကျား, Score: 0.4593314230442047
Word: မျောက်နီ, Score: 0.45792287588119507
Enter word or analogy (Ctrl+D or 'quit' to exit): ကျား
Error: Analogy query should be in the form 'A B C'
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
 ```

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --interactive
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ကျား မ အထီး
Vector for 'ကျား မ အထီး':
[-0.2133764   0.05952065  0.24507058  0.17731982 -0.44827342  0.19464786
  0.05977132  0.03105187 -0.3551465  -0.3290775  -0.37147254 -0.00439501
  0.07592285  0.19159193 -0.11377493  0.25995916  0.10650574  0.08568764
  0.05597349 -0.01809666  0.18027394 -0.02373214 -0.12484667  0.04042477
 -0.02436369  0.17348047  0.07218172  0.2804557  -0.09736003  0.17582098
  0.46391356  0.1915815  -0.3423941   0.01484453 -0.30543727  0.0069105
  0.25740895 -0.18216029 -0.01279015  0.09513247  0.15976083  0.0948505
  0.14407097 -0.29275614 -0.27402556 -0.08672122 -0.10746586 -0.10929436
 -0.06475465 -0.00069321  0.11535583 -0.00163587  0.23672439 -0.0323762
  0.16844     0.006665   -0.03675539  0.17001015  0.30406818  0.0897029
 -0.15117967  0.17463848 -0.05376938 -0.11447643 -0.11353999 -0.2517246
 -0.45260066 -0.18842667 -0.28869513  0.09737534 -0.03686793 -0.15284248
  0.2959105  -0.36555886 -0.2989536  -0.5416031   0.10765683  0.03192116
 -0.05761804 -0.12710963  0.25307015 -0.2304095  -0.13597593 -0.06556956
  0.45536718 -0.2490939  -0.04044142 -0.18877028 -0.34703982  0.31134784
  0.2522021  -0.20245932 -0.13711852 -0.08232339  0.0588808   0.09222991
 -0.25831127 -0.07015447 -0.04399963  0.07088248]
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
(LM) yekyaw.thu@gpu:~/exp/lm$
 ```

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --interactive
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ကျား
Nearest neighbors for 'ကျား':
Score: 0.7093421816825867, Word: ကျားကျား
Score: 0.5987985134124756, Word: မကန်း
Score: 0.5980209708213806, Word: ကျား၊
Score: 0.5814911127090454, Word: ခြင်္သေ့
Score: 0.5807584524154663, Word: ခြင်္သေ
Score: 0.5641698241233826, Word: မြင်းကျား
Score: 0.56353360414505, Word: ကျားသစ်
Score: 0.5549535751342773, Word: ရွှေကျား
Score: 0.5478503704071045, Word: မုဆိုး
Score: 0.5473718643188477, Word: ချောင်ချောင်
Enter word or analogy (Ctrl+D or 'quit' to exit): မ
Nearest neighbors for 'မ':
Score: 0.8295145034790039, Word: ဘူး
Score: 0.792195200920105, Word: ဟုတ်
Score: 0.7553627490997314, Word: သေး
Score: 0.7143582105636597, Word: တော့
Score: 0.7057028412818909, Word: ရ
Score: 0.7015810608863831, Word: သိ
Score: 0.6913994550704956, Word: ဆို
Score: 0.6792703866958618, Word: ဘာ
Score: 0.6725432276725769, Word: လည်း
Score: 0.6678541302680969, Word: “ဂီး”
Enter word or analogy (Ctrl+D or 'quit' to exit):
 ```

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --interactive
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): မေမေ ဖေဖေ မာမီ
Querying analogy for: မေမေ - ဖေဖေ + မာမီ
Analogies result:
Word: မာမီ့, Score: 0.6184867024421692
Word: မာမီစိုး, Score: 0.5875133275985718
Word: ပါးပါးလေး, Score: 0.5092029571533203
Word: ဂစ်, Score: 0.4941007196903229
Word: တူတူ, Score: 0.49397018551826477
Word: Madly, Score: 0.49262258410453796
Word: Christmas, Score: 0.49080973863601685
Word: ဂျော်လကီး, Score: 0.49078795313835144
Word: ဂျူဒီ, Score: 0.49044477939605713
Word: ဟောသူ, Score: 0.4883553087711334
Enter word or analogy (Ctrl+D or 'quit' to exit): ရွှေ ငွေ စိန်
Querying analogy for: ရွှေ - ငွေ + စိန်
Analogies result:
Word: တဖျတ်ဖျတ်, Score: 0.5251243710517883
Word: ရွှေဖီ, Score: 0.5215801000595093
Word: မြ, Score: 0.5002743005752563
Word: ပြာရောင်, Score: 0.4833815395832062
Word: မြရောင်, Score: 0.47850656509399414
Word: ပတ္တမြား, Score: 0.4767526686191559
Word: ဘယက်, Score: 0.476696640253067
Word: စိန်ဘယက်, Score: 0.47633424401283264
Word: ရွှေး, Score: 0.47402748465538025
Word: စိန်တုံး, Score: 0.47321921586990356
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
(LM) yekyaw.thu@gpu:~/exp/lm$
 ```

## Testing with File

I prepared python code as follows:   

(LM) yekyaw.thu@gpu:~/exp/lm$ cat ./ftlm_test_with_file.py  

```python
"""
python code for running fasttext_lm.py with test file.
Written by Ye Kyaw Thu, LU Lab., Myanmar
Last updated: 10 Feb 2024

How to run:
# for word_vector
python ./ftlm_test_with_file.py --input ./test1.txt --operation word_vector

# for nearest_neighbors
python ./ftlm_test_with_file.py --input ./test1.txt --operation nearest_neighbors

# for word_analogies
python ./ftlm_test_with_file.py --input ./test2.txt --operation word_analogies

"""

import argparse
import subprocess
import sys

def process_word(word, model_path, operation, k, output_file=None):
    command = [
        "python", "./fasttext_lm.py", "test",
        "--model", model_path,
        "--operation", operation,
        "--word", word,
        "--k", str(k)
    ]
    print(f"Running command: {' '.join(command)}")
    # Updated subprocess.run call without using capture_output
    result = subprocess.run(command, stdout=subprocess.PIPE, stderr=subprocess.STDOUT, text=True)
    output = result.stdout  # Captures both stdout and stderr
    if output:
        if output_file:
            with open(output_file, "a", encoding="utf-8") as f:
                f.write(output)
        else:
            print(output)

def process_analogy(words, model_path, operation, k, output_file=None):
    if len(words) != 3:
        print("Error: Analogy query should be in the form 'A B C'")
        return
    command = [
        "python", "./fasttext_lm.py", "test",
        "--model", model_path,
        "--operation", operation,
        "--analogy", " ".join(words),
        "--k", str(k)
    ]
    print(f"Running command: {' '.join(command)}")
    # Updated subprocess.run call without using capture_output
    result = subprocess.run(command, stdout=subprocess.PIPE, stderr=subprocess.STDOUT, text=True)
    output = result.stdout  # Captures both stdout and stderr
    if output:
        if output_file:
            with open(output_file, "a", encoding="utf-8") as f:
                f.write(output)
        else:
            print(output)

def main():
    parser = argparse.ArgumentParser(description="Process each word from a file or stdin.")
    parser.add_argument("-i", "--input", type=str, help="Input file name.")
    parser.add_argument("-o", "--output", type=str, help="Output file name.")
    parser.add_argument("--model", type=str, default="./model/fasttext.5gram.30ep.model", help="Path to the model.")
    parser.add_argument("--operation", type=str, default="nearest_neighbors", help="Operation to perform.")
    parser.add_argument("--k", type=int, default=10, help="Number of nearest neighbors.")

    args = parser.parse_args()

    # Clear the output file if it exists
    if args.output:
        open(args.output, "w").close()

    input_stream = open(args.input, "r", encoding="utf-8") if args.input else sys.stdin

    for line in input_stream:
        words = line.strip().split()
        if args.operation == 'word_analogies':
            process_analogy(words, args.model, args.operation, args.k, args.output)
        else:
            for word in words:
                process_word(word, args.model, args.operation, args.k, args.output)

    if args.input:
        input_stream.close()

if __name__ == "__main__":
    main()
 ```

I also preapred a shell script as follows:   

(LM) yekyaw.thu@gpu:~/exp/lm$ cat ./run_ftlm_test_with_file.sh  

 ```bash
#!/bin/bash

# for word_vector
python ./ftlm_test_with_file.py --input ./test1.txt --operation word_vector

# for nearest_neighbors
python ./ftlm_test_with_file.py --input ./test1.txt --operation nearest_neighbors

# for word_analogies
python ./ftlm_test_with_file.py --input ./test2.txt --operation word_analogies
 ```

I used two test files: test1.txt (one word, one line) and test2.txt (three words, one line).  
Test file for word_vector and nearest_neighbors testing:  

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ cat test1.txt
စိတ္တဇ
ရည်းစား
အမေ
သာဓု
မုန့်ဟင်းခါး
အင်တာနက်
ရန်ကုန်
ဆီးသွား
ဇာတ်ပို့
တင်္ခဏုပ္ပတ္တိဉာဏ်
(LM) yekyaw.thu@gpu:~/exp/lm$
 ```

Test file for word_analogies testing:   

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ cat test2.txt
ဝက် ဝက်သား ကြက်
ဘုရင် မိဖုရား ဘုန်းကြီး
အထီး အမ ယောက်ျား
ရေ ရေခွက် အရက်
လက်ရှည် လက်တို ဘောင်းဘီရှည်
အချစ် အမုန်း အပြုံး
(LM) yekyaw.thu@gpu:~/exp/lm$
 ```

Run the shell script:  

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ ./run_ftlm_test_with_file.sh | tee test_with_file_input.log
Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word စိတ္တဇ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'စိတ္တဇ':
[-1.0118635e+00  1.0804765e-01  2.3958233e-01  2.4650119e-01
  2.0188509e-01  3.5175404e-01  1.8384519e-01  4.5734906e-01
 -4.8504978e-01  4.8163366e-01 -1.5282388e-01  9.2564568e-02
  4.7543094e-01 -1.9328374e-01  1.5442489e-02 -2.7490082e-01
  3.7830120e-01 -4.0872806e-01  8.9323401e-02  1.1263998e+00
 -8.6765981e-01  1.9621801e-01  3.6416316e-01 -1.7021668e-01
  7.0038810e-03  8.4138453e-01  4.9688292e-01 -2.4119459e-02
  3.7231237e-01 -5.1518661e-01  1.3229102e-03  4.6606243e-01
  4.1202107e-01  3.2266781e-01 -8.2929337e-01  2.8710777e-01
  1.2599220e-03  2.4390523e-01 -1.4808235e-01 -4.3228593e-01
  1.2065072e-01  4.7314173e-01  6.7864799e-01 -1.0863521e+00
  6.5995616e-01 -4.0248251e-01 -9.2874193e-01 -3.9002779e-01
 -8.2800984e-01 -2.5206909e-01  1.8956582e-01  4.2796719e-01
  8.6607611e-01  1.3321432e+00  1.8578047e-01 -5.7821238e-01
  2.7912620e-01  3.6355558e-01  4.4318885e-03  1.7586060e-01
  6.6785496e-01  1.1742989e+00 -4.0142453e-01  2.3351520e-02
 -4.6152139e-01 -4.9297711e-01  3.2815117e-01 -2.8836131e-02
 -1.6051318e-01  3.5511452e-01 -1.3978106e-01 -3.9237389e-01
  3.6354846e-01 -1.2676646e+00 -4.0163737e-02 -2.6917177e-01
  4.0794367e-01 -3.0117077e-01 -2.0414083e-01  1.6573161e-01
  2.2023612e-01 -3.4486052e-01 -7.0996177e-01 -2.7559263e-01
  7.2685349e-01  2.1281652e-01  8.7010407e-01 -5.7892513e-01
  2.5250041e-01  5.6692266e-01  1.9470046e-01  6.1239950e-02
  3.4431386e-01  3.5601339e-01 -2.2040050e-01  6.8032444e-02
  3.0948302e-01 -9.0873092e-03  1.1514530e-02 -5.9673190e-01]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ရည်းစား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ရည်းစား':
[ 0.00545872  0.527198    0.01432193  0.5445639   0.5738146   0.54823387
 -0.6661694  -0.22563432  0.3080712   0.18273124 -0.40917802 -0.01643307
 -0.29031473  0.02067617  0.0057199   0.00701874 -0.23005985 -0.4732518
 -0.39426032  0.4628378   0.32595614 -0.03716286 -0.05230084  0.08075769
  0.42092556  0.90594155 -0.31796736  0.24898614  0.03457218  0.13545291
  0.17864306  0.6143033  -0.163252    0.00890038  0.12763634  0.3482217
 -0.29419518 -0.10987061  0.2230199   0.20541601  0.13627346  0.06805363
  0.2513385  -1.0457808   0.51511335  0.03677322 -0.15277545 -0.3774327
  0.14679018  0.37390333 -0.49898022  0.25565317  0.9608319   0.3106182
  0.01980724 -0.73499477 -0.0909228   0.68021715 -0.17656478  0.59768844
 -0.0019068   0.09405538  0.14493725  0.12839027  0.12632279  0.07582351
 -0.82635677 -0.06875096 -0.01664198  0.38611642  0.22505632 -0.14259006
  0.5298969  -0.809511   -0.31883645 -0.47477493  0.26791173  0.7880413
  0.5472069  -0.17453511  0.41897604 -0.34047446 -0.16893896 -0.39726076
  0.5926138  -0.5352696  -0.24583927 -0.0824409   0.11120781  0.16446197
  0.43986902 -0.26846722  0.03962776  0.15757991 -0.40479496 -0.20176798
  0.4497649   0.96132904  0.35028318 -0.12513237]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word အမေ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'အမေ':
[-1.69910476e-01 -2.66555369e-01  1.29693359e-01  2.72150964e-01
 -1.32694528e-01 -1.55923441e-01 -3.67432863e-01 -2.81770140e-01
 -1.19956635e-01  6.25784844e-02  3.65246385e-01  2.99581736e-01
 -3.65069270e-01  4.26132739e-01  2.96102494e-01 -2.56348938e-01
 -3.51052463e-01 -1.57406375e-01 -1.02139242e-01 -8.96002948e-02
 -2.00433955e-01  3.91312182e-01 -8.85316655e-02  1.31626889e-01
 -2.64364909e-02  1.92732066e-01 -5.46616137e-01  1.17411040e-01
 -8.00672099e-02  6.80270851e-01  2.81305552e-01  8.28937948e-01
  2.56537378e-01  5.26042357e-02  1.36516362e-01 -8.84473175e-02
  1.28511429e-01 -3.66490185e-01  5.07681608e-01 -4.08590406e-01
  5.29280677e-02  1.01022549e-01  7.94317052e-02 -2.75643200e-01
  6.24131501e-01 -1.18501171e-01  6.20949090e-01 -1.84965625e-01
 -5.00368252e-02 -2.49415133e-02 -2.22429350e-01  8.76734965e-03
 -2.06777260e-01  6.32293522e-01  4.87205088e-01  2.15735406e-01
 -5.03460541e-02  8.41718987e-02 -2.39133239e-01  1.73268974e-01
 -3.55069548e-01  2.87117392e-01 -3.21037710e-01 -2.16696054e-01
  6.19948208e-02 -6.50689900e-01 -4.28307354e-01 -2.16768533e-01
 -1.27354115e-01  1.33686528e-01 -4.67977077e-01 -3.15332502e-01
 -4.28023003e-02 -6.36987686e-01 -3.70684713e-01 -2.29675174e-01
 -9.97213498e-02 -4.13348190e-02 -7.59572834e-02 -4.05929089e-02
  3.81679416e-01 -3.56043279e-01 -1.78933158e-04  1.87574193e-01
  3.45053405e-01 -4.30758774e-01 -5.37969291e-01  3.15425582e-02
 -3.62754762e-01  6.28737271e-01 -2.37677060e-02  1.28046975e-01
 -6.53684884e-02  2.81813502e-01  5.23644924e-01  2.35873431e-01
  4.81236912e-02  1.04331411e-01 -1.80971488e-01  2.14252725e-01]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word သာဓု --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'သာဓု':
[ 0.6885621  -0.89991903  0.09157505  0.39147264  0.17538433  0.53623885
  0.64291185 -0.0603058   0.09840851  0.45903024 -0.02627039 -0.14790653
  0.00338989 -0.06122218  0.12620132  0.07073791 -0.58397615 -0.567091
 -0.5296934   0.48577324 -0.34596366  0.4338257   1.0020113  -1.5495461
 -0.69353104 -0.2124025  -0.41736528 -0.59420055 -0.41939327  0.10928092
  0.5667848  -0.65558594  0.26030394 -0.00989828 -0.03564563  0.27134654
  0.38641182 -0.60899377  0.07870974 -0.4400762   0.3031824   0.24116984
  0.59475917 -0.20015709  1.0558144   0.0910893   0.37429366 -0.1952413
 -0.46162716 -0.17987405 -0.01247071  0.13644128  0.3550797   0.5387067
  1.077959    0.3026126  -0.7727557   0.70528865  0.6696271   0.47925612
  0.38858122 -0.8541884  -0.22210348 -0.64314026  0.7624747  -0.9487921
 -1.0831865   0.91023666  0.4148441   0.48606464  0.06345042 -0.16681425
 -0.8445614  -0.24352446 -0.2073214  -0.15332626  0.32141325  0.18183294
 -0.18820132 -0.66306293 -0.04307999 -0.04328482 -0.00831574  0.92636263
  0.35618806  0.29760084  0.11701848 -0.46692792  0.7269805   0.47761354
  0.12058955 -0.21120284  0.14060293  0.80002356 -0.50139946  0.2670926
  0.11945935  0.49913025 -0.13529997 -0.45042244]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word မုန့်ဟင်းခါး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'မုန့်ဟင်းခါး':
[-6.5522212e-01 -5.5821413e-01 -7.8979484e-04  7.8250462e-01
 -1.5640819e-01 -4.6312028e-01 -2.5346023e-01  1.7039594e-01
 -1.6726755e-01  4.0068594e-01 -6.8440777e-01  5.3804915e-02
 -4.1264418e-01  1.4750420e-01 -1.8279535e-01  2.5512436e-01
  6.5616161e-01  5.2662039e-01 -9.2658556e-01  8.4109068e-02
  1.0440763e-01 -2.6855013e-01  1.3264622e-01  6.4255273e-01
 -4.5618477e-01  4.3694136e-01 -7.3397511e-01  4.4372761e-01
 -2.9637797e-03 -3.3642378e-02 -2.8328779e-01  5.2148756e-02
 -2.2310999e-01 -2.5903288e-02  3.3330557e-01  4.8846397e-01
  1.9821386e-01 -7.9070991e-01  5.2374363e-01 -7.3973858e-01
  1.1337626e+00 -9.5801100e-02  7.4050951e-01 -8.6247730e-01
  2.4718288e-01 -4.2136016e-01  2.2589897e-01  8.0632186e-01
  9.1786020e-02 -5.3360415e-01 -6.4309269e-01 -4.2099345e-01
 -3.9511374e-01  2.2302793e-01 -2.4163134e-01  3.2975489e-01
  2.0287614e-01  1.2997316e-01 -3.1112424e-01  8.1031293e-01
  3.1512704e-02  8.1592321e-01  4.3584746e-01  8.2599491e-01
 -1.5879302e-01 -6.7672372e-01 -8.9998049e-01 -2.4151684e-01
  4.4191271e-02 -3.5361049e-01 -7.0695728e-02 -4.1033658e-01
 -6.8380281e-02 -5.5166000e-01 -6.8882309e-02 -1.6344531e-01
 -3.8041747e-01 -8.8923998e-02  1.9535881e-01 -8.1487870e-01
 -2.6539370e-01 -1.9193619e-01 -5.8685265e-02  3.5316408e-01
 -9.5287167e-02 -5.4200238e-01 -3.1034866e-01 -2.8382221e-01
 -1.2925941e-01  6.5226358e-01  1.8440649e-01  1.7826356e-01
  8.6627811e-01  8.4322923e-01 -1.5398572e-01 -1.2926030e-02
 -1.7563760e-02 -1.9929048e-01 -8.6118644e-01  2.7387637e-01]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word အင်တာနက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'အင်တာနက်':
[-0.16182636  0.24229068  0.07997095 -0.14783688 -0.15370797 -0.26795155
 -0.22436784 -0.1467624  -0.24062526  0.2811765   0.15596862 -0.2891532
  0.31585634  0.5749548   0.43515167  0.28101647  0.1252028   0.16584074
 -0.5778557  -0.16181307  0.28904474 -0.12738362 -0.14982818 -0.21254241
 -0.7839702   0.62292904  0.45223948  0.9235177  -0.6496037  -0.12925716
 -0.8109895  -0.04301884  0.4228916   0.0851818  -0.5404664   0.06744979
  0.09972295  0.16218166  0.51367533  0.203276    0.00978012  0.6245306
  0.14671467 -0.53170806  0.1695907   0.19033436  0.10875098 -0.09528264
  0.31622174 -0.2976016  -0.49093246 -0.98813164  0.48243183 -0.25787058
  0.8324308   0.4109107  -0.20242809 -0.15793039 -0.07080945 -0.04555671
  0.20616016 -0.5467633   0.19953646  0.31621534  0.5104672  -0.0966205
 -0.90863925  0.57873714 -0.38404292 -0.85959774 -0.31258425 -0.4666886
 -0.03799115 -0.20772026  0.19844322  0.33700377  0.2215752  -0.12530312
  0.8281181  -0.13586482  0.58032084 -0.29894638 -0.13844073  0.2781583
  1.0750233  -0.55018294 -0.06730026  0.02406189  0.11628749 -0.4523496
  1.0307503   0.3565153   0.09228339  0.48486504  0.5360036  -0.8008978
 -0.2264376   0.20477295  0.18590422 -0.08280194]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ရန်ကုန် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ရန်ကုန်':
[ 7.4476264e-02  2.5062078e-01 -1.0861032e-01 -6.6695377e-02
 -3.1790668e-01 -1.2340111e-01 -4.0094808e-02  2.2088729e-01
 -2.4900627e-01  3.5108113e-01 -9.4307877e-02 -3.4346569e-02
 -4.9108791e-01  3.3403182e-01  1.7522499e-02 -2.8858286e-01
  1.5856387e-01  4.1084372e-02  7.4429549e-02  3.2894382e-01
  2.8404418e-01 -2.4715038e-01 -3.1510761e-01 -1.0847486e-01
 -5.1311493e-02  4.5151088e-01 -1.6492285e-01  6.8034661e-01
  3.2478228e-01 -9.4651245e-02  8.7020636e-01 -5.2918893e-01
 -7.0126720e-02  9.4903283e-02 -1.5446465e-01  9.9683195e-02
  3.6969316e-01 -4.7702834e-01  7.7617541e-02 -2.6339999e-01
  3.1286088e-01  4.0355930e-01  5.5499453e-02 -8.3948815e-01
 -8.0135450e-02 -2.2870211e-01 -5.0449944e-01 -1.3429974e-01
  3.1445304e-01 -3.9869523e-01 -3.9438719e-01  7.8248166e-02
  2.3291752e-02  3.6511579e-01  5.0144559e-01 -2.3482734e-01
 -1.0359774e-01  3.4254012e-01  2.9670751e-02  2.1895093e-01
  4.8743659e-01 -1.7835452e-01 -3.3680687e-03 -1.3866374e-01
  5.0699812e-01 -6.6751093e-01 -7.6501548e-01  3.3933172e-01
 -2.8413275e-01 -2.9287475e-01  4.1829798e-01  1.0205321e-01
  1.7531352e-01 -4.9704001e-03 -1.0069054e-01 -4.1549587e-01
  1.2872790e-01  1.0178172e-01 -4.2836938e-02 -5.6544136e-02
  3.7858427e-02  1.6662189e-01 -1.1597448e-01  3.7169069e-01
 -2.9572177e-01  1.7835034e-01 -1.9905187e-01  1.5396602e-01
  5.7301752e-02 -2.0437075e-01 -3.5133755e-01  3.3085072e-01
 -4.5872584e-01  2.9014957e-01  5.5782199e-01 -2.7614540e-01
  4.6154700e-04  3.9466545e-01  1.8263380e-01 -7.5932026e-02]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ဆီးသွား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ဆီးသွား':
[-3.8978156e-01  2.5926782e-02 -6.3465703e-01 -5.5769807e-01
 -5.8149832e-01 -5.1495105e-01  1.4739527e-01 -5.5100858e-01
 -1.9226469e-01  5.7077652e-01 -7.4251455e-01  4.2705312e-01
  1.5021369e-01 -2.9611105e-02  7.6041657e-01 -6.5112448e-01
  3.0730289e-01  4.3754378e-01  3.1970432e-01 -2.0293543e-02
  1.1734816e-01  2.0290552e-01  1.3706371e-01 -1.7940930e-01
 -5.3092235e-01  9.0932137e-01 -5.6168765e-01 -5.2574601e-02
 -2.0604153e-01 -6.0745150e-01 -2.7478170e-01 -7.3073578e-01
 -5.7732439e-01  4.1389874e-01  4.3220878e-02  1.3202089e-01
 -1.6999374e-01 -1.3530067e-01 -4.6334711e-01  4.5565632e-03
  5.0116766e-02  3.2500297e-01  3.1193713e-02 -2.2430679e-01
  4.2220750e-01 -1.7983150e-01  1.0296297e-01 -2.2819686e-01
 -7.8221954e-02 -4.2927599e-01 -5.5160064e-01 -1.7228146e-01
  9.4739503e-01  4.2285379e-02  7.4662298e-01  5.9781390e-01
 -2.3752446e-01  6.3365465e-01 -1.2297746e-01  1.4403978e-01
 -6.7851223e-02  5.1484388e-01  4.4175389e-01  2.7018869e-01
 -2.3414247e-01 -4.8379025e-01 -3.6317548e-01 -3.1911299e-01
  1.7148157e-03 -1.8083606e-02 -1.9532178e-02 -4.1842616e-01
 -1.0216276e-01 -1.7808354e-01  1.7834762e-02  1.8939550e-01
 -1.6542767e-01 -2.8219555e-02  5.2343768e-01 -4.4876996e-01
  4.0484306e-01 -5.3775185e-01 -2.0193784e-01  5.5279666e-01
  3.3552495e-01 -1.6709082e-01 -7.2491199e-02  2.6884368e-01
  2.7970502e-01 -1.4732128e-01  3.0005223e-01  1.2533194e-01
  1.8803807e-01  4.3778960e-02 -1.3662279e-01  2.9968110e-01
 -3.1881864e-05  4.5700312e-01 -9.5085758e-01 -7.8346789e-01]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ဇာတ်ပို့ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ဇာတ်ပို့':
[-2.0266183e-01  3.6240637e-01 -4.1869563e-01  5.0491285e-01
  1.9953236e-01  2.8306857e-01 -7.3879704e-02 -4.9864423e-02
 -1.7529368e-01  1.2046651e+00 -7.6443797e-01  2.8498477e-01
 -3.5754699e-01 -4.3318471e-01 -2.0691350e-01 -6.4632905e-01
  3.1081605e-01 -4.1262212e-01 -6.1757416e-01 -9.1797769e-01
 -9.8130786e-01 -8.1728660e-02 -1.1566362e-01  8.6991489e-04
 -7.5248408e-01 -1.7088480e-01 -2.3763654e-01 -1.4368899e-01
  3.9645065e-02 -3.0235592e-01  2.3224680e-01  5.2973408e-01
 -6.4875400e-01  6.4152873e-01 -3.7085544e-02  6.4300585e-01
  6.6946346e-01 -2.6642263e-01  8.6694896e-02  3.7976012e-01
  2.3157094e-01  1.4313576e+00 -3.8938108e-01 -2.3679212e-01
  5.7551491e-01  2.8015700e-01 -3.4927338e-01 -3.6500087e-01
  5.4842216e-01 -4.4491958e-02  2.0932448e-03 -1.0539333e-01
  4.0233254e-01  2.0361045e-01  3.3290842e-01  5.9211266e-01
 -6.0908192e-01  1.4255133e-01 -8.9889862e-02 -2.7974015e-01
 -1.5428384e-01  3.6750391e-01  5.6730592e-01 -1.4825085e-01
  1.8627161e-01 -3.6304295e-01 -7.7279145e-01  7.0756215e-01
 -5.3352404e-01  1.9233291e-01 -5.7243520e-01 -9.5744008e-01
 -3.8838157e-01 -4.0813684e-01 -7.9369219e-03 -6.8711694e-03
  7.7568525e-01  7.2944993e-01  2.2057438e-01 -2.9163575e-01
 -1.4792044e-01 -2.0411961e-01 -5.7960272e-01 -2.9904372e-01
  3.6663282e-01 -2.1748765e-01  1.5465550e-01 -4.8788500e-01
 -5.5286896e-01  5.9404200e-01  1.1442862e+00  2.3333743e-01
  2.8385302e-01  3.3311136e-02  2.2495168e-01 -3.0865189e-01
  2.4917295e-02  8.1451720e-01  2.7536744e-01 -6.1446571e-01]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word တင်္ခဏုပ္ပတ္တိဉာဏ် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'တင်္ခဏုပ္ပတ္တိဉာဏ်':
[-0.11541229  0.10395357 -0.11252035  0.21203052 -0.08080124 -0.48639387
  0.2089383  -0.0667093  -0.05739744 -0.11579878 -0.98748755  0.03679125
  0.523712    0.6323363  -0.34436882  0.38357842  0.11504064  0.5358087
 -0.03782908  0.08850771  0.16511993  0.45939952 -0.19094062 -0.1501373
 -0.57203466  0.01228668  0.05699036 -0.2668385   0.35891348  0.80128473
  0.04309111 -0.19172123 -0.31963983 -0.0258819  -0.41996348  0.2377998
  0.06938622 -0.4021461   0.3180154   0.01492259  0.19152945  0.33008662
 -0.32024485 -0.38434482  0.5478323  -0.0465069   0.188041   -0.08967008
 -0.13586088  0.5776601   0.04581776 -0.14816764 -0.30760345  0.37307692
  0.06524102  0.17847517 -0.2767326   0.07139228 -0.45972335  0.6297389
 -0.08449876  0.13938802  0.14582773 -0.44518352  0.4006172   0.00786821
  0.28356662  0.32068932 -0.21739957 -0.0315267   0.29852515 -0.5454241
  0.25583687 -0.6834677  -0.28355846 -0.5072807   0.4153551  -0.06377734
  0.14475681  0.34049183 -0.32477373 -0.59436625 -0.55700254  0.21601513
  0.9220212  -0.16587853  0.16825043 -0.50760317 -0.08639346  0.55517626
 -0.21949728  0.27982846  0.56420714  0.1891142   0.40381196 -0.04685044
  0.6599855   0.193569   -0.15609992 -0.71329224]

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word စိတ္တဇ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'စိတ္တဇ':
Score: 0.6745372414588928, Word: စိတ္တ
Score: 0.6314203143119812, Word: စိတ္တဗေဒ
Score: 0.5564653873443604, Word: စိတ္တသုခ
Score: 0.5403991341590881, Word: စွဲလမ်း
Score: 0.5255535244941711, Word: သမစိတ္တ
Score: 0.507357656955719, Word: ပင်ကိုယ်
Score: 0.5036177039146423, Word: ရင်ကွဲနာကျ
Score: 0.4915549159049988, Word: တကိုယ်တည်း
Score: 0.4914068579673767, Word: ဂျူးလိယက်
Score: 0.48948854207992554, Word: ညီဘွား

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ရည်းစား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ရည်းစား':
Score: 0.7757509350776672, Word: ရည်းစားစာ
Score: 0.6781648397445679, Word: ရည်းစားဟောင်း
Score: 0.6231962442398071, Word: တောဂေါ်လီ
Score: 0.6093384027481079, Word: သမီးရည်းစား
Score: 0.6000670790672302, Word: လရိပ်ချို
Score: 0.5970081686973572, Word: 🍸
Score: 0.580669105052948, Word: သူငယ်ချင်း
Score: 0.5788516402244568, Word: အနမ်း
Score: 0.5646747350692749, Word: ရွှေရင်အေး
Score: 0.5624873042106628, Word: စာ

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အမေ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အမေ':
Score: 0.761120617389679, Word: အဖေ
Score: 0.7552878260612488, Word: အမေ့
Score: 0.678351879119873, Word: အမေ.အမေ
Score: 0.6685445308685303, Word: သမီး
Score: 0.6548821926116943, Word: ကအမေ
Score: 0.6250607371330261, Word: အမေစု
Score: 0.6222426295280457, Word: အဖေ့
Score: 0.6068939566612244, Word: သန်းရွေ
Score: 0.5936732888221741, Word: ၁၃၄၄၈၈
Score: 0.5876482129096985, Word: မေမေစု

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word သာဓု --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'သာဓု':
Score: 0.8412624001502991, Word: သာဓုပါ
Score: 0.7210538983345032, Word: မွန်မြတ်
Score: 0.7169498205184937, Word: လှူနိုင်
Score: 0.7013123035430908, Word: နေယံ
Score: 0.6901063323020935, Word: ကိုနေယံ
Score: 0.6675360202789307, Word: ဒါနအလှူ
Score: 0.6646379828453064, Word: တန်ပိုး
Score: 0.6631753444671631, Word: မက‌
Score: 0.6534916758537292, Word: သုထု
Score: 0.6504325270652771, Word: ແລະເອື້ອຍນ້ອງ.

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word မုန့်ဟင်းခါး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'မုန့်ဟင်းခါး':
Score: 0.7852288484573364, Word: ဟင်းခါး
Score: 0.6910621523857117, Word: ကြက်ဟင်းခါး
Score: 0.6702976822853088, Word: လက်ဖက်သုပ်
Score: 0.6636655926704407, Word: မုန့်ဆီကြော်
Score: 0.6512320041656494, Word: ကြက်ဟင်းခါးသီး
Score: 0.6480793356895447, Word: မုန့်တီ
Score: 0.6474567651748657, Word: ကြက်သားဟင်း
Score: 0.6457094550132751, Word: မုန့်
Score: 0.641377329826355, Word: ငါးဟင်း
Score: 0.6351057887077332, Word: အသားဟင်း

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အင်တာနက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အင်တာနက်':
Score: 0.6849741339683533, Word: မြန်မာနက်
Score: 0.6563037037849426, Word: တာနကာ
Score: 0.6388484239578247, Word: ဘောနက်
Score: 0.6250481009483337, Word: ကွန်ရက်လိုင်း
Score: 0.60463947057724, Word: coverage
Score: 0.6005971431732178, Word: ကွန်နက်ရှင်
Score: 0.5924235582351685, Word: လူမှုကွန်ရက်
Score: 0.5914555191993713, Word: တာဝါတိုင်
Score: 0.5884498953819275, Word: မိုဘိုင်းဖုန်း
Score: 0.5841873288154602, Word: Flymya

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ရန်ကုန် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ရန်ကုန်':
Score: 0.756117582321167, Word: ရန်ကုန်၊
Score: 0.754541277885437, Word: ရန်ကုန်သား
Score: 0.7338629364967346, Word: မန္တလေး
Score: 0.6744452118873596, Word: မြို့
Score: 0.6673221588134766, Word: မန္တလေး၊
Score: 0.6669890880584717, Word: ရန်ကုန်သူ
Score: 0.651691198348999, Word: လှိုင်သာယာ
Score: 0.6367980241775513, Word: ချမ်းမြသာစည်
Score: 0.6322051882743835, Word: ပန်းဘဲတန်း
Score: 0.6280223727226257, Word: မင်္ဂလာဒုံ

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ဆီးသွား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ဆီးသွား':
Score: 0.7799282073974609, Word: စီးသွား
Score: 0.6609404683113098, Word: ပြီးသွား
Score: 0.634963870048523, Word: ဆီးသီး
Score: 0.6018061637878418, Word: ခရီးသွား
Score: 0.5888448357582092, Word: သွားတိုက်ဆေး
Score: 0.5876478552818298, Word: ခရီးသွားချက်လက်မှတ်
Score: 0.5850068926811218, Word: ဆီးသား
Score: 0.5780267119407654, Word: ရှာလကာရည်
Score: 0.576163113117218, Word: နို့မှုန့်
Score: 0.5697601437568665, Word: ကူလုပ်

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ဇာတ်ပို့ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ဇာတ်ပို့':
Score: 0.7116348743438721, Word: ဇာတ်ဆောင်ဆု
Score: 0.6891847848892212, Word: ဇာတ်ဆောင်
Score: 0.6787474751472473, Word: ဇာတ်ရံ
Score: 0.6786273717880249, Word: ဇာတ်ရှိန်
Score: 0.6701122522354126, Word: ဇာတ်ပျက်
Score: 0.6538248658180237, Word: သရုပ်ဆောင်
Score: 0.6390606760978699, Word: ဇာတ်ပေါင်း
Score: 0.6297541260719299, Word: ဇာတ်ကားလေး
Score: 0.6218425631523132, Word: အကယ်ဒမီ
Score: 0.6165277361869812, Word: ဇာတ်ကား

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word တင်္ခဏုပ္ပတ္တိဉာဏ် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'တင်္ခဏုပ္ပတ္တိဉာဏ်':
Score: 0.6905746459960938, Word: ဝိပ္ပတ္တိ
Score: 0.6794511079788208, Word: အရာထင်
Score: 0.6479311585426331, Word: ကဗျာစာပေ
Score: 0.6278204321861267, Word: ကဗျာစု
Score: 0.6260987520217896, Word: သမ္ပတ္တိ
Score: 0.6159682869911194, Word: ဂုဏ်ကျေးဇူး
Score: 0.6074728965759277, Word: ရင့်ကျက်
Score: 0.6056002974510193, Word: ဥဿဟ
Score: 0.6026166677474976, Word: ဂုဏ်တက်
Score: 0.5922082662582397, Word: ခွန်အားဗလ

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy ဝက် ဝက်သား ကြက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ဝက် - ဝက်သား + ကြက်
Analogies result:
Word: တောကြက်, Score: 0.5121555328369141
Word: ဥစားကြက်, Score: 0.5099843144416809
Word: ကြက်ကလေး, Score: 0.4849660098552704
Word: ခ.ဘဲ, Score: 0.47066834568977356
Word: အသားစားကြက်, Score: 0.4689839780330658
Word: အိမ်မွေး, Score: 0.46137741208076477
Word: ရေကြက်, Score: 0.46065887808799744
Word: ခ., Score: 0.4575563371181488
Word: ခ/ဘဲ, Score: 0.44462278485298157
Word: ကြိုးကြာငှက်, Score: 0.44371265172958374

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy ဘုရင် မိဖုရား ဘုန်းကြီး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ဘုရင် - မိဖုရား + ဘုန်းကြီး
Analogies result:
Word: ဘုန်းကြီးလမ်း, Score: 0.5942283868789673
Word: ဘုန်းကြီးကျောင်းသား, Score: 0.5466357469558716
Word: ဘုန်းကြီးကျောင်း, Score: 0.4987032115459442
Word: ဘုန်းတော်ကြီး, Score: 0.4942268133163452
Word: နှိပ်ကွပ်, Score: 0.49074065685272217
Word: သာကီမျိုး, Score: 0.48203378915786743
Word: ဘုန်းကြီးကျောင်းဝင်း, Score: 0.4753101170063019
Word: ဖူးမျှော်, Score: 0.4696580469608307
Word: ဘုန်းကံ, Score: 0.4639660716056824
Word: ဘုန်းဘုန်း, Score: 0.4624267816543579

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy အထီး အမ ယောက်ျား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အထီး - အမ + ယောက်ျား
Analogies result:
Word: ယောက်ျားကြီး, Score: 0.6168034672737122
Word: ယောက်ျားသား, Score: 0.6016280651092529
Word: လင်ယောက်ျား, Score: 0.5660913586616516
Word: ကျွဲရိုင်း, Score: 0.5407551527023315
Word: ဝံ့ရဲ, Score: 0.5309659838676453
Word: မိန်းမ, Score: 0.5306455492973328
Word: ယောက်ျားပျို, Score: 0.5153751373291016
Word: ယောက်ျားလေး, Score: 0.5015631318092346
Word: တစ်တွေ, Score: 0.49583834409713745
Word: .ယောက်ျား, Score: 0.49141883850097656

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy ရေ ရေခွက် အရက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ရေ - ရေခွက် + အရက်
Analogies result:
Word: ကိုချမ်း, Score: 0.5624952912330627
Word: ကိုခရမ်း, Score: 0.5311194658279419
Word: ကိုပိုင်, Score: 0.5098628997802734
Word: ဘီယာ, Score: 0.5079320669174194
Word: ကိုရခိုင်, Score: 0.492196649312973
Word: ဆီချက်, Score: 0.4914039671421051
Word: လရည်, Score: 0.48958122730255127
Word: နင်ဇီမေ, Score: 0.4873463809490204
Word: ကိုခင်လှိုင်, Score: 0.48692262172698975
Word: သောက်, Score: 0.48561981320381165

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy လက်ရှည် လက်တို ဘောင်းဘီရှည် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: လက်ရှည် - လက်တို + ဘောင်းဘီရှည်
Analogies result:
Word: ဘောင်းဘီတို, Score: 0.5471829771995544
Word: ဝတ်, Score: 0.5393813848495483
Word: ခရမ်းနုရောင်, Score: 0.5370433926582336
Word: အသက်ရှည်, Score: 0.5358654260635376
Word: အပြာနုရောင်, Score: 0.5329601168632507
Word: ရေကူးဝတ်စုံ, Score: 0.5274295210838318
Word: အပြာရင့်ရောင်, Score: 0.5247268080711365
Word: နုစို, Score: 0.5203062891960144
Word: ဆံပင်ရှည်, Score: 0.519849419593811
Word: ရေညှိရောင်, Score: 0.5172668099403381

Running command: python ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy အချစ် အမုန်း အပြုံး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အချစ် - အမုန်း + အပြုံး
Analogies result:
Word: အပြုံးရိပ်, Score: 0.5669716000556946
Word: အနမ်းဝိုင်, Score: 0.5554046034812927
Word: အနမ်း, Score: 0.5439690351486206
Word: နှင်းဆီပန်း, Score: 0.534136176109314
Word: မျက်ဝန်း, Score: 0.5284920930862427
Word: အချစ်စစ်, Score: 0.5265051126480103
Word: အပြုံးအရယ်, Score: 0.5172467231750488
Word: နှလုံးသား, Score: 0.5050758123397827
Word: စိတ်ကူးယဉ်သမား, Score: 0.5030249953269958
Word: စိတ်ကူးယဉ်, Score: 0.5015185475349426

(LM) yekyaw.thu@gpu:~/exp/lm$
 ```

## Prepared a Shell Script for Interactive Mode

(LM) yekyaw.thu@gpu:~/exp/lm$ cat ./run_ftlm_interactive_test.sh  

 ```bash
#!/bin/bash

# Interactive testing for word_vector
python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation word_vector --interactive

# Interactive testing for nearest_neighbors
python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation nearest_neighbors --interactive

# Interactive testing for word_analogies
python fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation word_analogies --interactive
 ```

## Testing interactive mode with above shell script

 ```
(LM) yekyaw.thu@gpu:~/exp/lm$ ./run_ftlm_interactive_test.sh
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ငြိမ်းချမ်းရေး
Vector for 'ငြိမ်းချမ်းရေး':
[-2.6637360e-01 -2.5988296e-02 -7.3015511e-02  1.2163663e-01
  4.7325525e-01  4.9233895e-02 -2.6486030e-01 -7.9712950e-02
 -2.0359485e-01  3.2073289e-01  2.3492716e-02  1.5137824e-01
 -3.2633483e-01  6.1063755e-01  2.4733391e-01  2.0441031e-02
  5.2976894e-01 -7.0290715e-03  9.1979176e-02 -1.0079595e-01
  6.6378200e-01  3.6550468e-01 -3.1398493e-01 -1.3358088e-01
 -5.3094395e-02  7.1050599e-02  1.8718870e-01 -2.0570207e-01
  2.4451354e-01  4.1718403e-01 -3.7144624e-02 -2.4825235e-01
  3.1419837e-01 -2.3688471e-01 -2.4889627e-01 -3.5098219e-01
  2.0846875e-01 -1.7309861e-01 -3.5218057e-01 -9.1800593e-02
  2.0443121e-01  9.7311333e-02 -4.4746837e-01  1.1773051e-01
 -2.3145953e-01  1.8410683e-04  5.0970137e-01 -4.6338090e-01
 -2.5228354e-01 -1.2123664e-01 -2.3879461e-01 -2.3346419e-02
 -1.6751730e-01  1.4633486e-02  7.4894392e-01  2.4342914e-01
 -1.3608977e-01  7.2178972e-01 -1.8077070e-01  2.1777430e-01
 -2.8583962e-01 -9.5663995e-02  2.0185781e-01  3.7827572e-01
  1.0411831e+00 -3.6657462e-01 -5.4706764e-01  2.9374129e-01
  2.0138292e-01 -6.1102718e-01  4.0427110e-01 -3.3217883e-01
  4.9038664e-01 -6.2400240e-01 -2.3442553e-01 -4.8564383e-01
  3.0073154e-01  7.2540991e-02  3.9905688e-01  3.9552775e-01
 -1.0344744e-01 -8.9070164e-02 -4.2539239e-01  4.5410705e-01
  4.9451463e-02  1.7267962e-01  6.2672305e-01  5.7268327e-01
 -3.2950407e-01  3.6410987e-01 -2.9874736e-02  2.2700162e-01
  6.5574628e-01  1.2953471e-01 -6.8689756e-02  1.8777786e-01
 -1.5561858e-01  5.7756954e-01 -6.2144953e-01 -2.1604720e-01]
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ငြိမ်းချမ်းရေး
Nearest neighbors for 'ငြိမ်းချမ်းရေး':
Score: 0.7946479320526123, Word: ငြိမ်းချမ်းပါ
Score: 0.7655441164970398, Word: ငြိမ်းချမ်း
Score: 0.760322093963623, Word: ငြိမ်းငြိမ်းချမ်းချမ်း
Score: 0.7493445873260498, Word: ငြိမ်းချမ်းသာယာ
Score: 0.7411526441574097, Word: ငြိမ်းချမ်းစွာ
Score: 0.7075689435005188, Word: ဦးငြိမ်းချမ်းဖြိုး
Score: 0.6769238710403442, Word: ငြိမ်းချမ်းအောင်
Score: 0.6592147350311279, Word: အတွင်းရေး
Score: 0.6398895978927612, Word: တိုင်းရေးပြည်ရေး
Score: 0.6279233694076538, Word: တိုင်းရေးပြည်ရာ
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ဆန် ထမင်း ဂျုံ
Querying analogy for: ဆန် - ထမင်း + ဂျုံ
Analogies result:
Word: ဂျုံမှုန့်, Score: 0.5106478929519653
Word: တန်ချိန်, Score: 0.49746260046958923
Word: ထုတ်လုပ်, Score: 0.46791139245033264
Word: ထွက်ကုန်ပစ္စည်း, Score: 0.4592607319355011
Word: ထွက်ကုန်, Score: 0.4577306807041168
Word: ဓာတ်မြေဩဇာ, Score: 0.44889649748802185
Word: တင်ပို့, Score: 0.44280552864074707
Word: ဓါတ်မြေဩဇာ, Score: 0.43992483615875244
Word: မြေပဲဆံ, Score: 0.4345601201057434
Word: ဂျုံး, Score: 0.4343375265598297
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
(LM) yekyaw.thu@gpu:~/exp/lm$
 ```

## MIT-LM ?!

Statistical LM က ငါသိရသလောက်က Python library အနေနဲ့ ခေါ်သုံးဖို့က အရမ်းအဆင်ပြေကြီး မဟုတ်ဘူး။  

SRILM LM က Python အနေနဲ့ wrapper လုပ်သုံးရင်တော့ ရပေမဲ့ library အနေနဲ့ မရှိဘူး။  
SRILM က သုံးဖို့အတွက် registration လုပ်ရတယ်။ Commercial အတွက် အဆင်မပြေဘူး။  

KenLM ကလည်း Python အနေနဲ့ သုံးလို့ရပေမဲ့ မော်ဒယ်ဆောက်တဲ့အပိုင်း မပါဘူး။ ဆောက်ပြီးသား KenLM မော်ဒယ်ကိုပဲ load လုပ်ပြီး သုံးဖို့လောက်ပဲ အဆင်ပြေတယ်။  

MITLM ကလည်း အရမ်းကြာနေပြီ update လည်း နောက်ပိုင်း မလုပ်တော့ဘူးလားလို့ ...  







## Corpus Cleaning

https://github.com/ye-kyaw-thu/tools/blob/master/python/clean_non_burmese.py

နဲ့ corpus ထဲက မမြင်ရတဲ့ ZWNJ, ZWJ, နိုင်ငံခြားဘာသာစကားရဲ့ စာလုံးတွေ၊ ဂဏန်းတွေကိုလည်း ဖျက်ခဲ့တယ်။ 

## Training and Testing  with Cleaned Corpus

(base) yekyaw.thu@gpu:~/exp/lm/corpus$ shuf ./myNovelv1_wordseg.txt > ./myNovelv1_wordseg.shuf
(base) yekyaw.thu@gpu:~/exp/lm/corpus$

Combined two monolingual corpora:  

(base) yekyaw.thu@gpu:~/exp/lm/corpus$ cat ./myWord_myPOS_myPara.merged.shuf ./myNovelv1_wordseg.shuf > myWord_myPOS_myPara_myNovelv1_wordseg.shuf
(base) yekyaw.thu@gpu:~/exp/lm/corpus$ wc ./myWord_myPOS_myPara_myNovelv1_wordseg.shuf
  358047  7554252 96329489 ./myWord_myPOS_myPara_myNovelv1_wordseg.shuf
(base) yekyaw.thu@gpu:~/exp/lm/corpus$




## Reference

https://alphacephei.com/nsh/2020/12/13/lm-toolkits.html
https://github.com/alphacep/vosk-space/blob/master/lm.md

https://github.com/mmz33/N-Gram-Language-Model

https://github.com/shayan09/Text-Generation-using-NGRAM-models/blob/master/ngram.py

## KenLM

ဒီတခါတော့ KenLM နဲ့ LM model ဆောက်ဖို့ ပြင်ဆင်မယ်။   

## Installation of conda-forge boost cmake gcc

The followings are about my Python version:  

```
(LM) yekyaw.thu@gpu:~/exp/lm$ which python
/home/yekyaw.thu/.conda/envs/LM/bin/python
(LM) yekyaw.thu@gpu:~/exp/lm$ python --version
Python 3.8.18
(LM) yekyaw.thu@gpu:~/exp/lm$
```

Install build dependencies: KenLM requires boost, cmake, and gcc to compile.  

```
(LM) yekyaw.thu@gpu:~/exp/lm$ conda install -c conda-forge boost cmake gcc
Collecting package metadata (current_repodata.json): done
Solving environment: -
The environment is inconsistent, please check the package plan carefully
The following packages are causing the inconsistency:

  - defaults/linux-64::pip==23.3.1=py38h06a4308_0
  - conda-forge/linux-64::numpy==1.22.3=py38h99721a1_2
  - defaults/linux-64::tk==8.6.12=h1ccaba5_0
  - defaults/linux-64::setuptools==68.2.2=py38h06a4308_0
  - conda-forge/linux-64::libopenblas==0.3.20=pthreads_h78a6416_0
  - conda-forge/linux-64::python_abi==3.8=2_cp38
  - defaults/linux-64::python==3.8.18=h955ad1f_0
  - defaults/linux-64::ncurses==6.4=h6a678d5_0
  - defaults/linux-64::zlib==1.2.13=h5eee18b_0
  - conda-forge/linux-64::fasttext==0.9.2=py38h43d8883_4
  - defaults/linux-64::openssl==3.0.13=h7f8727e_0
  - defaults/linux-64::libgcc-ng==11.2.0=h1234567_1
  - conda-forge/linux-64::libblas==3.9.0=15_linux64_openblas
  - conda-forge/linux-64::libcblas==3.9.0=15_linux64_openblas
  - defaults/linux-64::xz==5.4.5=h5eee18b_0
  - defaults/linux-64::wheel==0.41.2=py38h06a4308_0
  - defaults/linux-64::libffi==3.4.4=h6a678d5_0
  - defaults/linux-64::readline==8.2=h5eee18b_0
  - conda-forge/linux-64::pybind11==2.6.1=py38h82cb98a_0
  - defaults/linux-64::sqlite==3.41.2=h5eee18b_0
  - conda-forge/linux-64::liblapack==3.9.0=15_linux64_openblas
  - defaults/linux-64::libstdcxx-ng==11.2.0=h1234567_1
done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/LM

  added / updated specs:
    - boost
    - cmake
    - gcc


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    _libgcc_mutex-0.1          |      conda_forge           3 KB  conda-forge
    _openmp_mutex-4.5          |            2_gnu          23 KB  conda-forge
    binutils_impl_linux-64-2.40|       hf600244_0         5.2 MB  conda-forge
    boost-1.84.0               |       hb563948_0          13 KB  conda-forge
    bzip2-1.0.8                |       hd590300_5         248 KB  conda-forge
    c-ares-1.26.0              |       hd590300_0         159 KB  conda-forge
    cmake-3.28.3               |       hcfe8598_0        17.9 MB  conda-forge
    gcc-13.2.0                 |       h574f8da_2          26 KB  conda-forge
    gcc_impl_linux-64-13.2.0   |       h338b0a0_5        50.8 MB  conda-forge
    icu-73.2                   |       h59595ed_0        11.5 MB  conda-forge
    kernel-headers_linux-64-2.6.32|      he073ed8_16         692 KB  conda-forge
    keyutils-1.6.1             |       h166bdaf_0         115 KB  conda-forge
    krb5-1.20.1                |       h81ceb04_0         1.3 MB  conda-forge
    ld_impl_linux-64-2.40      |       h41732ed_0         688 KB  conda-forge
    libboost-1.84.0            |       h6fcfa73_0         2.6 MB  conda-forge
    libboost-devel-1.84.0      |       h00ab1b0_0          35 KB  conda-forge
    libboost-headers-1.84.0    |       ha770c72_0        13.1 MB  conda-forge
    libboost-python-1.84.0     |   py38hae673b5_0         116 KB  conda-forge
    libboost-python-devel-1.84.0|   py38hb563948_0          16 KB  conda-forge
    libcurl-8.5.0              |       h251f7ec_0         416 KB
    libedit-3.1.20191231       |       he28a2e2_2         121 KB  conda-forge
    libev-4.33                 |       hd590300_2         110 KB  conda-forge
    libexpat-2.5.0             |       hcb278e6_1          76 KB  conda-forge
    libgcc-devel_linux-64-13.2.0|     ha9c7c90_105         2.5 MB  conda-forge
    libgcc-ng-13.2.0           |       h807b86a_5         752 KB  conda-forge
    libgomp-13.2.0             |       h807b86a_5         410 KB  conda-forge
    libnghttp2-1.57.0          |       h2d74bed_0         674 KB
    libsanitizer-13.2.0        |       h7e041cc_5         3.9 MB  conda-forge
    libssh2-1.10.0             |       hdbd6064_2         292 KB
    libstdcxx-ng-13.2.0        |       h7e041cc_5         3.7 MB  conda-forge
    libuv-1.47.0               |       hd590300_0         872 KB  conda-forge
    libzlib-1.2.13             |       hd590300_5          60 KB  conda-forge
    numpy-1.24.4               |   py38h59b608b_0         6.4 MB  conda-forge
    rhash-1.4.4                |       hd590300_0         181 KB  conda-forge
    sysroot_linux-64-2.12      |      he073ed8_16        14.6 MB  conda-forge
    zlib-1.2.13                |       hd590300_5          91 KB  conda-forge
    zstd-1.5.5                 |       hfc55251_0         532 KB  conda-forge
    ------------------------------------------------------------
                                           Total:       139.9 MB

The following NEW packages will be INSTALLED:

  binutils_impl_lin~ conda-forge/linux-64::binutils_impl_linux-64-2.40-hf600244_0
  boost              conda-forge/linux-64::boost-1.84.0-hb563948_0
  bzip2              conda-forge/linux-64::bzip2-1.0.8-hd590300_5
  c-ares             conda-forge/linux-64::c-ares-1.26.0-hd590300_0
  cmake              conda-forge/linux-64::cmake-3.28.3-hcfe8598_0
  gcc                conda-forge/linux-64::gcc-13.2.0-h574f8da_2
  gcc_impl_linux-64  conda-forge/linux-64::gcc_impl_linux-64-13.2.0-h338b0a0_5
  icu                conda-forge/linux-64::icu-73.2-h59595ed_0
  kernel-headers_li~ conda-forge/noarch::kernel-headers_linux-64-2.6.32-he073ed8_16
  keyutils           conda-forge/linux-64::keyutils-1.6.1-h166bdaf_0
  krb5               conda-forge/linux-64::krb5-1.20.1-h81ceb04_0
  libboost           conda-forge/linux-64::libboost-1.84.0-h6fcfa73_0
  libboost-devel     conda-forge/linux-64::libboost-devel-1.84.0-h00ab1b0_0
  libboost-headers   conda-forge/linux-64::libboost-headers-1.84.0-ha770c72_0
  libboost-python    conda-forge/linux-64::libboost-python-1.84.0-py38hae673b5_0
  libboost-python-d~ conda-forge/linux-64::libboost-python-devel-1.84.0-py38hb563948_0
  libcurl            pkgs/main/linux-64::libcurl-8.5.0-h251f7ec_0
  libedit            conda-forge/linux-64::libedit-3.1.20191231-he28a2e2_2
  libev              conda-forge/linux-64::libev-4.33-hd590300_2
  libexpat           conda-forge/linux-64::libexpat-2.5.0-hcb278e6_1
  libgcc-devel_linu~ conda-forge/noarch::libgcc-devel_linux-64-13.2.0-ha9c7c90_105
  libnghttp2         pkgs/main/linux-64::libnghttp2-1.57.0-h2d74bed_0
  libsanitizer       conda-forge/linux-64::libsanitizer-13.2.0-h7e041cc_5
  libssh2            pkgs/main/linux-64::libssh2-1.10.0-hdbd6064_2
  libuv              conda-forge/linux-64::libuv-1.47.0-hd590300_0
  libzlib            conda-forge/linux-64::libzlib-1.2.13-hd590300_5
  rhash              conda-forge/linux-64::rhash-1.4.4-hd590300_0
  sysroot_linux-64   conda-forge/noarch::sysroot_linux-64-2.12-he073ed8_16
  zstd               conda-forge/linux-64::zstd-1.5.5-hfc55251_0

The following packages will be UPDATED:

  ld_impl_linux-64   pkgs/main::ld_impl_linux-64-2.38-h118~ --> conda-forge::ld_impl_linux-64-2.40-h41732ed_0
  libgcc-ng          pkgs/main::libgcc-ng-11.2.0-h1234567_1 --> conda-forge::libgcc-ng-13.2.0-h807b86a_5
  libgomp              pkgs/main::libgomp-11.2.0-h1234567_1 --> conda-forge::libgomp-13.2.0-h807b86a_5
  libstdcxx-ng       pkgs/main::libstdcxx-ng-11.2.0-h12345~ --> conda-forge::libstdcxx-ng-13.2.0-h7e041cc_5
  numpy                               1.22.3-py38h99721a1_2 --> 1.24.4-py38h59b608b_0
  zlib                    pkgs/main::zlib-1.2.13-h5eee18b_0 --> conda-forge::zlib-1.2.13-hd590300_5

The following packages will be SUPERSEDED by a higher-priority channel:

  _libgcc_mutex           pkgs/main::_libgcc_mutex-0.1-main --> conda-forge::_libgcc_mutex-0.1-conda_forge
  _openmp_mutex          pkgs/main::_openmp_mutex-5.1-1_gnu --> conda-forge::_openmp_mutex-4.5-2_gnu


Proceed ([y]/n)? y


Downloading and Extracting Packages
rhash-1.4.4          | 181 KB    | ############################################### | 100%
gcc_impl_linux-64-13 | 50.8 MB   | ############################################### | 100%
libev-4.33           | 110 KB    | ############################################### | 100%
libnghttp2-1.57.0    | 674 KB    | ############################################### | 100%
numpy-1.24.4         | 6.4 MB    | ############################################### | 100%
libgcc-ng-13.2.0     | 752 KB    | ############################################### | 100%
libsanitizer-13.2.0  | 3.9 MB    | ############################################### | 100%
libuv-1.47.0         | 872 KB    | ############################################### | 100%
libedit-3.1.20191231 | 121 KB    | ############################################### | 100%
libssh2-1.10.0       | 292 KB    | ############################################### | 100%
sysroot_linux-64-2.1 | 14.6 MB   | ############################################### | 100%
krb5-1.20.1          | 1.3 MB    | ############################################### | 100%
bzip2-1.0.8          | 248 KB    | ############################################### | 100%
_libgcc_mutex-0.1    | 3 KB      | ############################################### | 100%
zstd-1.5.5           | 532 KB    | ############################################### | 100%
keyutils-1.6.1       | 115 KB    | ############################################### | 100%
libboost-headers-1.8 | 13.1 MB   | ############################################### | 100%
ld_impl_linux-64-2.4 | 688 KB    | ############################################### | 100%
libzlib-1.2.13       | 60 KB     | ############################################### | 100%
zlib-1.2.13          | 91 KB     | ############################################### | 100%
libexpat-2.5.0       | 76 KB     | ############################################### | 100%
gcc-13.2.0           | 26 KB     | ############################################### | 100%
libboost-python-1.84 | 116 KB    | ############################################### | 100%
libgcc-devel_linux-6 | 2.5 MB    | ############################################### | 100%
kernel-headers_linux | 692 KB    | ############################################### | 100%
libboost-devel-1.84. | 35 KB     | ############################################### | 100%
libcurl-8.5.0        | 416 KB    | ############################################### | 100%
libboost-python-deve | 16 KB     | ############################################### | 100%
cmake-3.28.3         | 17.9 MB   | ############################################### | 100%
libboost-1.84.0      | 2.6 MB    | ############################################### | 100%
c-ares-1.26.0        | 159 KB    | ############################################### | 100%
boost-1.84.0         | 13 KB     | ############################################### | 100%
libstdcxx-ng-13.2.0  | 3.7 MB    | ############################################### | 100%
libgomp-13.2.0       | 410 KB    | ############################################### | 100%
_openmp_mutex-4.5    | 23 KB     | ############################################### | 100%
binutils_impl_linux- | 5.2 MB    | ############################################### | 100%
icu-73.2             | 11.5 MB   | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(LM) yekyaw.thu@gpu:~/exp/lm$
```

## Installation of KenLM

I got following error:   

```
(LM) yekyaw.thu@gpu:~/exp/lm$ pip install kenlm
Collecting kenlm
  Using cached kenlm-0.2.0.tar.gz (427 kB)
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Building wheels for collected packages: kenlm
  Building wheel for kenlm (pyproject.toml) ... error
  error: subprocess-exited-with-error

  × Building wheel for kenlm (pyproject.toml) did not run successfully.
  │ exit code: 1
  ╰─> [79 lines of output]
      bash: /home/yekyaw.thu/.conda/envs/sentence-transformer/lib/libtinfo.so.6: no version information available (required by bash)
      bash: /home/yekyaw.thu/.conda/envs/sentence-transformer/lib/libtinfo.so.6: no version information available (required by bash)
      bash: /home/yekyaw.thu/.conda/envs/sentence-transformer/lib/libtinfo.so.6: no version information available (required by bash)
      Will build with KenLM max_order set to 6
      running bdist_wheel
      running build
      running build_ext
      CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
        Compatibility with CMake < 3.5 will be removed from a future version of
        CMake.

        Update the VERSION argument <min> value or use a ...<max> suffix to tell
        CMake that the project does not need compatibility with older versions.


      -- The C compiler identification is GNU 13.2.0
      -- The CXX compiler identification is unknown
      -- Detecting C compiler ABI info
      -- Detecting C compiler ABI info - done
      -- Check for working C compiler: /home/yekyaw.thu/.conda/envs/LM/bin/cc - skipped
      -- Detecting C compile features
      -- Detecting C compile features - done
      CMake Error at CMakeLists.txt:14 (project):
        No CMAKE_CXX_COMPILER could be found.

        Tell CMake where to find the compiler by setting either the environment
        variable "CXX" or the CMake cache entry CMAKE_CXX_COMPILER to the full path
        to the compiler, or to the compiler name if it is in the PATH.


      -- Configuring incomplete, errors occurred!
      Traceback (most recent call last):
        File "/home/yekyaw.thu/.conda/envs/LM/lib/python3.8/site-packages/pip/_vendor/pyproject_hooks/_in_process/_in_process.py", line 353, in <module>
          main()
        File "/home/yekyaw.thu/.conda/envs/LM/lib/python3.8/site-packages/pip/_vendor/pyproject_hooks/_in_process/_in_process.py", line 335, in main
          json_out['return_val'] = hook(**hook_input['kwargs'])
        File "/home/yekyaw.thu/.conda/envs/LM/lib/python3.8/site-packages/pip/_vendor/pyproject_hooks/_in_process/_in_process.py", line 251, in build_wheel
          return _build_backend().build_wheel(wheel_directory, config_settings,
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/build_meta.py", line 404, in build_wheel
          return self._build_with_temp_dir(
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/build_meta.py", line 389, in _build_with_temp_dir
          self.run_setup()
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/build_meta.py", line 480, in run_setup
          super(_BuildMetaLegacyBackend, self).run_setup(setup_script=setup_script)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/build_meta.py", line 311, in run_setup
          exec(code, locals())
        File "<string>", line 124, in <module>
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/__init__.py", line 103, in setup
          return distutils.core.setup(**attrs)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 185, in setup
          return run_commands(dist)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/core.py", line 201, in run_commands
          dist.run_commands()
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 969, in run_commands
          self.run_command(cmd)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/dist.py", line 963, in run_command
          super().run_command(command)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/wheel/bdist_wheel.py", line 368, in run
          self.run_command("build")
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
          self.distribution.run_command(command)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/dist.py", line 963, in run_command
          super().run_command(command)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/command/build.py", line 131, in run
          self.run_command(cmd_name)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/cmd.py", line 318, in run_command
          self.distribution.run_command(command)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/dist.py", line 963, in run_command
          super().run_command(command)
        File "/tmp/pip-build-env-qempws8l/overlay/lib/python3.8/site-packages/setuptools/_distutils/dist.py", line 988, in run_command
          cmd_obj.run()
        File "<string>", line 104, in run
        File "/home/yekyaw.thu/.conda/envs/LM/lib/python3.8/subprocess.py", line 364, in check_call
          raise CalledProcessError(retcode, cmd)
      subprocess.CalledProcessError: Command '['cmake', '/tmp/pip-install-nf1rsnq3/kenlm_ca75faa9bb3c4fd0ad6a73f91e8f98ba', '-DCMAKE_LIBRARY_OUTPUT_DIRECTORY=/tmp/pip-install-nf1rsnq3/kenlm_ca75faa9bb3c4fd0ad6a73f91e8f98ba/build/lib.linux-x86_64-cpython-38', '-DBUILD_SHARED_LIBS=ON', '-DBUILD_PYTHON_STANDALONE=ON', '-DKENLM_MAX_ORDER=6', '-DCMAKE_BUILD_TYPE=Release']' returned non-zero exit status 1.
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
  ERROR: Failed building wheel for kenlm
Failed to build kenlm
ERROR: Could not build wheels for kenlm, which is required to install pyproject.toml-based projects
(LM) yekyaw.thu@gpu:~/exp/lm$
```

g++ ကို မတွေ့တာ ...  

## KenLM Installation with GitHub Repository

```
(LM) yekyaw.thu@gpu:~/exp/lm$ git clone https://github.com/kpu/kenlm.git
Cloning into 'kenlm'...
remote: Enumerating objects: 14161, done.
remote: Counting objects: 100% (474/474), done.
remote: Compressing objects: 100% (329/329), done.
remote: Total 14161 (delta 162), reused 406 (delta 131), pack-reused 13687
Receiving objects: 100% (14161/14161), 5.91 MiB | 3.17 MiB/s, done.
Resolving deltas: 100% (8042/8042), done.
(LM) yekyaw.thu@gpu:~/exp/lm$
```

```
(LM) yekyaw.thu@gpu:~/exp/lm$ cd kenlm/
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ ls
BUILDING             compile_query_only.sh  Doxyfile     pyproject.toml  util
clean_query_only.sh  COPYING                LICENSE      python
cmake                COPYING.3              lm           README.md
CMakeLists.txt       COPYING.LESSER.3       MANIFEST.in  setup.py
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$
```

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ mkdir build
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm$ cd build
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$ cmake ..
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 13.2.0
-- The CXX compiler identification is unknown
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /home/yekyaw.thu/.conda/envs/LM/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
CMake Error at CMakeLists.txt:14 (project):
  No CMAKE_CXX_COMPILER could be found.

  Tell CMake where to find the compiler by setting either the environment
  variable "CXX" or the CMake cache entry CMAKE_CXX_COMPILER to the full path
  to the compiler, or to the compiler name if it is in the PATH.


-- Configuring incomplete, errors occurred!
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$
```

## Clean Conda Env and Install Again


```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$ conda update -n base -c defaults conda  
```

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$ conda clean --all
```

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$ conda install -c conda-forge gxx_linux-64
Collecting package metadata (current_repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 24.1.0

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/yekyaw.thu/.conda/envs/LM

  added / updated specs:
    - gxx_linux-64


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    binutils_linux-64-2.40     |       hbdbef99_2          28 KB  conda-forge
    gcc_linux-64-13.2.0        |       h112eaf3_2          30 KB  conda-forge
    gxx_impl_linux-64-13.2.0   |       h338b0a0_5        13.0 MB  conda-forge
    gxx_linux-64-13.2.0        |       hc53e3bf_2          28 KB  conda-forge
    libstdcxx-devel_linux-64-13.2.0|     ha9c7c90_105        12.4 MB  conda-forge
    openssl-3.2.1              |       hd590300_0         2.7 MB  conda-forge
    ------------------------------------------------------------
                                           Total:        28.2 MB

The following NEW packages will be INSTALLED:

  binutils_linux-64  conda-forge/linux-64::binutils_linux-64-2.40-hbdbef99_2
  gcc_linux-64       conda-forge/linux-64::gcc_linux-64-13.2.0-h112eaf3_2
  gxx_impl_linux-64  conda-forge/linux-64::gxx_impl_linux-64-13.2.0-h338b0a0_5
  gxx_linux-64       conda-forge/linux-64::gxx_linux-64-13.2.0-hc53e3bf_2
  libstdcxx-devel_l~ conda-forge/noarch::libstdcxx-devel_linux-64-13.2.0-ha9c7c90_105

The following packages will be UPDATED:

  openssl              pkgs/main::openssl-3.0.13-h7f8727e_0 --> conda-forge::openssl-3.2.1-hd590300_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
libstdcxx-devel_linu | 12.4 MB   | ############################################### | 100%
gxx_linux-64-13.2.0  | 28 KB     | ############################################### | 100%
openssl-3.2.1        | 2.7 MB    | ############################################### | 100%
binutils_linux-64-2. | 28 KB     | ############################################### | 100%
gxx_impl_linux-64-13 | 13.0 MB   | ############################################### | 100%
gcc_linux-64-13.2.0  | 30 KB     | ############################################### | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$

## Install KenLM from Repository Again

I need to rerun cmake again ...  

(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$ cmake ..
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The CXX compiler identification is GNU 13.2.0
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /home/yekyaw.thu/.conda/envs/LM/bin/x86_64-conda-linux-gnu-c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Found Boost: /home/yekyaw.thu/.conda/envs/LM/lib/cmake/Boost-1.84.0/BoostConfig.cmake (found suitable version "1.84.0", minimum required is "1.41.0") found components: program_options system thread unit_test_framework
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- Found Threads: TRUE
-- Found ZLIB: /home/yekyaw.thu/.conda/envs/LM/lib/libz.so (found version "1.2.13")
-- Found BZip2: /home/yekyaw.thu/.conda/envs/LM/lib/libbz2.so (found version "1.0.8")
-- Looking for BZ2_bzCompressInit
-- Looking for BZ2_bzCompressInit - found
-- Looking for lzma_auto_decoder in /home/yekyaw.thu/.conda/envs/LM/lib/liblzma.so
-- Looking for lzma_auto_decoder in /home/yekyaw.thu/.conda/envs/LM/lib/liblzma.so - found
-- Looking for lzma_easy_encoder in /home/yekyaw.thu/.conda/envs/LM/lib/liblzma.so
-- Looking for lzma_easy_encoder in /home/yekyaw.thu/.conda/envs/LM/lib/liblzma.so - found
-- Looking for lzma_lzma_preset in /home/yekyaw.thu/.conda/envs/LM/lib/liblzma.so
-- Looking for lzma_lzma_preset in /home/yekyaw.thu/.conda/envs/LM/lib/liblzma.so - found
-- Found LibLZMA: /home/yekyaw.thu/.conda/envs/LM/lib/liblzma.so (found version "5.4.5")
-- Looking for clock_gettime in rt
-- Looking for clock_gettime in rt - found
-- Found OpenMP_C: -fopenmp (found version "4.5")
-- Found OpenMP_CXX: -fopenmp (found version "4.5")
-- Found OpenMP: TRUE (found version "4.5")
-- Configuring done (1.4s)
-- Generating done (0.0s)
-- Build files have been written to: /home/yekyaw.thu/exp/lm/kenlm/build
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$
```

Run make got 2 errors as follows:    

```
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$ make -j 20
...
...
...
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `memcpy@GLIBC_2.14'
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `clock_gettime@GLIBC_2.17'
collect2: error: ld returned 1 exit status
make[2]: *** [lm/filter/CMakeFiles/filter.dir/build.make:107: bin/filter] Error 1
make[1]: *** [CMakeFiles/Makefile2:541: lm/filter/CMakeFiles/filter.dir/all] Error 2
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `memcpy@GLIBC_2.14'
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `clock_gettime@GLIBC_2.17'
collect2: error: ld returned 1 exit status
make[2]: *** [lm/CMakeFiles/kenlm_benchmark.dir/build.make:106: bin/kenlm_benchmark] Error 1
make[1]: *** [CMakeFiles/Makefile2:404: lm/CMakeFiles/kenlm_benchmark.dir/all] Error 2
make: *** [Makefile:136: all] Error 2
```

Hope it will be OK! ...  

Not OK. and Run again and Error Information is as follows:   

```
/home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/normalize.cc:50:33: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
   50 | struct PtrGreater : public std::binary_function<const BackoffQueueEntry *, const BackoffQueueEntry *, bool> {
      |                                 ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
[ 87%] Linking CXX executable ../../bin/phrase_table_vocab
/home/yekyaw.thu/exp/lm/kenlm/lm/builder/../../util/stream/sort.hh:203:33: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
  203 |     class Greater : public std::binary_function<const Entry &, const Entry &, bool> {
      |                                 ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `memcpy@GLIBC_2.14'
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `clock_gettime@GLIBC_2.17'
collect2: error: ld returned 1 exit status
make[2]: *** [lm/filter/CMakeFiles/phrase_table_vocab.dir/build.make:107: bin/phrase_table_vocab] Error 1
make[1]: *** [CMakeFiles/Makefile2:569: lm/filter/CMakeFiles/phrase_table_vocab.dir/all] Error 2
In file included from /home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/tune_instances.cc:20:
/home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/../common/compare.hh:15:55: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
   15 | template <class Child> class Comparator : public std::binary_function<const void *, const void *, bool> {
      |                                                       ^~~~~~~~~~~~~~~
In file included from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/string:49,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/locale_classes.h:40,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/ios_base.h:41,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/ios:44,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/istream:40,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/sstream:40,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/complex:45,
                 from /usr/include/eigen3/Eigen/Core:96,
                 from /home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/tune_matrix.hh:7,
                 from /home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/tune_instances.hh:4,
                 from /home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/tune_instances.cc:18:
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
/home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/../common/compare.hh:173:69: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
  173 | template <class Range> struct SuffixLexicographicLess : public std::binary_function<const Range, const Range, bool> {
      |                                                                     ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
In file included from /home/yekyaw.thu/exp/lm/kenlm/lm/filter/vocab.hh:6,
                 from /home/yekyaw.thu/exp/lm/kenlm/lm/filter/filter_main.cc:7:
/home/yekyaw.thu/exp/lm/kenlm/lm/filter/../../util/multi_intersection.hh:14:61: warning:
template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
   14 | template <class Range> struct RangeLessBySize : public std::binary_function<const Range &, const Range &, bool> {
      |                                                             ^~~~~~~~~~~~~~~
In file included from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/string:49:
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
In file included from /home/yekyaw.thu/exp/lm/kenlm/lm/filter/vocab.hh:8:
/home/yekyaw.thu/exp/lm/kenlm/lm/filter/../../util/string_piece_hash.hh:24:48: warning: 'template<class _Arg, class _Result> struct std::unary_function' is deprecated [-Wdeprecated-declarations]
   24 | struct StringPieceCompatibleHash : public std::unary_function<const StringPiece &, size_t> {
      |                                                ^~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:117:12: note: declared here
  117 |     struct unary_function
      |            ^~~~~~~~~~~~~~
/home/yekyaw.thu/exp/lm/kenlm/lm/filter/../../util/string_piece_hash.hh:30:50: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
   30 | struct StringPieceCompatibleEquals : public std::binary_function<const StringPiece &, const std::string &, bool> {
      |                                                  ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
In file included from /home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/../../util/stream/sort.hh:29,
                 from /home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/tune_instances.cc:33:
/home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/../../util/stream/../sized_iterator.hh:130:86: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
  130 | template <class Delegate, class Proxy = SizedProxy> class SizedCompare : public std::binary_function<const Proxy &, const Proxy &, bool> {
      |                                                                                      ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
/home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/../../util/stream/../sized_iterator.hh:157:71: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
  157 | template <class Delegate, unsigned Size> class JustPODDelegate : std::binary_function<const JustPOD<Size> &, const JustPOD<Size> &, bool> {
      |                                                                       ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
/home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/../../util/stream/sort.hh:203:33: warning: 'template<class _Arg1, class _Arg2, class _Result> struct std::binary_function' is deprecated [-Wdeprecated-declarations]
  203 |     class Greater : public std::binary_function<const Entry &, const Entry &, bool> {
      |                                 ^~~~~~~~~~~~~~~
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_function.h:131:12: note: declared here
  131 |     struct binary_function
      |            ^~~~~~~~~~~~~~~
In file included from /home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/tune_instances.cc:34:
/home/yekyaw.thu/exp/lm/kenlm/lm/interpolate/../../util/tokenize_piece.hh:99:77: warning:
'template<class _Category, class _Tp, class _Distance, class _Pointer, class _Reference> struct std::iterator' is deprecated [-Wdeprecated-declarations]
   99 | template <class Find, bool SkipEmpty = false> class TokenIter : public std::iterator<std::forward_iterator_tag, const StringPiece, std::ptrdiff_t, const StringPiece *, const StringPiece &> {
      |                                                                             ^~~~~~~~
In file included from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_algobase.h:65,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/specfun.h:43,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/cmath:3699,
                 from /home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/complex:44:
/home/yekyaw.thu/.conda/envs/LM/x86_64-conda-linux-gnu/include/c++/13.2.0/bits/stl_iterator_base_types.h:127:34: note: declared here
  127 |     struct _GLIBCXX17_DEPRECATED iterator
      |                                  ^~~~~~~~
[ 88%] Linking CXX static library ../../lib/libkenlm_builder.a
[ 88%] Built target kenlm_builder
[ 89%] Linking CXX static library ../../lib/libkenlm_interpolate.a
[ 89%] Built target kenlm_interpolate
[ 90%] Linking CXX executable ../../bin/filter
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `memcpy@GLIBC_2.14'
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `clock_gettime@GLIBC_2.17'
collect2: error: ld returned 1 exit status
make[2]: *** [lm/filter/CMakeFiles/filter.dir/build.make:107: bin/filter] Error 1
make[1]: *** [CMakeFiles/Makefile2:541: lm/filter/CMakeFiles/filter.dir/all] Error 2
[ 91%] Linking CXX executable ../bin/kenlm_benchmark
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `memcpy@GLIBC_2.14'
/home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../x86_64-conda-linux-gnu/bin/ld: /home/yekyaw.thu/.conda/envs/LM/bin/../lib/gcc/x86_64-conda-linux-gnu/13.2.0/../../../../lib/liblzma.so: undefined reference to `clock_gettime@GLIBC_2.17'
collect2: error: ld returned 1 exit status
make[2]: *** [lm/CMakeFiles/kenlm_benchmark.dir/build.make:106: bin/kenlm_benchmark] Error 1
make[1]: *** [CMakeFiles/Makefile2:404: lm/CMakeFiles/kenlm_benchmark.dir/all] Error 2
make: *** [Makefile:136: all] Error 2
(LM) yekyaw.thu@gpu:~/exp/lm/kenlm/build$
```

## Finally 

မည်သို့ မည်ပုံ ပြုလုပ်လိုက်သည် မသိ ...  

```
(LM) yekyaw.thu@gpu:~/exp/lm$ pip install https://github.com/kpu/kenlm/archive/master.zip
Collecting https://github.com/kpu/kenlm/archive/master.zip
  Downloading https://github.com/kpu/kenlm/archive/master.zip (553 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 553.6/553.6 kB 495.6 kB/s eta 0:00:00
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Preparing metadata (pyproject.toml) ... done
Building wheels for collected packages: kenlm
  Building wheel for kenlm (pyproject.toml) ... done
  Created wheel for kenlm: filename=kenlm-0.2.0-cp38-cp38-linux_x86_64.whl size=595588 sha256=20ebd3b500fc26b796e57c785e1381d295307d8408037e25c5ef24abc72e2c73
  Stored in directory: /tmp/pip-ephem-wheel-cache-bl3g4iz5/wheels/ff/08/4e/a3ddc0e786e0f3c1fcd2e7a82c4324c02fc3ae2638471406d2
Successfully built kenlm
Installing collected packages: kenlm
Successfully installed kenlm-0.2.0
(LM) yekyaw.thu@gpu:~/exp/lm$
```

Note: တကယ်ကတော့ make clean လုပ်ပြီး နောက်မှာ make -j 20 ပြန် run လိုက်တာမှာ အထက်ပါအတိုင်း pip ကိုသုံးပြီး လုပ်တဲ့ installation က အဆင်ပြေသွားတဲ့ပုံရှိတယ်။  

## Check import KenLM

```
(LM) yekyaw.thu@gpu:~/exp/lm$ python
Python 3.8.18 (default, Sep 11 2023, 13:40:15)
[GCC 11.2.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import kenlm
>>> print(dir(kenlm))
['ARPALoadComplain', 'Config', 'FullScoreReturn', 'LanguageModel', 'LoadMethod', 'Model', 'State', '__builtins__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', '__test__', 'os']
>>> 
```
