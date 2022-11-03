## Khmer Polarity Classification with Traditional Machine Learning Algorithms

## K-nearest Neighbors Result

```python
## KNN Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 3 Nov 2022

import pandas as pd
import re
from os import system, listdir
from os.path import isfile, join
from random import shuffle

import warnings
warnings.filterwarnings("ignore")


polar_train = pd.read_csv('csv/train.csv')
polar_test = pd.read_csv('csv/test.csv')

### Text Vectorization

from sklearn.feature_extraction.text import CountVectorizer, TfidfTransformer
from joblib import dump, load # used for saving and loading sklearn objects
from scipy.sparse import save_npz, load_npz # used for saving and loading sparse matrices

system("mkdir 'data_preprocessors'")
system("mkdir 'vectorized_data'")


# Unigram Counts

unigram_vectorizer = CountVectorizer(ngram_range=(1, 1))
unigram_vectorizer.fit(polar_train['text'].values)

dump(unigram_vectorizer, 'data_preprocessors/unigram_vectorizer.joblib')

# unigram_vectorizer = load('data_preprocessors/unigram_vectorizer.joblib')

X_train_unigram = unigram_vectorizer.transform(polar_train['text'].values)

save_npz('vectorized_data/X_train_unigram.npz', X_train_unigram)

# X_train_unigram = load_npz('vectorized_data/X_train_unigram.npz')


# Unigram Tf-Idf

unigram_tf_idf_transformer = TfidfTransformer()
unigram_tf_idf_transformer.fit(X_train_unigram)

dump(unigram_tf_idf_transformer, 'data_preprocessors/unigram_tf_idf_transformer.joblib')

# unigram_tf_idf_transformer = load('data_preprocessors/unigram_tf_idf_transformer.joblib')

X_train_unigram_tf_idf = unigram_tf_idf_transformer.transform(X_train_unigram)

save_npz('vectorized_data/X_train_unigram_tf_idf.npz', X_train_unigram_tf_idf)

# X_train_unigram_tf_idf = load_npz('vectorized_data/X_train_unigram_tf_idf.npz')


# Bigram Counts

bigram_vectorizer = CountVectorizer(ngram_range=(1, 2))
bigram_vectorizer.fit(polar_train['text'].values)

dump(bigram_vectorizer, 'data_preprocessors/bigram_vectorizer.joblib')

# bigram_vectorizer = load('data_preprocessors/bigram_vectorizer.joblib')

X_train_bigram = bigram_vectorizer.transform(polar_train['text'].values)

save_npz('vectorized_data/X_train_bigram.npz', X_train_bigram)

# X_train_bigram = load_npz('vectorized_data/X_train_bigram.npz')


# Bigram Tf-Idf

bigram_tf_idf_transformer = TfidfTransformer()
bigram_tf_idf_transformer.fit(X_train_bigram)

dump(bigram_tf_idf_transformer, 'data_preprocessors/bigram_tf_idf_transformer.joblib')

# bigram_tf_idf_transformer = load('data_preprocessors/bigram_tf_idf_transformer.joblib')

X_train_bigram_tf_idf = bigram_tf_idf_transformer.transform(X_train_bigram)

save_npz('vectorized_data/X_train_bigram_tf_idf.npz', X_train_bigram_tf_idf)

# X_train_bigram_tf_idf = load_npz('vectorized_data/X_train_bigram_tf_idf.npz')

### Choosing the Data Format


from sklearn.model_selection import train_test_split
from scipy.sparse import csr_matrix
import numpy as np

# Import k-nearest neighbors library
from sklearn.neighbors import KNeighborsClassifier

def train_and_show_scores_KNN(X: csr_matrix, y: np.array, title: str, model: str) -> None:
    X_train, X_valid, y_train, y_valid = train_test_split(
        X, y, train_size=0.75, stratify=y
    )

    clf = KNeighborsClassifier(n_neighbors=5)
    clf.fit(X_train, y_train)
    train_score = clf.score(X_train, y_train)
    valid_score = clf.score(X_valid, y_valid)
    print(f'{title}\nTrain score: {round(train_score, 2)} ; Validation score: {round(valid_score, 2)}\n')

    #saving model
    dump(clf, 'classifiers/' + model)

y_train = polar_train['label'].values

train_and_show_scores_KNN(X_train_unigram, y_train, 'KNN, Unigram Counts', 'knn_unigram_count.joblib')
train_and_show_scores_KNN(X_train_unigram_tf_idf, y_train, 'KNN, Unigram Tf-Idf', 'knn_unigram_tf-idf.joblib')
train_and_show_scores_KNN(X_train_bigram, y_train, 'KNN, Bigram Counts', 'knn_bigram_count.joblib')
train_and_show_scores_KNN(X_train_bigram_tf_idf, y_train, 'KNN, Bigram Tf-Idf', 'knn_bigram_tf-idf.joblib')


### Testing/Evaluation

X_test = unigram_vectorizer.transform(polar_test['text'].values)
X_test = unigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

knn_unigram_counts = load('classifiers/knn_unigram_count.joblib')
score = knn_unigram_counts.score(X_test, y_test)
print('KNN Test Result, Unigram Counts: ', score)

# Predict the class of test set
y_predict = knn_unigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)

knn_unigram_tfidf = load('classifiers/knn_unigram_tf-idf.joblib')
score = knn_unigram_tfidf.score(X_test, y_test)
print('KNN Test Result, Unigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = knn_unigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)

X_test = bigram_vectorizer.transform(polar_test['text'].values)
X_test = bigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

knn_bigram_counts = load('classifiers/knn_bigram_count.joblib')
score = knn_bigram_counts.score(X_test, y_test)
print('KNN Test Result, Bigram Count: ', score)

# Predict the class of test set
y_predict = knn_bigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)

knn_bigram_tfidf = load('classifiers/knn_bigram_tf-idf.joblib')
score = knn_bigram_tfidf.score(X_test, y_test)
print('KNN Test Result, Bigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = knn_bigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
```

