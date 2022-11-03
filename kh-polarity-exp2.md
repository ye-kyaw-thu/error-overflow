## Khmer Polarity Classification with Traditional Machine Learning Algorithms

## K-nearest Neighbors Result

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
