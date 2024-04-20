# HS Classification with SVM, NV, CRF

## Library Installation

ရှေ့မှာက xgBoost နဲ့ HS classification ကို လုပ်ကြည့်ခဲ့တယ်။  
အဲဒီ xgboost Anaconda Environment ပေါ်မှာပဲ လိုတဲ့ library တွေကို ထပ် install လုပ်ခဲ့တယ်။   

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ pip install sklearn_crfsuite
Collecting sklearn_crfsuite
  Downloading sklearn_crfsuite-0.3.6-py2.py3-none-any.whl.metadata (3.8 kB)
Collecting python-crfsuite>=0.8.3 (from sklearn_crfsuite)
  Downloading python_crfsuite-0.9.10-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (4.2 kB)
Collecting six (from sklearn_crfsuite)
  Downloading six-1.16.0-py2.py3-none-any.whl.metadata (1.8 kB)
Collecting tabulate (from sklearn_crfsuite)
  Downloading tabulate-0.9.0-py3-none-any.whl.metadata (34 kB)
Collecting tqdm>=2.0 (from sklearn_crfsuite)
  Downloading tqdm-4.66.2-py3-none-any.whl.metadata (57 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 57.6/57.6 kB 631.4 kB/s eta 0:00:00
Downloading sklearn_crfsuite-0.3.6-py2.py3-none-any.whl (12 kB)
Downloading python_crfsuite-0.9.10-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.1 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.1/1.1 MB 5.8 MB/s eta 0:00:00
Downloading tqdm-4.66.2-py3-none-any.whl (78 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 78.3/78.3 kB 960.0 kB/s eta 0:00:00
Downloading six-1.16.0-py2.py3-none-any.whl (11 kB)
Downloading tabulate-0.9.0-py3-none-any.whl (35 kB)
Installing collected packages: python-crfsuite, tqdm, tabulate, six, sklearn_crfsuite
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
google-auth 2.16.0 requires pyasn1-modules>=0.2.1, which is not installed.
tensorboard 2.11.2 requires werkzeug>=1.0.1, which is not installed.
tensorflow 2.11.0 requires typing-extensions>=3.6.6, which is not installed.
Successfully installed python-crfsuite-0.9.10 six-1.16.0 sklearn_crfsuite-0.3.6 tabulate-0.9.0 tqdm-4.66.2
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$
```

## Data Preparation  

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ cp ../xgboost/long-data/ . -r
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ cp ../xgboost/short-data/ . -r
```

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ wc ./long-data/{ltrain,ltest}.txt
   9137  163390 2068583 ./long-data/ltrain.txt
   1000   17880  223453 ./long-data/ltest.txt
  10137  181270 2292036 total
```

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ wc ./short-data/{strain,stest}.txt
  9137  61854 901839 ./short-data/strain.txt
  1000   6725  96170 ./short-data/stest.txt
 10137  68579 998009 total
```

data format example ... 

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ head -n 5 ./long-data/{ltrain,ltest}
.txt
==> ./long-data/ltrain.txt <==
__label__ab လီး တောင် ရိုးရိုး မ ဟုတ် ဘူး တပတ်လည် လီး ပဲ
__label__ab ဆူ စရာ ရှိ လည်း ကွယ်ရာ မှာ ပြော ပါ လား ကွာ စိတ် နု တဲ့ သူ ဆို ရှက် ပြီး သတ်သေ လောက် တယ် တစ် နိုင်ငံ လုံး မြင် အောင် ပြ နေ ကြ တာ မှား ရင် လည်း မှား မယ် အမှား ဆို အမှန် ကို ထောက်ပြ ပေး မှ ဆရာ ဖြစ် မှာ ခု ဟာ က ဆောက်ရှက်ခွဲ နေ တာ
__label__ab သေခါနီး ရိက္ခာ ယူ နေ ကြ တယ် GL
__label__ab အောက်တန်းစား စိတ်ဓာတ် တွေ ဖာဆန် တဲ့ လုပ်ရပ် နဲ့ အတွေး တွေ
__label__no စာအုပ် အဟောင်း သတင်းစာ အဟောင်း ပဲ ကျန် တော့ မှာ ဗျာ ရောင်းစား စရာ က လည်း

==> ./long-data/ltest.txt <==
__label__ab $ရူး ဒိုင် တွေ နဲ့ တော့ ဟူး 🥶🥶🥶🥵🥵🥵
__label__bo ဘာ မ ဟုတ် တာ လို့ ပြော ထွက် တဲ့ ပါးစပ် ပေါက် ရေမြင်းပါးစပ် ကျပ်မပြည့်မ 😒 ငါ ပြော မိ ပြန် ပီ 😔
__label__ab စောက်ကောင်မ မ သိ နဲ့
__label__ab mmsp ပဲ ကိုမေကိုလိုး တွေ တစ်နေကုန် ပျက် လာ တော့ လည်း လာ လိုက် ပျက် လိုက် နဲ့
__label__ab ဘောပြားမကြီး ဟ
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$
```

data format example for short hs dataset ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ head -n 5 ./short-data/{strain,stest
}.txt
==> ./short-data/strain.txt <==
__label__ab လီး တောင် မ လီး ပဲ
__label__ab လောက် ဆောက်ရှက်ခွဲ
__label__ab သေခါနီး
__label__ab အောက်တန်းစား ဖာဆန်
__label__no စာအုပ် အဟောင်း သတင်းစာ အဟောင်း ပဲ ကျန် တော့ မှာ ဗျာ ရောင်းစား စရာ က လည်း

==> ./short-data/stest.txt <==
__label__ab $ရူး
__label__bo မ ပေါက် ရေမြင်းပါးစပ် ကျပ်မပြည့်မ
__label__ab စောက်ကောင်မ မ
__label__ab mmsp ပဲ ကိုမေကိုလိုး
__label__ab ဘောပြားမကြီး
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$
```

## Experiments

Running with word2vec feature ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ ./run-word2vec.sh
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier naive_bayes --eval f1
+ tee long-w2v-nv.log
F1 Score: 0.0963278237645313
Precision: 0.3670059552280218
Recall: 0.088

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.639s
user    0m2.462s
sys     0m0.101s
+ tee long-w2v-rf.log
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier random_forest --eval f1
F1 Score: 0.39357281336549627
Precision: 0.5752920240782544
Recall: 0.512

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m11.522s
user    0m12.338s
sys     0m0.098s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier gradient_boosting --eval f1
+ tee long-w2v-gb.log
F1 Score: 0.39109837349233423
Precision: 0.36473809523809525
Recall: 0.504

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m26.460s
user    5m27.230s
sys     0m0.102s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier svm --eval f1
+ tee long-w2v-svm.log
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m16.007s
user    0m16.745s
sys     0m0.193s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier ensemble --eval f1
+ tee long-w2v-en.log
F1 Score: 0.39448664829011965
Precision: 0.6757298429319372
Recall: 0.538

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m50.069s
user    5m50.732s
sys     0m0.202s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$
```

Running with tf-idf feature ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ ./run-tfidf.sh
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier naive_bayes --eval f1
+ tee long-tfidf-nv.log
F1 Score: 0.1445807801091839
Precision: 0.42824540370151243
Recall: 0.105

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.873s
user    0m0.745s
sys     0m0.129s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier random_forest --eval f1
+ tee long-tfidf-rf.log
F1 Score: 0.41354989600539327
Precision: 0.4635407612712491
Recall: 0.511

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.985s
user    0m6.925s
sys     0m0.060s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier gradient_boosting --eval f1
+ tee long-tfidf-gb.log
F1 Score: 0.4100955386312028
Precision: 0.3744787194185306
Recall: 0.521

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m14.472s
user    0m14.407s
sys     0m0.060s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier svm --eval f1
+ tee long-tfidf-svm.log
F1 Score: 0.40671215715344705
Precision: 0.39687026406429393
Recall: 0.523

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.764s
user    0m3.658s
sys     0m0.106s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier ensemble --eval f1
+ tee long-tfidf-en.log
F1 Score: 0.4145612875218677
Precision: 0.5422201466694502
Recall: 0.531

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m24.302s
user    0m24.047s
sys     0m0.246s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$
```

Running with fastText feature ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ ./run-fasttext.sh
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier naive_bayes --eval f1
+ tee long-ft-nv.log
F1 Score: 0.0578773604892823
Precision: 0.46272552262525607
Recall: 0.071

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.332s
user    0m7.469s
sys     0m0.154s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier random_forest --eval f1
+ tee long-ft-rf.log
F1 Score: 0.3915960307572852
Precision: 0.58879730713246
Recall: 0.519

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m14.476s
user    0m17.497s
sys     0m0.222s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier gradient_boosting --eval f1
+ tee long-ft-gb.log
F1 Score: 0.39507619528241933
Precision: 0.33493112087573235
Recall: 0.514

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m31.296s
user    5m33.970s
sys     0m0.186s
+ tee long-ft-svm.log
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier svm --eval f1
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m18.223s
user    0m21.024s
sys     0m0.272s
+ python 5ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier ensemble --eval f1
+ tee long-ft-en.log
F1 Score: 0.3961165209030033
Precision: 0.6612242571255306
Recall: 0.544

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m56.793s
user    5m59.430s
sys     0m0.341s
+ set +x
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$
```

## Command line Options of Current Code

```
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$ python ./5ml.py --help
usage: 5ml.py [-h] --train_file TRAIN_FILE --test_file TEST_FILE --feature
              {tfidf,word2vec,fasttext} [--stopword_file STOPWORD_FILE]
              --classifier
              {svm,random_forest,gradient_boosting,naive_bayes,ensemble}
              [--eval {f1,error}]

Text Classification with various ML classifiers

optional arguments:
  -h, --help            show this help message and exit
  --train_file TRAIN_FILE
                        Path to training data file
  --test_file TEST_FILE
                        Path to testing data file
  --feature {tfidf,word2vec,fasttext}
                        Text feature type: tfidf, word2vec, or fasttext
  --stopword_file STOPWORD_FILE
                        Path to stopword file (optional)
  --classifier {svm,random_forest,gradient_boosting,naive_bayes,ensemble}
                        Classifier type: svm, random_forest, gradient_boosting,
                        naive_bayes, or ensemble
  --eval {f1,error}     Evaluation metric: f1 or error, default=f1
(xgboost) yekyaw.thu@gpu:~/exp/hs-svm-nv-crf$
```

## Modifying the Code

I wanna combined xgboost methods and see the ensemble results ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ python ./6ml.py --help
usage: 6ml.py [-h] --train_file TRAIN_FILE --test_file TEST_FILE --feature
              {tfidf,word2vec,fasttext} [--stopword_file STOPWORD_FILE]
              --classifier
              {svm,random_forest,gradient_boosting,naive_bayes,xgboost,ensemble}
              [--eval {f1,error}]

Text Classification with various ML classifiers

optional arguments:
  -h, --help            show this help message and exit
  --train_file TRAIN_FILE
                        Path to training data file
  --test_file TEST_FILE
                        Path to testing data file
  --feature {tfidf,word2vec,fasttext}
                        Text feature type: tfidf, word2vec, or fasttext
  --stopword_file STOPWORD_FILE
                        Path to stopword file (optional)
  --classifier {svm,random_forest,gradient_boosting,naive_bayes,xgboost,ensemble}
                        Classifier type: svm, random_forest, gradient_boosting,
                        naive_bayes, xgboost, or ensemble
  --eval {f1,error}     Evaluation metric: f1 or error, default=f1
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

Current updated code:  

(xgboost) yekyaw.thu@gpu:~/exp/6ml$ cat 6ml.py  

```python
"""
for HS Long, Short experiment with 6 ML methods.
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 7 April 2024
Usage: python ./6ml.py --help
"""

import argparse
import numpy as np
import scipy as sp
from sklearn.feature_extraction.text import TfidfVectorizer
from gensim.models import Word2Vec, FastText
from sklearn.metrics import f1_score, precision_score, recall_score, accuracy_score
from sklearn.svm import SVC
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.naive_bayes import GaussianNB
from sklearn.preprocessing import LabelEncoder
import xgboost as xgb

# Function to load Burmese text data
def load_data(file_path):
    texts = []
    labels = []
    label_map = {}
    with open(file_path, 'r', encoding='utf-8') as file:
        for line_no, line in enumerate(file, start=1):
            parts = line.strip().split(' ', 1)
            if len(parts) < 2:
                print(f"Error: Line {line_no} in the file '{file_path}' does not contain both label and text. Skipping...")
                continue
            label = parts[0]
            text = parts[1]
            texts.append(text)
            label = label.split('__label__')[-1].strip()
            if label == "":
                label = "BLANK"
            if label not in label_map:
                label_map[label] = len(label_map)
            labels.append(label_map[label])
    return texts, labels, label_map

# Function to load stop words from file
def load_stopwords(file_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        stopwords = file.read().splitlines()
    return stopwords

# Function to calculate text features
def calculate_features(train_texts, test_texts, train_labels, test_labels, feature_type, stopwords=None):
    if feature_type == 'tfidf':
        vectorizer = TfidfVectorizer(stop_words=stopwords)
        train_features = vectorizer.fit_transform(train_texts)
        test_features = vectorizer.transform(test_texts)
    elif feature_type == 'word2vec':
        word2vec_model = Word2Vec(sentences=[text.split() for text in train_texts], vector_size=100, window=5, min_count=1, workers=4)
        train_features = np.array([np.mean([word2vec_model.wv[word] for word in text.split() if word in word2vec_model.wv] or [np.zeros(100)], axis=0) for text in train_texts])
        test_features = np.array([np.mean([word2vec_model.wv[word] for word in text.split() if word in word2vec_model.wv] or [np.zeros(100)], axis=0) for text in test_texts])
    elif feature_type == 'fasttext':
        fasttext_model = FastText(sentences=[text.split() for text in train_texts], vector_size=100, window=5, min_count=1, workers=4)
        train_features = np.array([np.mean([fasttext_model.wv[word] for word in text.split() if word in fasttext_model.wv] or [np.zeros(100)], axis=0) for text in train_texts])
        test_features = np.array([np.mean([fasttext_model.wv[word] for word in text.split() if word in fasttext_model.wv] or [np.zeros(100)], axis=0) for text in test_texts])
    else:
        raise ValueError("Invalid feature type. Choose from 'tfidf', 'word2vec', or 'fasttext'.")

    # Convert labels to list of lists format
    train_labels_nested = [[label] for label in train_labels]
    test_labels_nested = [[label] for label in test_labels]

    return train_features, test_features, train_labels_nested, test_labels_nested

def train_evaluate_model(train_features, train_labels, test_features, test_labels, classifier_type, eval_metric, label_map):
    if classifier_type == 'svm':
        classifier = SVC(kernel='linear')
    elif classifier_type == 'random_forest':
        classifier = RandomForestClassifier()
    elif classifier_type == 'gradient_boosting':
        classifier = GradientBoostingClassifier()
    elif classifier_type == 'naive_bayes':
        if isinstance(train_features, sp.sparse.spmatrix):
            train_features = train_features.toarray()
            test_features = test_features.toarray()
        classifier = GaussianNB()
    elif classifier_type == 'xgboost':
        classifier = xgb.XGBClassifier()
    elif classifier_type == 'ensemble':
        svm_pred = SVC(kernel='linear').fit(train_features, np.ravel(train_labels)).predict(test_features)
        rf_pred = RandomForestClassifier().fit(train_features, np.ravel(train_labels)).predict(test_features)
        gb_pred = GradientBoostingClassifier().fit(train_features, np.ravel(train_labels)).predict(test_features)
        nb_pred = GaussianNB().fit(train_features, np.ravel(train_labels)).predict(test_features)
        xgb_pred = xgb.XGBClassifier().fit(train_features, np.ravel(train_labels)).predict(test_features)
        pred_labels = np.array([svm_pred, rf_pred, gb_pred, nb_pred, xgb_pred])
        ensemble_pred = np.apply_along_axis(lambda x: np.argmax(np.bincount(x)), axis=0, arr=pred_labels)
        return ensemble_pred
    else:
        raise ValueError("Invalid classifier type. Choose from 'svm', 'random_forest', 'gradient_boosting', 'naive_bayes', 'xgboost', or 'ensemble'.")

    classifier.fit(train_features, np.ravel(train_labels))
    pred_labels = classifier.predict(test_features)
    return pred_labels

def main(args):
    train_texts, train_labels, label_map = load_data(args.train_file)
    test_texts, test_labels, _ = load_data(args.test_file)
    stopwords = None
    if args.stopword_file:
        stopwords = load_stopwords(args.stopword_file)
    train_features, test_features, train_labels_nested, test_labels_nested = calculate_features(train_texts, test_texts, train_labels, test_labels, args.feature, stopwords)
    pred_labels = train_evaluate_model(train_features, train_labels_nested, test_features, test_labels_nested, args.classifier, args.eval, label_map)
    if args.eval == 'f1':
        f1 = f1_score(test_labels, pred_labels, average='weighted')
        precision = precision_score(test_labels, pred_labels, average='weighted', zero_division=1)
        recall = recall_score(test_labels, pred_labels, average='weighted')
        print(f"F1 Score: {f1}")
        print(f"Precision: {precision}")
        print(f"Recall: {recall}")
    elif args.eval == 'error':
        error_rate = 1.0 - accuracy_score(test_labels, pred_labels)
        print(f"Error Rate: {error_rate}")
    print("\nNumeric Label - Original Label")
    for numeric_label, text_label in label_map.items():
        print(f"{numeric_label} - {text_label}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Text Classification with various ML classifiers')
    parser.add_argument('--train_file', type=str, help='Path to training data file', required=True)
    parser.add_argument('--test_file', type=str, help='Path to testing data file', required=True)
    parser.add_argument('--feature', type=str, help='Text feature type: tfidf, word2vec, or fasttext', choices=['tfidf', 'word2vec', 'fasttext'], required=True)
    parser.add_argument('--stopword_file', type=str, help='Path to stopword file (optional)', default=None)
    parser.add_argument('--classifier', type=str, help='Classifier type: svm, random_forest, gradient_boosting, naive_bayes, xgboost, or ensemble', choices=['svm', 'random_forest', 'gradient_boosting', 'naive_bayes', 'xgboost', 'ensemble'], required=True)
    parser.add_argument('--eval', type=str, help='Evaluation metric: f1 or error, default=f1', choices=['f1', 'error'], default='f1')
    args = parser.parse_args()
    main(args)

```

## Experiment with 6ML 
  
--feature tf-idf အတွက် approach ခြောက်မျိုးရဲ့ ရလဒ်က အောက်ပါအတိုင်းပါ။  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-tfidf.sh
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier naive_bayes --eval f1
+ tee long-tfidf-nv.log
F1 Score: 0.1445807801091839
Precision: 0.42824540370151243
Recall: 0.105

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.873s
user    0m0.745s
sys     0m0.128s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier random_forest --eval f1
+ tee long-tfidf-rf.log
F1 Score: 0.4187995389182376
Precision: 0.46771190091767306
Recall: 0.513

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.888s
user    0m6.816s
sys     0m0.072s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier gradient_boosting --eval f1
+ tee long-tfidf-gb.log
F1 Score: 0.41235146701299313
Precision: 0.385972293508812
Recall: 0.521

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m14.957s
user    0m14.895s
sys     0m0.056s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier svm --eval f1
+ tee long-tfidf-svm.log
F1 Score: 0.40671215715344705
Precision: 0.39687026406429393
Recall: 0.523

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.678s
user    0m3.578s
sys     0m0.100s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier xgboost --eval f1
+ tee long-tfidf-xg.log
F1 Score: 0.42302645952482565
Precision: 0.3813030902713106
Recall: 0.523

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m7.000s
user    2m9.396s
sys     0m5.724s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier ensemble --eval f1
+ tee long-tfidf-en.log

F1 Score: 0.3966806690929452
Precision: 0.5888337442999493
Recall: 0.54

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    6m6.095s
user    8m59.944s
sys     0m7.639s
+ set +x

real    6m39.494s
user    11m35.374s
sys     0m13.722s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

Run word2vec and the results is as follows ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-word2vec.sh
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier naive_bayes --eval f1
+ tee long-w2v-nv.log
F1 Score: 0.10134604789315642
Precision: 0.3880013535748953
Recall: 0.091

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.739s
user    0m2.584s
sys     0m0.097s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier random_forest --eval f1
+ tee long-w2v-rf.log
F1 Score: 0.3912822260875222
Precision: 0.591213107883208
Recall: 0.513

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m11.961s
user    0m12.821s
sys     0m0.094s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier gradient_boosting --eval f1
+ tee long-w2v-gb.log
F1 Score: 0.3959964769777223
Precision: 0.4117332049393905
Recall: 0.507

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m34.682s
user    5m35.371s
sys     0m0.120s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier svm --eval f1
+ tee long-w2v-svm.log
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m15.923s
user    0m16.721s
sys     0m0.180s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier xgboost --eval f1
+ tee long-w2v-xg.log
F1 Score: 0.3987736126801547
Precision: 0.5798533681710213
Recall: 0.504

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m10.021s
user    2m52.446s
sys     0m6.625s
+ tee long-w2v-en.log
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier ensemble --eval f1
F1 Score: 0.39525898416215843
Precision: 0.6643081611022787
Recall: 0.525

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    6m5.218s
user    9m1.462s
sys     0m7.671s
+ set +x

real    12m19.546s
user    18m1.406s
sys     0m14.790s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

Run --feature fasttext and the results are as follows ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-fasttext.sh
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier naive_bayes --eval f1
+ tee long-ft-nv.log
F1 Score: 0.05802372194564271
Precision: 0.4113340584448931
Recall: 0.059

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.447s
user    0m7.526s
sys     0m0.197s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier random_forest --eval f1
+ tee long-ft-rf.log
F1 Score: 0.3937680735453931
Precision: 0.5728646581475609
Recall: 0.519

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m14.394s
user    0m17.493s
sys     0m0.204s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier gradient_boosting --eval f1
+ tee long-ft-gb.log
F1 Score: 0.3965407862524935
Precision: 0.3858347061493079
Recall: 0.519

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m34.197s
user    5m36.943s
sys     0m0.214s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier svm --eval f1
+ tee long-ft-svm.log
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m19.564s
user    0m22.403s
sys     0m0.230s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier xgboost --eval f1
+ tee long-ft-xg.log
F1 Score: 0.4006935479740554
Precision: 0.5633777647530617
Recall: 0.503

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m11.578s
user    2m31.443s
sys     0m5.317s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier ensemble --eval f1
+ tee long-ft-en.log
F1 Score: 0.3974672650438306
Precision: 0.6780947875277796
Recall: 0.543

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    6m5.328s
user    8m53.028s
sys     0m7.415s
+ set +x

real    12m29.511s
user    17m48.837s
sys     0m13.576s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

## The Ensemble Approach Explanation

စာတမ်းမှာ ရှင်းပြဖို့အတွက်လည်း အသုံးဝင်လိမ့်မယ် ...  

```
In the given code, the ensemble method combines predictions from five different classifiers: Support Vector Machine (SVM), Random Forest, Gradient Boosting, Naive Bayes (NB), and XGBoost. Here's how the ensemble method works in detail based on your code and library usage:

Training the Base Classifiers: Initially, each of the five base classifiers (SVM, Random Forest, Gradient Boosting, Naive Bayes, XGBoost) is trained independently using the training data.

Obtaining Predictions: After training, each classifier makes predictions on the test data.

Combining Predictions: Once the predictions are obtained from each classifier, the ensemble method combines these predictions to produce a final prediction. The ensemble method used here is a simple majority voting scheme.

For each data point in the test set, the prediction made by each of the five classifiers is obtained.

Then, for each data point, the most common prediction among the five classifiers is chosen as the final prediction. This is achieved using np.apply_along_axis function to apply the argmax(np.bincount(x)) function across the predictions of the five classifiers.

Returning Final Prediction: The final prediction obtained through the ensemble method is returned as the output.

Regarding the weights assigned to each base classifier, your current approach doesn't explicitly assign weights. Instead, it gives equal importance to each classifier by simply counting the votes (predictions) from each model and selecting the most common prediction.

If you want to assign different weights to different classifiers in your ensemble, you could modify the approach to incorporate weighted voting. This would involve assigning a weight to each classifier's prediction, and then combining these weighted predictions to generate the final ensemble prediction. However, in your current implementation, each classifier has equal weight in the final decision.
```

## Re-run and Make Confirmation  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-tfidf.sh
+ tee long-tfidf-nv.log
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier naive_bayes --eval f1
F1 Score: 0.1445807801091839
Precision: 0.42824540370151243
Recall: 0.105

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m0.908s
user    0m0.768s
sys     0m0.141s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier random_forest --eval f1
+ tee long-tfidf-rf.log
F1 Score: 0.41509173140146116
Precision: 0.4310555612000025
Recall: 0.512

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.967s
user    0m6.875s
sys     0m0.092s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier gradient_boosting --eval f1
+ tee long-tfidf-gb.log
F1 Score: 0.41125481691325505
Precision: 0.3924137969271166
Recall: 0.522

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m14.576s
user    0m14.488s
sys     0m0.082s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier svm --eval f1
+ tee long-tfidf-svm.log
F1 Score: 0.40671215715344705
Precision: 0.39687026406429393
Recall: 0.523

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m3.656s
user    0m3.539s
sys     0m0.118s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature tfidf --classifier xgboost --eval f1
+ tee long-tfidf-xg.log
F1 Score: 0.42302645952482565
Precision: 0.3813030902713106
Recall: 0.523

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m9.677s
user    3m3.516s
sys     0m8.787s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier ensemble --eval f1
+ tee long-tfidf-en.log
F1 Score: 0.3970542598054894
Precision: 0.5668857367668098
Recall: 0.532

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    6m6.307s
user    9m53.968s
sys     0m10.063s
+ set +x

real    6m42.093s
user    13m23.155s
sys     0m19.282s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

with --feature word2vec  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-word2vec.sh
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier naive_bayes --eval f1
+ tee long-w2v-nv.log
F1 Score: 0.09025233784690216
Precision: 0.37980092639777707
Recall: 0.086

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.701s
user    0m2.560s
sys     0m0.088s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier random_forest --eval f1
+ tee long-w2v-rf.log
F1 Score: 0.3950574099298059
Precision: 0.6661568011958147
Recall: 0.516

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m11.644s
user    0m12.501s
sys     0m0.128s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier gradient_boosting --eval f1
+ tee long-w2v-gb.log
F1 Score: 0.3942964269867469
Precision: 0.3720251428571428
Recall: 0.508

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m29.387s
user    5m30.113s
sys     0m0.100s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier svm --eval f1
+ tee long-w2v-svm.log
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m15.795s
user    0m16.575s
sys     0m0.138s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier xgboost --eval f1
+ tee long-w2v-xg.log
F1 Score: 0.38799593532249427
Precision: 0.5589782062953461
Recall: 0.493

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m11.664s
user    3m24.330s
sys     0m8.119s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature word2vec --classifier ensemble --eval f1
+ tee long-w2v-en.log
F1 Score: 0.39542296057128734
Precision: 0.6613761762509336
Recall: 0.529

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    6m10.649s
user    10m3.440s
sys     0m10.934s
+ set +x

real    12m20.841s
user    19m29.518s
sys     0m19.511s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

with --feature fasttext  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-fasttext.sh
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier naive_bayes --eval f1
+ tee long-ft-nv.log
F1 Score: 0.04440650163397616
Precision: 0.4380366449821293
Recall: 0.055

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.370s
user    0m7.371s
sys     0m0.176s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier random_forest --eval f1
+ tee long-ft-rf.log
F1 Score: 0.39303442471093303
Precision: 0.5542936245966696
Recall: 0.521

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m14.154s
user    0m16.990s
sys     0m0.220s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier gradient_boosting --eval f1
+ tee long-ft-gb.log
F1 Score: 0.3995349724879961
Precision: 0.3740762596983069
Recall: 0.515

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m30.772s
user    5m33.568s
sys     0m0.210s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier svm --eval f1
+ tee long-ft-svm.log
F1 Score: 0.3891555842479019
Precision: 0.7524010000000001
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m18.381s
user    0m21.167s
sys     0m0.330s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier xgboost --eval f1
+ tee long-ft-xg.log
F1 Score: 0.3903405221851717
Precision: 0.5467904700309985
Recall: 0.502

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m14.408s
user    3m33.871s
sys     0m8.534s
+ python 6ml.py --train_file ./long-data/ltrain.txt --test_file ./long-data/ltest.txt --feature fasttext --classifier ensemble --eval f1
+ tee long-ft-en.log
F1 Score: 0.3923618367140473
Precision: 0.6508327526132405
Recall: 0.531

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    6m1.338s
user    8m26.146s
sys     0m6.063s
+ set +x

real    12m23.425s
user    18m19.115s
sys     0m15.533s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

## Code (9 April 2024 Version)  

(base) yekyaw.thu@gpu:~/exp/6ml$ cat 6ml.py  

```python
"""
for HS Long, Short experiment with 6 ML methods.
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 7 April 2024
Usage: python ./6ml.py --help
"""

import argparse
import numpy as np
import scipy as sp
from sklearn.feature_extraction.text import TfidfVectorizer
from gensim.models import Word2Vec, FastText
from sklearn.metrics import f1_score, precision_score, recall_score, accuracy_score
from sklearn.svm import SVC
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.naive_bayes import GaussianNB
from sklearn.preprocessing import LabelEncoder
import xgboost as xgb

# Function to load Burmese text data
def load_data(file_path):
    texts = []
    labels = []
    label_map = {}
    with open(file_path, 'r', encoding='utf-8') as file:
        for line_no, line in enumerate(file, start=1):
            parts = line.strip().split(' ', 1)
            if len(parts) < 2:
                print(f"Error: Line {line_no} in the file '{file_path}' does not contain both label and text. Skipping...")
                continue
            label = parts[0]
            text = parts[1]
            texts.append(text)
            label = label.split('__label__')[-1].strip()
            if label == "":
                label = "BLANK"
            if label not in label_map:
                label_map[label] = len(label_map)
            labels.append(label_map[label])
    return texts, labels, label_map

# Function to load stop words from file
def load_stopwords(file_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        stopwords = file.read().splitlines()
    return stopwords

# Function to calculate text features
def calculate_features(train_texts, test_texts, train_labels, test_labels, feature_type, stopwords=None):
    if feature_type == 'tfidf':
        vectorizer = TfidfVectorizer(stop_words=stopwords)
        train_features = vectorizer.fit_transform(train_texts)
        test_features = vectorizer.transform(test_texts)
    elif feature_type == 'word2vec':
        word2vec_model = Word2Vec(sentences=[text.split() for text in train_texts], vector_size=100, window=5, min_count=1, workers=4)
        train_features = np.array([np.mean([word2vec_model.wv[word] for word in text.split() if word in word2vec_model.wv] or [np.zeros(100)], axis=0) for text in train_texts])
        test_features = np.array([np.mean([word2vec_model.wv[word] for word in text.split() if word in word2vec_model.wv] or [np.zeros(100)], axis=0) for text in test_texts])
    elif feature_type == 'fasttext':
        fasttext_model = FastText(sentences=[text.split() for text in train_texts], vector_size=100, window=5, min_count=1, workers=4)
        train_features = np.array([np.mean([fasttext_model.wv[word] for word in text.split() if word in fasttext_model.wv] or [np.zeros(100)], axis=0) for text in train_texts])
        test_features = np.array([np.mean([fasttext_model.wv[word] for word in text.split() if word in fasttext_model.wv] or [np.zeros(100)], axis=0) for text in test_texts])
    else:
        raise ValueError("Invalid feature type. Choose from 'tfidf', 'word2vec', or 'fasttext'.")

    # Convert labels to list of lists format
    train_labels_nested = [[label] for label in train_labels]
    test_labels_nested = [[label] for label in test_labels]

    return train_features, test_features, train_labels_nested, test_labels_nested

def train_evaluate_model(train_features, train_labels, test_features, test_labels, classifier_type, eval_metric, label_map):
    if classifier_type == 'svm':
        classifier = SVC(kernel='linear')
    elif classifier_type == 'random_forest':
        classifier = RandomForestClassifier()
    elif classifier_type == 'gradient_boosting':
        classifier = GradientBoostingClassifier()
    elif classifier_type == 'naive_bayes':
        if isinstance(train_features, sp.sparse.spmatrix):
            train_features = train_features.toarray()
            test_features = test_features.toarray()
        classifier = GaussianNB()
    elif classifier_type == 'xgboost':
        classifier = xgb.XGBClassifier()
    elif classifier_type == 'ensemble':
        svm_pred = SVC(kernel='linear').fit(train_features, np.ravel(train_labels)).predict(test_features)
        rf_pred = RandomForestClassifier().fit(train_features, np.ravel(train_labels)).predict(test_features)
        gb_pred = GradientBoostingClassifier().fit(train_features, np.ravel(train_labels)).predict(test_features)
        nb_pred = GaussianNB().fit(train_features, np.ravel(train_labels)).predict(test_features)
        xgb_pred = xgb.XGBClassifier().fit(train_features, np.ravel(train_labels)).predict(test_features)
        pred_labels = np.array([svm_pred, rf_pred, gb_pred, nb_pred, xgb_pred])
        ensemble_pred = np.apply_along_axis(lambda x: np.argmax(np.bincount(x)), axis=0, arr=pred_labels)
        return ensemble_pred
    else:
        raise ValueError("Invalid classifier type. Choose from 'svm', 'random_forest', 'gradient_boosting', 'naive_bayes', 'xgboost', or 'ensemble'.")

    classifier.fit(train_features, np.ravel(train_labels))
    pred_labels = classifier.predict(test_features)
    return pred_labels

def main(args):
    train_texts, train_labels, label_map = load_data(args.train_file)
    test_texts, test_labels, _ = load_data(args.test_file)
    stopwords = None
    if args.stopword_file:
        stopwords = load_stopwords(args.stopword_file)
    train_features, test_features, train_labels_nested, test_labels_nested = calculate_features(train_texts, test_texts, train_labels, test_labels, args.feature, stopwords)
    pred_labels = train_evaluate_model(train_features, train_labels_nested, test_features, test_labels_nested, args.classifier, args.eval, label_map)
    if args.eval == 'f1':
        f1 = f1_score(test_labels, pred_labels, average='weighted')
        precision = precision_score(test_labels, pred_labels, average='weighted', zero_division=1)
        recall = recall_score(test_labels, pred_labels, average='weighted')
        print(f"F1 Score: {f1}")
        print(f"Precision: {precision}")
        print(f"Recall: {recall}")
    elif args.eval == 'error':
        error_rate = 1.0 - accuracy_score(test_labels, pred_labels)
        print(f"Error Rate: {error_rate}")
    print("\nNumeric Label - Original Label")
    for numeric_label, text_label in label_map.items():
        print(f"{numeric_label} - {text_label}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Text Classification with various ML classifiers')
    parser.add_argument('--train_file', type=str, help='Path to training data file', required=True)
    parser.add_argument('--test_file', type=str, help='Path to testing data file', required=True)
    parser.add_argument('--feature', type=str, help='Text feature type: tfidf, word2vec, or fasttext', choices=['tfidf', 'word2vec', 'fasttext'], required=True)
    parser.add_argument('--stopword_file', type=str, help='Path to stopword file (optional)', default=None)
    parser.add_argument('--classifier', type=str, help='Classifier type: svm, random_forest, gradient_boosting, naive_bayes, xgboost, or ensemble', choices=['svm', 'random_forest', 'gradient_boosting', 'naive_bayes', 'xgboost', 'ensemble'], required=True)
    parser.add_argument('--eval', type=str, help='Evaluation metric: f1 or error, default=f1', choices=['f1', 'error'], default='f1')
    args = parser.parse_args()
    main(args)

```

--help screen ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ python ./6ml.py --help
usage: 6ml.py [-h] --train_file TRAIN_FILE --test_file TEST_FILE --feature
              {tfidf,word2vec,fasttext} [--stopword_file STOPWORD_FILE]
              --classifier
              {svm,random_forest,gradient_boosting,naive_bayes,xgboost,ensemble}
              [--eval {f1,error}]

Text Classification with various ML classifiers

optional arguments:
  -h, --help            show this help message and exit
  --train_file TRAIN_FILE
                        Path to training data file
  --test_file TEST_FILE
                        Path to testing data file
  --feature {tfidf,word2vec,fasttext}
                        Text feature type: tfidf, word2vec, or fasttext
  --stopword_file STOPWORD_FILE
                        Path to stopword file (optional)
  --classifier {svm,random_forest,gradient_boosting,naive_bayes,xgboost,ensemble}
                        Classifier type: svm, random_forest, gradient_boosting,
                        naive_bayes, xgboost, or ensemble
  --eval {f1,error}     Evaluation metric: f1 or error, default=f1
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

## Shell Scripts for LONG HS  

(xgboost) yekyaw.thu@gpu:~/exp/6ml$ cat ./run-tfidf.sh   

```bash
#!/bin/bash

## feature: tf-idf
## naive_bayes, random_forest, gradient_boosting, svm, xgboost or ensemble
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 7 April 2024

set -x;
time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf \
--classifier naive_bayes --eval f1 | tee long-tfidf-nv.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf \
--classifier random_forest --eval f1 | tee long-tfidf-rf.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf \
--classifier gradient_boosting --eval f1 | tee long-tfidf-gb.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf \
--classifier svm --eval f1 | tee long-tfidf-svm.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature tfidf \
--classifier xgboost --eval f1 | tee long-tfidf-xg.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext \
--classifier ensemble --eval f1 | tee long-tfidf-en.log
set +x;
```

(xgboost) yekyaw.thu@gpu:~/exp/6ml$ cat ./run-word2vec.sh  

```bash
#!/bin/bash

## feature: word2vec
## naive_bayes, random_forest, gradient_boosting, svm, xgboost or ensemble
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last Updated: 7 April 2024

set -x;
time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec \
--classifier naive_bayes --eval f1 | tee long-w2v-nv.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec \
--classifier random_forest --eval f1 | tee long-w2v-rf.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec \
--classifier gradient_boosting --eval f1 | tee long-w2v-gb.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec \
--classifier svm --eval f1 | tee long-w2v-svm.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec \
--classifier xgboost --eval f1 | tee long-w2v-xg.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature word2vec \
--classifier ensemble --eval f1 | tee long-w2v-en.log
set +x;
```

(xgboost) yekyaw.thu@gpu:~/exp/6ml$ cat ./run-fasttext.sh  

```bash
#!/bin/bash

## feature: fasttext
## naive_bayes, random_forest, gradient_boosting, svm, xgboost or ensemble
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated 7 April 2024

set -x;
time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext \
--classifier naive_bayes --eval f1 | tee long-ft-nv.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext \
--classifier random_forest --eval f1 | tee long-ft-rf.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext \
--classifier gradient_boosting --eval f1 | tee long-ft-gb.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext \
--classifier svm --eval f1 | tee long-ft-svm.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext \
--classifier xgboost --eval f1 | tee long-ft-xg.log

time python 6ml.py --train_file ./long-data/ltrain.txt \
--test_file ./long-data/ltest.txt --feature fasttext \
--classifier ensemble --eval f1 | tee long-ft-en.log

set +x;
```

## LONG Results in Graphs  

```
| Feature    | Classifier         | F1 Score | Precision | Recall |
|------------|--------------------|----------|-----------|--------|
| TF-IDF     | Naive Bayes        | 0.144    | 0.428     | 0.105  |
| TF-IDF     | Random Forest      | 0.415    | 0.431     | 0.512  |
| TF-IDF     | Gradient Boosting  | 0.411    | 0.392     | 0.522  |
| TF-IDF     | SVM                | 0.407    | 0.397     | 0.523  |
| TF-IDF     | XGBoost            | 0.423    | 0.381     | 0.523  |
| TF-IDF     | Ensemble           | 0.397    | 0.567     | 0.532  |
| Word2Vec   | Naive Bayes        | 0.090    | 0.380     | 0.086  |
| Word2Vec   | Random Forest      | 0.395    | 0.666     | 0.516  |
| Word2Vec   | Gradient Boosting  | 0.394    | 0.372     | 0.508  |
| Word2Vec   | SVM                | 0.389    | 0.752     | 0.549  |
| Word2Vec   | XGBoost            | 0.388    | 0.559     | 0.493  |
| Word2Vec   | Ensemble           | 0.395    | 0.661     | 0.529  |
| FastText   | Naive Bayes        | 0.044    | 0.438     | 0.055  |
| FastText   | Random Forest      | 0.393    | 0.554     | 0.521  |
| FastText   | Gradient Boosting  | 0.400    | 0.374     | 0.515  |
| FastText   | SVM                | 0.389    | 0.752     | 0.549  |
| FastText   | XGBoost            | 0.390    | 0.547     | 0.502  |
| FastText   | Ensemble           | 0.392    | 0.651     | 0.531  |
```

table သုံးခုအနေနဲ့ ခွဲဆွဲကြည့် ...  

```

### TF-IDF:

| Classifier         | F1 Score | Precision | Recall |
|--------------------|----------|-----------|--------|
| Naive Bayes        | 0.144    | 0.428     | 0.105  |
| Random Forest      | 0.415    | 0.431     | 0.512  |
| Gradient Boosting  | 0.411    | 0.392     | 0.522  |
| SVM                | 0.407    | 0.397     | 0.523  |
| XGBoost            | 0.423    | 0.381     | 0.523  |
| Ensemble           | 0.397    | 0.567     | 0.532  |

### Word2Vec:

| Classifier         | F1 Score | Precision | Recall |
|--------------------|----------|-----------|--------|
| Naive Bayes        | 0.090    | 0.380     | 0.086  |
| Random Forest      | 0.395    | 0.666     | 0.516  |
| Gradient Boosting  | 0.394    | 0.372     | 0.508  |
| SVM                | 0.389    | 0.752     | 0.549  |
| XGBoost            | 0.388    | 0.559     | 0.493  |
| Ensemble           | 0.395    | 0.661     | 0.529  |

### FastText:

| Classifier         | F1 Score | Precision | Recall |
|--------------------|----------|-----------|--------|
| Naive Bayes        | 0.044    | 0.438     | 0.055  |
| Random Forest      | 0.393    | 0.554     | 0.521  |
| Gradient Boosting  | 0.400    | 0.374     | 0.515  |
| SVM                | 0.389    | 0.752     | 0.549  |
| XGBoost            | 0.390    | 0.547     | 0.502  |
| Ensemble           | 0.392    | 0.651     | 0.531  |

```


## LONG Results with Latex Format  

for tf-idf ...  

```
\begin{table}[h]
\centering
\caption{Performance Metrics for TF-IDF Feature Extraction}
\label{tab:tfidf}
\begin{tabular}{|c|c|c|c|}
\hline
Classifier         & F1 Score & Precision & Recall \\
\hline
Naive Bayes        & 0.144    & 0.428     & 0.105  \\
Random Forest      & 0.415    & 0.431     & 0.512  \\
Gradient Boosting  & 0.411    & 0.392     & 0.522  \\
SVM                & 0.407    & 0.397     & 0.523  \\
XGBoost            & 0.423    & 0.381     & 0.523  \\
Ensemble           & 0.397    & 0.567     & 0.532  \\
\hline
\end{tabular}
\end{table}

```

for word2vec ...  

```
\begin{table}[h]
\centering
\caption{Performance Metrics for Word2Vec Feature Extraction}
\label{tab:word2vec}
\begin{tabular}{|c|c|c|c|}
\hline
Classifier         & F1 Score & Precision & Recall \\
\hline
Naive Bayes        & 0.090    & 0.380     & 0.086  \\
Random Forest      & 0.395    & 0.666     & 0.516  \\
Gradient Boosting  & 0.394    & 0.372     & 0.508  \\
SVM                & 0.389    & 0.752     & 0.549  \\
XGBoost            & 0.388    & 0.559     & 0.493  \\
Ensemble           & 0.395    & 0.661     & 0.529  \\
\hline
\end{tabular}
\end{table}

```

for fasttext ...  

```
\begin{table}[h]
\centering
\caption{Performance Metrics for FastText Feature Extraction}
\label{tab:fasttext}
\begin{tabular}{|c|c|c|c|}
\hline
Classifier         & F1 Score & Precision & Recall \\
\hline
Naive Bayes        & 0.044    & 0.438     & 0.055  \\
Random Forest      & 0.393    & 0.554     & 0.521  \\
Gradient Boosting  & 0.400    & 0.374     & 0.515  \\
SVM                & 0.389    & 0.752     & 0.549  \\
XGBoost            & 0.390    & 0.547     & 0.502  \\
Ensemble           & 0.392    & 0.651     & 0.531  \\
\hline
\end{tabular}
\end{table}

```

## Preparing Shell Scripts for SHORT HS  

for tf-idf ...  
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ cat ./run-tfidf-short.sh  

```bash
#!/bin/bash

## for short HS
## feature: tf-idf
## naive_bayes, random_forest, gradient_boosting, svm, xgboost or ensemble
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 9 April 2024

set -x;
time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature tfidf \
--classifier naive_bayes --eval f1 | tee short-tfidf-nv.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature tfidf \
--classifier random_forest --eval f1 | tee short-tfidf-rf.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature tfidf \
--classifier gradient_boosting --eval f1 | tee short-tfidf-gb.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature tfidf \
--classifier svm --eval f1 | tee short-tfidf-svm.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature tfidf \
--classifier xgboost --eval f1 | tee short-tfidf-xg.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--classifier ensemble --eval f1 | tee short-tfidf-en.log
set +x;
```

for word2vec ...  
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ cat run-word2vec-short.sh  

```bash
#!/bin/bash

## for short hs
## feature: word2vec
## naive_bayes, random_forest, gradient_boosting, svm, xgboost or ensemble
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last Updated: 9 April 2024

set -x;
time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature word2vec \
--classifier naive_bayes --eval f1 | tee short-w2v-nv.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature word2vec \
--classifier random_forest --eval f1 | tee short-w2v-rf.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature word2vec \
--classifier gradient_boosting --eval f1 | tee short-w2v-gb.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature word2vec \
--classifier svm --eval f1 | tee short-w2v-svm.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature word2vec \
--classifier xgboost --eval f1 | tee short-w2v-xg.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature word2vec \
--classifier ensemble --eval f1 | tee short-w2v-en.log
set +x;
```

for fasttext ...  
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ cat run-fasttext-short.sh  

```bash

#!/bin/bash

## for short hs
## feature: fasttext
## naive_bayes, random_forest, gradient_boosting, svm, xgboost or ensemble
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated 9 April 2024

set -x;
time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--classifier naive_bayes --eval f1 | tee short-ft-nv.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--classifier random_forest --eval f1 | tee short-ft-rf.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--classifier gradient_boosting --eval f1 | tee short-ft-gb.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--classifier svm --eval f1 | tee short-ft-svm.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--classifier xgboost --eval f1 | tee short-ft-xg.log

time python 6ml.py --train_file ./short-data/strain.txt \
--test_file ./short-data/stest.txt --feature fasttext \
--classifier ensemble --eval f1 | tee short-ft-en.log

set +x;
```

## Training/Testing for SHORT HS  

with tf-idf results ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-tfidf-short.sh
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --classifier naive_bayes --eval f1
+ tee short-tfidf-nv.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.0626453360950898
Precision: 0.36011580199682847
Recall: 0.045

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.845s
user    0m0.840s
sys     0m0.233s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --classifier random_forest --eval f1
+ tee short-tfidf-rf.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4545580972459906
Precision: 0.4705274184812046
Recall: 0.523

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.282s
user    0m4.179s
sys     0m0.068s
+ tee short-tfidf-gb.log
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --classifier gradient_boosting --eval f1
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4456348379334548
Precision: 0.40686750365351393
Recall: 0.531

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m7.178s
user    0m7.114s
sys     0m0.062s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --classifier svm --eval f1
+ tee short-tfidf-svm.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4474197066208483
Precision: 0.4249350308291804
Recall: 0.525

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.810s
user    0m1.680s
sys     0m0.096s
+ tee short-tfidf-xg.log
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature tfidf --classifier xgboost --eval f1
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4445809429290888
Precision: 0.39020783921291147
Recall: 0.528

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.476s
user    0m43.121s
sys     0m1.449s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --classifier ensemble --eval f1
+ tee short-tfidf-en.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.44763424775793104
Precision: 0.6194360155973059
Recall: 0.55

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m41.679s
user    6m57.200s
sys     0m1.913s
+ set +x

real    6m3.272s
user    7m54.136s
sys     0m3.821s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

with word2vec results ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-word2vec-short.sh
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --classifier naive_bayes --eval f1
+ tee short-w2v-nv.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.058545502220572816
Precision: 0.6204964078083295
Recall: 0.052

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m1.190s
user    0m1.457s
sys     0m0.062s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --classifier random_forest --eval f1
+ tee short-w2v-rf.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4480235209290911
Precision: 0.4333607022607022
Recall: 0.536

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m11.142s
user    0m11.390s
sys     0m0.082s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --classifier gradient_boosting --eval f1
+ tee short-w2v-gb.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4487076866521063
Precision: 0.4237842878234517
Recall: 0.532

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    4m55.642s
user    4m55.807s
sys     0m0.080s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --classifier svm --eval f1
+ tee short-w2v-svm.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.44258590308370044
Precision: 0.7577269372693727
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m5.380s
user    0m5.607s
sys     0m0.095s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --classifier xgboost --eval f1
+ tee short-w2v-xg.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.44669908074981973
Precision: 0.43335294117647055
Recall: 0.532

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m4.344s
user    1m17.945s
sys     0m1.628s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature word2vec --classifier ensemble --eval f1
+ tee short-w2v-en.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4465450144541826
Precision: 0.44451724137931037
Recall: 0.539

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m12.699s
user    6m28.039s
sys     0m1.950s
+ set +x

real    10m30.399s
user    13m0.247s
sys     0m3.898s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

with fasttext results ...  

```
(xgboost) yekyaw.thu@gpu:~/exp/6ml$ time ./run-fasttext-short.sh
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --classifier naive_bayes --eval f1
+ tee short-ft-nv.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.03394996992830295
Precision: 0.27510183610024885
Recall: 0.04

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m2.951s
user    0m3.651s
sys     0m0.172s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --classifier random_forest --eval f1
+ tee short-ft-rf.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.44964784274439945
Precision: 0.41477361142727065
Recall: 0.535

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m12.766s
user    0m13.466s
sys     0m0.180s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --classifier gradient_boosting --eval f1
+ tee short-ft-gb.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.44584080958601263
Precision: 0.40271981292517006
Recall: 0.538

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    4m56.644s
user    4m57.333s
sys     0m0.110s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --classifier svm --eval f1
+ tee short-ft-svm.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4413249202410492
Precision: 0.7560390025575447
Recall: 0.549

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m33.254s
user    0m33.952s
sys     0m0.183s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --classifier xgboost --eval f1
+ tee short-ft-xg.log
Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.45116093724006034
Precision: 0.40510368455074336
Recall: 0.537

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    0m6.255s
user    1m22.257s
sys     0m1.967s
+ python 6ml.py --train_file ./short-data/strain.txt --test_file ./short-data/stest.txt --feature fasttext --classifier ensemble --eval f1
+ tee short-ft-en.log

Error: Line 1014 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 3671 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 5922 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6184 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
Error: Line 6584 in the file './short-data/strain.txt' does not contain both label and text. Skipping...
F1 Score: 0.4496016258452081
Precision: 0.4159436090225564
Recall: 0.548

Numeric Label - Original Label
ab - 0
no - 1
bo - 2
re - 3
po - 4
le - 5
ed - 6
se - 7
ra - 8
BLANK - 9

real    5m37.203s
user    6m52.483s
sys     0m2.080s
+ set +x

real    11m29.075s
user    14m3.144s
sys     0m4.691s
(xgboost) yekyaw.thu@gpu:~/exp/6ml$
```

## Result Tables with Markdown Format

```
### TF-IDF:

| Classifier         | F1 Score | Precision | Recall |
|--------------------|----------|-----------|--------|
| Naive Bayes        | 0.063    | 0.360     | 0.045  |
| Random Forest      | 0.455    | 0.471     | 0.523  |
| Gradient Boosting  | 0.446    | 0.407     | 0.531  |
| SVM                | 0.447    | 0.425     | 0.525  |
| XGBoost            | 0.445    | 0.390     | 0.528  |
| Ensemble           | 0.448    | 0.619     | 0.550  |

### Word2Vec:

| Classifier         | F1 Score | Precision | Recall |
|--------------------|----------|-----------|--------|
| Naive Bayes        | 0.059    | 0.620     | 0.052  |
| Random Forest      | 0.448    | 0.433     | 0.536  |
| Gradient Boosting  | 0.449    | 0.424     | 0.532  |
| SVM                | 0.443    | 0.758     | 0.549  |
| XGBoost            | 0.447    | 0.433     | 0.532  |
| Ensemble           | 0.447    | 0.445     | 0.539  |

### FastText:

| Classifier         | F1 Score | Precision | Recall |
|--------------------|----------|-----------|--------|
| Naive Bayes        | 0.034    | 0.275     | 0.040  |
| Random Forest      | 0.450    | 0.415     | 0.535  |
| Gradient Boosting  | 0.446    | 0.403     | 0.538  |
| SVM                | 0.441    | 0.756     | 0.549  |
| XGBoost            | 0.451    | 0.405     | 0.537  |
| Ensemble           | 0.450    | 0.416     | 0.548  |

These tables show the F1 scores, Precision, and Recall values for each classifier and feature representation method based on the provided experiment results.
```

## Result Tables with Latex Format  

for tf-idf feature ... 

```
\begin{table}[htbp]
  \centering
  \caption{TF-IDF Results}
  \begin{tabular}{|l|l|l|l|}
  \hline
  Classifier         & F1 Score & Precision & Recall \\
  \hline
  Naive Bayes        & 0.063    & 0.360     & 0.045  \\
  Random Forest      & 0.455    & 0.471     & 0.523  \\
  Gradient Boosting  & 0.446    & 0.407     & 0.531  \\
  SVM                & 0.447    & 0.425     & 0.525  \\
  XGBoost            & 0.445    & 0.390     & 0.528  \\
  Ensemble           & 0.448    & 0.619     & 0.550  \\
  \hline
  \end{tabular}
\end{table}

```

for word2vec feature ...  

```
\begin{table}[htbp]
  \centering
  \caption{Word2Vec Results}
  \begin{tabular}{|l|l|l|l|}
  \hline
  Classifier         & F1 Score & Precision & Recall \\
  \hline
  Naive Bayes        & 0.059    & 0.620     & 0.052  \\
  Random Forest      & 0.448    & 0.433     & 0.536  \\
  Gradient Boosting  & 0.449    & 0.424     & 0.532  \\
  SVM                & 0.443    & 0.758     & 0.549  \\
  XGBoost            & 0.447    & 0.433     & 0.532  \\
  Ensemble           & 0.447    & 0.445     & 0.539  \\
  \hline
  \end{tabular}
\end{table}

```

for fasttext feature ...  

```
\begin{table}[htbp]
  \centering
  \caption{FastText Results}
  \begin{tabular}{|l|l|l|l|}
  \hline
  Classifier         & F1 Score & Precision & Recall \\
  \hline
  Naive Bayes        & 0.034    & 0.275     & 0.040  \\
  Random Forest      & 0.450    & 0.415     & 0.535  \\
  Gradient Boosting  & 0.446    & 0.403     & 0.538  \\
  SVM                & 0.441    & 0.756     & 0.549  \\
  XGBoost            & 0.451    & 0.405     & 0.537  \\
  Ensemble           & 0.450    & 0.416     & 0.548  \\
  \hline
  \end{tabular}
\end{table}

```

I also zipped the whole folder of 6ml/ and copied to the local machine.  