Results are as follows:  

```
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd# python knn-classifier.py
KNN, Unigram Counts
Train score: 0.64 ; Validation score: 0.52

KNN, Unigram Tf-Idf
Train score: 0.64 ; Validation score: 0.52

KNN, Bigram Counts
Train score: 0.62 ; Validation score: 0.51

KNN, Bigram Tf-Idf
Train score: 0.6 ; Validation score: 0.46

KNN Test Result, Unigram Counts:  0.492
Error Rate: 0.51
KNN Test Result, Unigram Tf-Idf:  0.533
Error Rate: 0.47
KNN Test Result, Bigram Count:  0.472
Error Rate: 0.53
KNN Test Result, Bigram Tf-Idf:  0.462
Error Rate: 0.54
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd# 
```

## Decision Tree

```python
## Decision Tree Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 3 Nov 2022

import pandas as pd
import re
from os import system, listdir
from os.path import isfile, join
from random import shuffle

import warnings
warnings.filterwarnings("ignore")


polar_train = pd.read_csv('csv/train.csv')
polar_test = pd.read_csv('csv/test.csv')

### Text Vectorization

from sklearn.feature_extraction.text import CountVectorizer, TfidfTransformer
from joblib import dump, load # used for saving and loading sklearn objects
from scipy.sparse import save_npz, load_npz # used for saving and loading sparse matrices

system("mkdir 'data_preprocessors'")
system("mkdir 'vectorized_data'")


# Unigram Counts

unigram_vectorizer = CountVectorizer(ngram_range=(1, 1))
unigram_vectorizer.fit(polar_train['text'].values)

dump(unigram_vectorizer, 'data_preprocessors/unigram_vectorizer.joblib')

# unigram_vectorizer = load('data_preprocessors/unigram_vectorizer.joblib')

X_train_unigram = unigram_vectorizer.transform(polar_train['text'].values)

save_npz('vectorized_data/X_train_unigram.npz', X_train_unigram)

# X_train_unigram = load_npz('vectorized_data/X_train_unigram.npz')


# Unigram Tf-Idf

unigram_tf_idf_transformer = TfidfTransformer()
unigram_tf_idf_transformer.fit(X_train_unigram)

dump(unigram_tf_idf_transformer, 'data_preprocessors/unigram_tf_idf_transformer.joblib')

# unigram_tf_idf_transformer = load('data_preprocessors/unigram_tf_idf_transformer.joblib')

X_train_unigram_tf_idf = unigram_tf_idf_transformer.transform(X_train_unigram)

save_npz('vectorized_data/X_train_unigram_tf_idf.npz', X_train_unigram_tf_idf)

# X_train_unigram_tf_idf = load_npz('vectorized_data/X_train_unigram_tf_idf.npz')


# Bigram Counts

bigram_vectorizer = CountVectorizer(ngram_range=(1, 2))
bigram_vectorizer.fit(polar_train['text'].values)

dump(bigram_vectorizer, 'data_preprocessors/bigram_vectorizer.joblib')

# bigram_vectorizer = load('data_preprocessors/bigram_vectorizer.joblib')

X_train_bigram = bigram_vectorizer.transform(polar_train['text'].values)

save_npz('vectorized_data/X_train_bigram.npz', X_train_bigram)

# X_train_bigram = load_npz('vectorized_data/X_train_bigram.npz')


# Bigram Tf-Idf

bigram_tf_idf_transformer = TfidfTransformer()
bigram_tf_idf_transformer.fit(X_train_bigram)

dump(bigram_tf_idf_transformer, 'data_preprocessors/bigram_tf_idf_transformer.joblib')

# bigram_tf_idf_transformer = load('data_preprocessors/bigram_tf_idf_transformer.joblib')

X_train_bigram_tf_idf = bigram_tf_idf_transformer.transform(X_train_bigram)

save_npz('vectorized_data/X_train_bigram_tf_idf.npz', X_train_bigram_tf_idf)

# X_train_bigram_tf_idf = load_npz('vectorized_data/X_train_bigram_tf_idf.npz')

### Choosing the Data Format


from sklearn.model_selection import train_test_split
from scipy.sparse import csr_matrix
import numpy as np

# Import logistic regression library
from sklearn import tree

def train_and_show_scores_DTREE(X: csr_matrix, y: np.array, title: str, model: str) -> None:
    X_train, X_valid, y_train, y_valid = train_test_split(
        X, y, train_size=0.75, stratify=y
    )

    clf = tree.DecisionTreeClassifier(criterion='entropy')
    clf.fit(X_train, y_train)
    train_score = clf.score(X_train, y_train)
    valid_score = clf.score(X_valid, y_valid)
    print(f'{title}\nTrain score: {round(train_score, 2)} ; Validation score: {round(valid_score, 2)}\n')

    #saving model
    dump(clf, 'classifiers/' + model)

y_train = polar_train['label'].values

train_and_show_scores_DTREE(X_train_unigram, y_train, 'DTREE, Unigram Counts', 'dtree_unigram_count.joblib')
train_and_show_scores_DTREE(X_train_unigram_tf_idf, y_train, 'DTREE, Unigram Tf-Idf', 'dtree_unigram_tf-idf.joblib')
train_and_show_scores_DTREE(X_train_bigram, y_train, 'DTREE, Bigram Counts', 'dtree_bigram_count.joblib')
train_and_show_scores_DTREE(X_train_bigram_tf_idf, y_train, 'DTREE, Bigram Tf-Idf', 'dtree_bigram_tf-idf.joblib')


### Testing/Evaluation

X_test = unigram_vectorizer.transform(polar_test['text'].values)
X_test = unigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

dtree_unigram_counts = load('classifiers/dtree_unigram_count.joblib')
score = dtree_unigram_counts.score(X_test, y_test)
print('Decision Tree Test Result, Unigram Counts: ', score)

# Predict the class of test set
y_predict = dtree_unigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)

dtree_unigram_tfidf = load('classifiers/dtree_unigram_tf-idf.joblib')
score = dtree_unigram_tfidf.score(X_test, y_test)
print('Decision Tree Test Result, Unigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = dtree_unigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)

X_test = bigram_vectorizer.transform(polar_test['text'].values)
X_test = bigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

dtree_bigram_counts = load('classifiers/dtree_bigram_count.joblib')
score = dtree_bigram_counts.score(X_test, y_test)
print('Decision Tree Test Result, Bigram Count: ', score)

# Predict the class of test set
y_predict = dtree_bigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)

dtree_bigram_tfidf = load('classifiers/dtree_bigram_tf-idf.joblib')
score = dtree_bigram_tfidf.score(X_test, y_test)
print('Decision Tree Test Result, Bigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = dtree_bigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)


```

Results are as follows:  

```
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd# python dtree-classifier.py
DTREE, Unigram Counts
Train score: 0.84 ; Validation score: 0.52

DTREE, Unigram Tf-Idf
Train score: 0.83 ; Validation score: 0.53

DTREE, Bigram Counts
Train score: 0.83 ; Validation score: 0.53

DTREE, Bigram Tf-Idf
Train score: 0.84 ; Validation score: 0.53

Decision Tree Test Result, Unigram Counts:  0.538
Error Rate: 0.46
Decision Tree Test Result, Unigram Tf-Idf:  0.549
Error Rate: 0.45
Decision Tree Test Result, Bigram Count:  0.567
Error Rate: 0.43
Decision Tree Test Result, Bigram Tf-Idf:  0.524
Error Rate: 0.48
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd#
```

## Random Forest

```python

```

Results are as follows:  

```
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd# python ./rforest-classifier.py
RFOREST, Unigram Counts
Train score: 0.83 ; Validation score: 0.58

RFOREST, Unigram Tf-Idf
Train score: 0.83 ; Validation score: 0.58

RFOREST, Bigram Counts
Train score: 0.84 ; Validation score: 0.57

RFOREST, Bigram Tf-Idf
Train score: 0.84 ; Validation score: 0.57

Random Forest Test Result, Unigram Counts:  0.535
Error Rate: 0.47
Random Forest Test Result, Unigram Tf-Idf:  0.577
Error Rate: 0.42
Random Forest Test Result, Bigram Count:  0.576
Error Rate: 0.42
Random Forest Test Result, Bigram Tf-Idf:  0.579
Error Rate: 0.42
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd#
```

## Support Vector Machine (SVM)

```python

```

Results are as follows:  

```
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd# python svm-classifier.py
SVM, Unigram Counts
Train score: 0.62 ; Validation score: 0.59

SVM, Unigram Tf-Idf
Train score: 0.6 ; Validation score: 0.57

SVM, Bigram Counts
Train score: 0.77 ; Validation score: 0.56

SVM, Bigram Tf-Idf
Train score: 0.69 ; Validation score: 0.59

SVM Test Result, Unigram Counts:  0.583
Error Rate: 0.42
SVM Test Result, Unigram Tf-Idf:  0.581
Error Rate: 0.42
SVM Test Result, Bigram Count:  0.577
Error Rate: 0.42
SVM Test Result, Bigram Tf-Idf:  0.608
Error Rate: 0.39
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd#
```

## Stochastic Gradient Descent (SGD)

```python

```

Results are as follows:  

```
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd# python sgd-classifier2.py
SGD, Unigram Counts
Train score: 0.64 ; Validation score: 0.58

SGD, Unigram Tf-Idf
Train score: 0.63 ; Validation score: 0.59

SGD, Bigram Counts
Train score: 0.79 ; Validation score: 0.57

SGD, Bigram Tf-Idf
Train score: 0.74 ; Validation score: 0.59

SGD Test Result, Unigram Counts:  0.584
Error Rate: 0.42
SGD Test Result, Unigram Tf-Idf:  0.588
Error Rate: 0.41
SGD Test Result, Bigram Count:  0.57
Error Rate: 0.43
SGD Test Result, Bigram Tf-Idf:  0.597
Error Rate: 0.40
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd#
```

## SGD Tuning Result

```python

```

Results are as follows:  


```
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd# python kh-sgd.py
Unigram Counts
Train score: 0.64 ; Validation score: 0.59

Unigram Tf-Idf
Train score: 0.63 ; Validation score: 0.59

Bigram Counts
Train score: 0.79 ; Validation score: 0.56

Bigram Tf-Idf
Train score: 0.74 ; Validation score: 0.58

Best params: {'eta0': 0.009619888350768734, 'learning_rate': 'adaptive', 'loss': 'hinge'}
Best score: 0.5926347935337761
Best params: {'alpha': 9.80091439157578e-05, 'penalty': 'l2'}
Best score: 0.5921915810558676

Result with the Best SGD Classifier: 0.598
Error Rate: 0.40
(polar) root@e050ac832975:/home/ye/exp/kh-polar/sgd#
```
