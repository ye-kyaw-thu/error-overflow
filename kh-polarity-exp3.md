# Khmer Polarity Classification (F1, P, R)

For this time, I wanna see the ML model results with F1, Precision and Reall.   
And thus, update the python codes and re-run the experiments ...  

## Data Preparation

Copy the CSV files to the new experiment folder:  
```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ cp ~/tool/fastText/kh-polar/kh-final-fasttext/baseline-sentence/{train,test}.csv ./run-for-f1/
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$
```

Check the filesize:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar$ cd run-for-f1/
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ wc {train,test}.csv
   9015  698068 5188719 train.csv
   1001   75893  563454 test.csv
  10016  773961 5752173 total
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ 
```

Check the content:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ head train.csv
sentence,label
▁រដ្ឋ ម ន្ត រី ប រ ិ ស្ថាន អ ៊ ុយ ក្រ ែន បាន បញ្ជា ក់ កាល ពី ថ ្ ង ៃ ច ន្ទ ទី ▁៣ ▁ខែ ត ុល ា ថា ▁ការ ខ ូ ច ខាត ប រ ិ ស្ថាន ក្នុង ប្រ ទេស អ ៊ ុយ ក្រ ែន ដែ ល ប ណ្តាល មក ពី ការ ឈ ្ល ាន ព ាន រ ប ស់ រ ុ ស្ ស៊ី ត្រ ូវ បាន គេ ប៉ ាន់ ប្រ មា ណ ថា ▁មាន ទ ំ ហ ំ ជា ង ▁៣ ៥ ៣ ព ាន់ ល ាន ដ ុល ្ល ារ ▁ជាមួយ នឹង ត ំ ប ន់ អ ភ ិ រ ក្ស ធ ម្ ម ជាតិ រ ាប់ ល ាន ហ ិក តា ទ ៀ ត ស្ ថ ិត ន ៅ ក ្រោម ការ គ ំ រា មក ំ ហ ែង ▁។,negative
▁ខ្ញុំ ច ង់ ច ាប់ ផ្តើម ប្រ ើ ផ ា ស ពិសេស ស ំ រ ាប់ អ ្ន ក ធ្វើដំណើរ,neutral
▁ក្រោយ ពេល ដែ ល វា បាន ហ ែ ល ប ត់ ច ុះ ប ត់ ឡើង គ ្រ ប់ ៗ ក ន ្ល ែង វា ទៅ ដល់ ស្រ ុក ខ ោ ន ហើយ វា ស ំ ច ត ន ៅ ទី នោះ ២ . ២ ថ ្ ង ៃ ទ ើ ប វា ហ ែ ល ច ុះ មក វិញ ។,neutral
▁យើង បាន ស្ត ាប់ ល ឺ ឧ ទ ារ ហ រ ណ៍ ពី កិច្ច ខ ិត ខ ំ ប្រ ឹង ប្រ ែង ទ ាំង ស្រ ុង ស្ត ី ពី ការ ច ាក់ វ៉ា ក់ ស ាំង ▁នៅ ទូ ទ ាំង ពិ ភ ព លោក ▁បាន ក ាត់ បន្ថ យ អ ត្រា ស្លាប់ រ ប ស់ ក ្ម េង យ៉ា ង ច្រើន ។,positive
▁ជា ច ុង ក្រ ោ យ រ ឿ ង មួយ នេះ បាន ប ង ្រ ៀន ខ្ញុំ ឱ្យ ដឹង ថា ស្ ន េ ហា ▁បើ មាន ការ ខ ិត ខ ំ ល ះ ប ង់ តែ ម្ ខាង ▁គឺ ម ិន អា ច ដ ើ រ ទៅ មុខ បាន ឡ ើយ ▁លុះ ត្រា តែ មាន ការ ចូលរួម ល ះ ប ង់ ជ ្រោម ជ ្រ ែង ទ ាំង ស ង ខាង ទ ើ ប ស្ ន េ ហា មួយ នោះ អា ច ប ន្ត ដំណើរ ទៅ មុខ ស្ វែង រ ក ព ន ្ល ឺ នៃ ស ុ ភ ម ង្គ ល ឃើញ ។,positive
▁លោក ▁បន្ត ▁ថា ▁លោក ▁និង ▁ កម្ម ករ ▁មាន ▁ប្រាក់ ▁ចំណ ូល ▁មិន ▁ទ ៀង ▁ទ ាត់ ▁ហើយ ▁ការ ▁ដ ោះ ស្រ ាយ ▁បញ្ហា ▁ជី វ ភាព ▁មាន ▁ការ ▁ ល ំ ប ា ក ▁តែ ▁ចេះ ▁តែ ▁ខ ិត ខ ំ ▁ជ ម្ ន ះ ▁ឧប ស គ្គ ▁ទាំង ▁ នេះ ៖ ▁ « ធ ្វ ើ ការ ▁ធ្វើ ▁ប ័ ត្រ ▁អី ▁ហ្នឹង ▁គឺ ▁ច្រើន ▁ជាង ▁មុន ▁ទៀត ▁លើក ▁មុន ▁ត្រឹម តែ ▁ ៨ . ០០០ ▁ឬ ▁ ៧ . ០០០ ប ា ត ▁បាន ▁ណា ▁កន្លែង ▁ ខ្លះ ▁ណា ▁ទ ារ ▁ច្រើន ▁ក៏ ▁ប្រាំ ប ី ▁ព ាន់ ▁កន្លែង ▁ណា ▁គេ ▁ យ ោ គ យ ល់ ▁ទៅ ▁ប្រាំ ▁ពីរ ▁ព ាន់ ▁បាទ ▁អ៊ី ច ឹង ▁ណា ▁មួយ ▁ឆ្នាំ ▁ពីរ ▁ឆ្នាំ ។,negative
▁ការ ជ េរ ប្រ មា ថ ម៉ា ក់ ង ាយ នេះ ▁ត្រូវ បាន ▁លោក ▁កែវ ▁ រ ត ន ៈ ▁បញ្ជា ក់ ថា ▁ដោយសារ ការ ក ើ ន ឡើង គ ី ឡ ូ ភ្លើង ▁និង ▁ការ ដ ាច់ ភ្លើង ក្នុង រ ដ ូវ ក ្ត ៅ ជា ដ ើម ▁ ៕,negative
▁សម ិទ្ធ ផល ▁ក្នុង ថ ្ ង ៃ នេះ ▁គឺជា ▁ម ោ ទ ក ភាព ▁ នៃ ▁ការ ខ ិត ខ ំ ▁ប្រ ឹង ប្រ ែង ▁ រ ប ▁ ស់ ▁យើង ▁ហើយ ▁ពួក យើង ▁មាន ▁ម ោ ▁ទ ▁ក ▁ភាព ▁ណាស់ ▁ដែល ▁យើង ▁គឺជា ▁បុគ្គល ិក ▁របស់ ▁ ដា ▁ ណ ន់ ▁ Danone ▁។,positive
▁ពិ ត ណ ាស់ ▁កាហ្វេ ដែ ល គ ្ មាន សារ ជាតិ ក ា ហ្វ េ អ ៊ ី ន ▁នៅ តែ មាន សារ ជាតិ ក ា ហ្វ េ អ ៊ ី ន ចំនួ ន ▁៣ % ▁។,positive
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ 
```

train the test.csv file:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ head test.csv
sentence,label
▁ នេះ ប ើ តា ម ប្រ សា ស ន៍ រ ប ស់ ▁ឯក ឧ ត្ត ម ▁ ន េ ត្រ ▁ភ ក ្ត រា ▁រដ្ឋ លេខ ា ធ ិ ការ ▁និង ជា អ ន ុ ប្រ ធាន អ ច ិ ន្ត រ ៃ យ ៍ ក្រ ុ ម ការ ង ារ ប្រឆាំង ការ ស ម្ អា ត ប្រ ាក់ នៃ ក្រ ស ួង ប រ ិ ស្ថាន ▁កាល ថ ្ ង ៃ ទី ៥ ▁ខែ ត ុល ា ▁ឆ្នាំ ២ ០ ២ ២ ▁។,negative
▁ចំណ ែក ▁ម ន្ត រី ▁ សិទ្ធិ ម ន ុ ស្ស ▁និង ▁អ្នក វិ ភ ា គ ▁យល់ ▁ថា ▁អ្វី ▁ដែល ▁លោក ▁ ហ៊ុន ▁ស ែន ▁លើក ▁ឡើង ▁មក ▁នោះ ▁ជា ▁វ ោ ហា រ សា ស្ត រ ▁ ន យោប ាយ ▁ដើម្បី ▁ប ន ្ល ំ ▁ការ ▁ពិ ត ▁ប៉ុណ្ណ ោះ ។,negative
▁ការងា រ មាន ស្ ថ ិ រ ភាព ▁ហើយ អ ្ន ក អា ច ទ ទ ួល បាន ស ម ិទ្ធ ផល ជ ាក់ ល ាក់ ក្នុង អា ជ ី ព រ ប ស់ អ ្ន ក ▁ ធាន ា ជ ី វ ិត រ ប ស់ អ ្ន ក ។,positive
▁ការ ព ្យ ាប ាល : ▁គ្រប់គ្រ ង រោគ ស ញ្ញា ▁និង ▁ ផល វិ ប ា ក ▁កាត់ បន្ថ យ ការ វិ វ ត្ត ន៍ រ ប ស់ ជ ំ ង ឺ ។,positive
▁ យ ោង តា ម ក្រ ស ួង បាន ឱ្យ ដឹង ថា ▁ក ម្រិត វិ ទ ្យ ុស កម្ម ន ៅ ទី ត ាំង រ ោង ច ក្រ ហ្ សា ផ ូរ ី ហ្ សា ▁ដែល ជា រ ោង ច ក្រ ថា ម ពល ន ុយ ក ្ល េ អ ៊ ែ រ ដ ៏ ធ ំ ប ំ ផ ុត រ ប ស់ អ ឺ រ ៉ ុ ប ▁នៅ តែ មាន ល ក្ខ ណ ៈ ធ ម្មតា ន ៅ ឡ ើយ ។,neutral
▁រាជ ធាន ី ▁ភ្នំពេ ញ ▁ ៖ ▁ស ម្តេច ▁ ត េ ▁ជ ោ ▁ ហ៊ុន ▁ស ែន ▁នា យ ក ▁រដ្ឋ ម ន្ត រី ▁ នៃ ▁កម្ព ុជា ▁បាន ▁ចំ អ ក ▁ឲ្យ ក្រ ុ ម ▁ ប្រឆាំង ដែ ល ▁ ដឹកនាំ ▁ដោយ លោក ▁សម ▁ រ ▁ ង ្ ស៊ី ▁ដែល ▁ស ម្តេច ▁បាន ▁ហៅ ▁ថា ▁ជា ▁ច ោ រ ▁ ក្ ប ត់ ជាតិ ▁នោះ ថា ▁បាន ▁បង្កើត ▁ក ំ ហ ុស ▁ យ ុទ្ធ សា ស្ត រ ▁ធំ ▁២ ▁រហូត ▁នាំ ទុក្ខ ▁ដល់ ▁អ្នក គ ាំ ទ្រ ▁របស់ ▁ខ្លួន ▁។,negative
▁ប ទ នេះ ព េញ ចិត្ត ណ ាស់,positive
▁អ ំ ណា ន ជា អ ំ ណា ច ▁វិ ភ ា គ ទាន លើ ក នេះ យើង ព ិត ជា ធ ្វ ើ បាន ល ឿន ណ ាស់ ▁ត្រឹម តែ រយៈ ពេល ៤ ថ ្ ង ៃ ប៉ ុ ណ្ណ ោះ មាន អ ្ន ក ស្ ន ើ ស ៀ វ ភ ៅ នេះ គ ្រ ប់ ចំនួ ន ៥ ០០០ ក្ ប ាល ។,positive
▁ពិធី ស ម្ ព ោ ធ ជា ផ្ ល ូវ ការ ▁ក្រុម ហ៊ុន ▁ហ ន ុ មាន ▁ប៊ ែ វ ើ រី ជ ី ស ក ្រោម អ ធ ិ ប ត ី ភាព ដ ៏ ខ ្ ព ង់ ខ ្ ព ស់ ▁ឯក ឧ ត្ត ម ▁ ឧ ត្ត ម ស េ ន ី យ ៍ ឯ ក ▁ ហ៊ុន ▁ ម៉ា ណ ែ ត ▁អ គ្គ ម េ បញ្ជា ការ រ ង នៃ ក ង យ ោ ធ ពល ខ េ ម រ ភូមិ ន្ទ ▁និង ជា ម េ បញ្ជា ការ ក ង ទ ័ ព ជ ើ ង គ ោក ៕,positive
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ 
```

## KNN

Original python code that I run with R^2 or score() is as follows:  

```python
## KNN Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 3 Nov 2022
## Reference:
## https://towardsdatascience.com/building-a-sentiment-classifier-using-scikit-learn-54c8e7c5d2f0

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

1st, I create a new folder according to the data path inside the original python code.  


```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ mkdir csv
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ mv *.csv ./csv
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ ls
csv
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ ls ./csv
test.csv  train.csv
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

Moreover, according to the original code, I need to update the header label and thus ...  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ nano ./csv/train.csv 
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ nano ./csv/test.csv 
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ head -2 ./csv/train.csv 
text,label
▁រដ្ឋ ម ន្ត រី ប រ ិ ស្ថាន អ ៊ ុយ ក្រ ែន បាន បញ្ជា ក់ កាល ពី ថ ្ ង ៃ ច ន្ទ ទី ▁៣ ▁ខែ ត ុល ា ថា ▁ការ ខ ូ ច ខាត ប រ ិ ស្ថាន ក្នុង ប្រ ទេស អ ៊ ុយ ក្រ ែន ដែ ល ប ណ្តាល មក ពី ការ ឈ ្ល ាន ព ាន រ ប ស់ រ ុ ស្ ស៊ី ត្រ ូវ បាន គេ ប៉ ាន់ ប្រ មា ណ ថា ▁មាន ទ ំ ហ ំ ជា ង ▁៣ ៥ ៣ ព ាន់ ល ាន ដ ុល ្ល ារ ▁ជាមួយ នឹង ត ំ ប ន់ អ ភ ិ រ ក្ស ធ ម្ ម ជាតិ រ ាប់ ល ាន ហ ិក តា ទ ៀ ត ស្ ថ ិត ន ៅ ក ្រោម ការ គ ំ រា មក ំ ហ ែង ▁។,negative
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ head -2 ./csv/test.csv 
text,label
▁ នេះ ប ើ តា ម ប្រ សា ស ន៍ រ ប ស់ ▁ឯក ឧ ត្ត ម ▁ ន េ ត្រ ▁ភ ក ្ត រា ▁រដ្ឋ លេខ ា ធ ិ ការ ▁និង ជា អ ន ុ ប្រ ធាន អ ច ិ ន្ត រ ៃ យ ៍ ក្រ ុ ម ការ ង ារ ប្រឆាំង ការ ស ម្ អា ត ប្រ ាក់ នៃ ក្រ ស ួង ប រ ិ ស្ថាន ▁កាល ថ ្ ង ៃ ទី ៥ ▁ខែ ត ុល ា ▁ឆ្នាំ ២ ០ ២ ២ ▁។,negative
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

I also need to create a new folder named classifier in advance.  
After above preprocessings I run with the original code and check the results:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./knn-classifier.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
KNN, Unigram Counts
Train score: 0.63 ; Validation score: 0.51

KNN, Unigram Tf-Idf
Train score: 0.62 ; Validation score: 0.5

KNN, Bigram Counts
Train score: 0.63 ; Validation score: 0.49

KNN, Bigram Tf-Idf
Train score: 0.62 ; Validation score: 0.47

KNN Test Result, Unigram Counts:  0.491
Error Rate: 0.51
KNN Test Result, Unigram Tf-Idf:  0.517
Error Rate: 0.48
KNN Test Result, Bigram Count:  0.464
Error Rate: 0.54
KNN Test Result, Bigram Tf-Idf:  0.48
Error Rate: 0.52

real	0m6.956s
user	0m6.056s
sys	0m1.673s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

2nd time run the same code and check the scores:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ rm -r data_preprocessors/
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ rm -r vectorized_data/
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./knn-classifier.py 
KNN, Unigram Counts
Train score: 0.62 ; Validation score: 0.48

KNN, Unigram Tf-Idf
Train score: 0.62 ; Validation score: 0.51

KNN, Bigram Counts
Train score: 0.58 ; Validation score: 0.44

KNN, Bigram Tf-Idf
Train score: 0.62 ; Validation score: 0.48

KNN Test Result, Unigram Counts:  0.474
Error Rate: 0.53
KNN Test Result, Unigram Tf-Idf:  0.503
Error Rate: 0.50
KNN Test Result, Bigram Count:  0.338
Error Rate: 0.66
KNN Test Result, Bigram Tf-Idf:  0.5
Error Rate: 0.50

real	0m6.914s
user	0m6.013s
sys	0m1.391s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

3rd time running and check the KNN results:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./knn-classifier.py 
KNN, Unigram Counts
Train score: 0.62 ; Validation score: 0.51

KNN, Unigram Tf-Idf
Train score: 0.65 ; Validation score: 0.52

KNN, Bigram Counts
Train score: 0.61 ; Validation score: 0.48

KNN, Bigram Tf-Idf
Train score: 0.61 ; Validation score: 0.5

KNN Test Result, Unigram Counts:  0.463
Error Rate: 0.54
KNN Test Result, Unigram Tf-Idf:  0.535
Error Rate: 0.47
KNN Test Result, Bigram Count:  0.363
Error Rate: 0.64
KNN Test Result, Bigram Tf-Idf:  0.51
Error Rate: 0.49

real	0m6.462s
user	0m5.578s
sys	0m1.373s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

As we can seen above, the results might be change according to the running time.  

## KNN Results with F1, P and R

Updated the KNN python code as follows:  

```python
## KNN Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 8 Feb 2023
## Reference:
## https://towardsdatascience.com/building-a-sentiment-classifier-using-scikit-learn-54c8e7c5d2f0
## https://vitalflux.com/accuracy-precision-recall-f1-score-python-example/  
## https://stackoverflow.com/questions/62792001/precision-and-recall-are-the-same-within-a-model
## https://towardsdatascience.com/micro-macro-weighted-averages-of-f1-score-clearly-explained-b603420b292f
## https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html

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
#from sklearn.metrics import precision_score, recall_score, f1_score, accuracy_score
from sklearn.metrics import classification_report

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

y_pred = knn_unigram_counts.predict(X_test)

# Predict the class of test set
y_predict = knn_unigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

knn_unigram_tfidf = load('classifiers/knn_unigram_tf-idf.joblib')
score = knn_unigram_tfidf.score(X_test, y_test)
print('KNN Test Result, Unigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = knn_unigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

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
print('----------')
print(classification_report(y_test, y_predict))
print('')

knn_bigram_tfidf = load('classifiers/knn_bigram_tf-idf.joblib')
score = knn_bigram_tfidf.score(X_test, y_test)
print('KNN Test Result, Bigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = knn_bigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))

```

The updated results:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./knn-classifier.py 
KNN, Unigram Counts
Train score: 0.62 ; Validation score: 0.48

KNN, Unigram Tf-Idf
Train score: 0.64 ; Validation score: 0.53

KNN, Bigram Counts
Train score: 0.63 ; Validation score: 0.5

KNN, Bigram Tf-Idf
Train score: 0.61 ; Validation score: 0.48

KNN Test Result, Unigram Counts:  0.457
Error Rate: 0.54
----------
              precision    recall  f1-score   support

    negative       0.36      0.55      0.43       325
     neutral       0.08      0.05      0.07        92
    positive       0.62      0.47      0.53       583

    accuracy                           0.46      1000
   macro avg       0.35      0.36      0.34      1000
weighted avg       0.49      0.46      0.46      1000


KNN Test Result, Unigram Tf-Idf:  0.529
Error Rate: 0.47
----------
              precision    recall  f1-score   support

    negative       0.40      0.37      0.38       325
     neutral       0.11      0.05      0.07        92
    positive       0.61      0.69      0.65       583

    accuracy                           0.53      1000
   macro avg       0.38      0.37      0.37      1000
weighted avg       0.50      0.53      0.51      1000


KNN Test Result, Bigram Count:  0.426
Error Rate: 0.57
----------
              precision    recall  f1-score   support

    negative       0.32      0.37      0.34       325
     neutral       0.04      0.04      0.04        92
    positive       0.58      0.52      0.55       583

    accuracy                           0.43      1000
   macro avg       0.31      0.31      0.31      1000
weighted avg       0.44      0.43      0.43      1000


KNN Test Result, Bigram Tf-Idf:  0.483
Error Rate: 0.52
----------
              precision    recall  f1-score   support

    negative       0.35      0.37      0.36       325
     neutral       0.16      0.08      0.10        92
    positive       0.58      0.61      0.60       583

    accuracy                           0.48      1000
   macro avg       0.36      0.35      0.35      1000
weighted avg       0.47      0.48      0.47      1000


real	0m7.099s
user	0m6.202s
sys	0m1.429s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

If you run with "average=micro", the P, R and F1 results will be the same as Accuracy score as follows:  
```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./knn-classifier.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
KNN, Unigram Counts
Train score: 0.61 ; Validation score: 0.51

KNN, Unigram Tf-Idf
Train score: 0.62 ; Validation score: 0.5

KNN, Bigram Counts
Train score: 0.63 ; Validation score: 0.5

KNN, Bigram Tf-Idf
Train score: 0.62 ; Validation score: 0.48

KNN Test Result, Unigram Counts:  0.497
Error Rate: 0.50
----------
Accuracy: 0.497
Precision: 0.497
Recall: 0.497
F1 Score: 0.497

KNN Test Result, Unigram Tf-Idf:  0.487
Error Rate: 0.51
----------
Accuracy: 0.487
Precision: 0.487
Recall: 0.487
F1 Score: 0.487

KNN Test Result, Bigram Count:  0.496
Error Rate: 0.50
----------
Accuracy: 0.496
Precision: 0.496
Recall: 0.496
F1 Score: 0.496

KNN Test Result, Bigram Tf-Idf:  0.483
Error Rate: 0.52
----------
Accuracy: 0.483
Precision: 0.483
Recall: 0.483
F1 Score: 0.483

real	0m6.880s
user	0m5.938s
sys	0m1.427s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

## D-Tree Result with F1, P and R

Updated python code for D-Tree is as follows:  

```python
## Decision Tree Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 8 Feb 2023
## Reference:
## https://towardsdatascience.com/building-a-sentiment-classifier-using-scikit-learn-54c8e7c5d2f0
## https://vitalflux.com/accuracy-precision-recall-f1-score-python-example/  
## https://stackoverflow.com/questions/62792001/precision-and-recall-are-the-same-within-a-model
## https://towardsdatascience.com/micro-macro-weighted-averages-of-f1-score-clearly-explained-b603420b292f
## https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html

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
from sklearn.metrics import classification_report

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
print('----------')
print(classification_report(y_test, y_predict))
print('')

dtree_unigram_tfidf = load('classifiers/dtree_unigram_tf-idf.joblib')
score = dtree_unigram_tfidf.score(X_test, y_test)
print('Decision Tree Test Result, Unigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = dtree_unigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

X_test = bigram_vectorizer.transform(polar_test['text'].values)
X_test = bigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

dtree_bigram_counts = load('classifiers/dtree_bigram_count.joblib')
score = dtree_bigram_counts.score(X_test, y_test)
print('Decision Tree Test Result, Bigram Count: ', score)
print('----------')
print(classification_report(y_test, y_predict))
print('')

# Predict the class of test set
y_predict = dtree_bigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

dtree_bigram_tfidf = load('classifiers/dtree_bigram_tf-idf.joblib')
score = dtree_bigram_tfidf.score(X_test, y_test)
print('Decision Tree Test Result, Bigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = dtree_bigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')
```

D-Tree results with F1, P and R are as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./dtree-classifier.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
DTREE, Unigram Counts
Train score: 0.83 ; Validation score: 0.52

DTREE, Unigram Tf-Idf
Train score: 0.83 ; Validation score: 0.53

DTREE, Bigram Counts
Train score: 0.83 ; Validation score: 0.53

DTREE, Bigram Tf-Idf
Train score: 0.83 ; Validation score: 0.53

Decision Tree Test Result, Unigram Counts:  0.546
Error Rate: 0.45
----------
              precision    recall  f1-score   support

    negative       0.42      0.26      0.32       325
     neutral       0.15      0.08      0.10        92
    positive       0.61      0.78      0.68       583

    accuracy                           0.55      1000
   macro avg       0.39      0.37      0.37      1000
weighted avg       0.50      0.55      0.51      1000


Decision Tree Test Result, Unigram Tf-Idf:  0.524
Error Rate: 0.48
----------
              precision    recall  f1-score   support

    negative       0.40      0.32      0.35       325
     neutral       0.13      0.07      0.09        92
    positive       0.60      0.71      0.65       583

    accuracy                           0.52      1000
   macro avg       0.37      0.36      0.36      1000
weighted avg       0.49      0.52      0.50      1000


Decision Tree Test Result, Bigram Count:  0.553
----------
              precision    recall  f1-score   support

    negative       0.40      0.32      0.35       325
     neutral       0.13      0.07      0.09        92
    positive       0.60      0.71      0.65       583

    accuracy                           0.52      1000
   macro avg       0.37      0.36      0.36      1000
weighted avg       0.49      0.52      0.50      1000


Error Rate: 0.45
----------
              precision    recall  f1-score   support

    negative       0.33      0.10      0.15       325
     neutral       0.07      0.01      0.02        92
    positive       0.58      0.89      0.71       583

    accuracy                           0.55      1000
   macro avg       0.33      0.33      0.29      1000
weighted avg       0.45      0.55      0.46      1000


Decision Tree Test Result, Bigram Tf-Idf:  0.543
Error Rate: 0.46
----------
              precision    recall  f1-score   support

    negative       0.41      0.30      0.35       325
     neutral       0.18      0.08      0.11        92
    positive       0.61      0.75      0.67       583

    accuracy                           0.54      1000
   macro avg       0.40      0.38      0.38      1000
weighted avg       0.50      0.54      0.51      1000



real	0m2.581s
user	0m2.586s
sys	0m0.648s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ 
```

## Random Forest Results with F1, P and R

I updated the code as follows:  

```python
## Random Forest Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 8 Feb 2023
## Reference:
## https://towardsdatascience.com/building-a-sentiment-classifier-using-scikit-learn-54c8e7c5d2f0
## https://vitalflux.com/accuracy-precision-recall-f1-score-python-example/  
## https://stackoverflow.com/questions/62792001/precision-and-recall-are-the-same-within-a-model
## https://towardsdatascience.com/micro-macro-weighted-averages-of-f1-score-clearly-explained-b603420b292f
## https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html

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

# Import the Random Forests library
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report

def train_and_show_scores_RFOREST(X: csr_matrix, y: np.array, title: str, model: str) -> None:
    X_train, X_valid, y_train, y_valid = train_test_split(
        X, y, train_size=0.75, stratify=y
    )

    clf = RandomForestClassifier()
    clf.fit(X_train, y_train)
    train_score = clf.score(X_train, y_train)
    valid_score = clf.score(X_valid, y_valid)
    print(f'{title}\nTrain score: {round(train_score, 2)} ; Validation score: {round(valid_score, 2)}\n')

    #saving model
    dump(clf, 'classifiers/' + model)

y_train = polar_train['label'].values

train_and_show_scores_RFOREST(X_train_unigram, y_train, 'RFOREST, Unigram Counts', 'rforest_unigram_count.joblib')
train_and_show_scores_RFOREST(X_train_unigram_tf_idf, y_train, 'RFOREST, Unigram Tf-Idf', 'rforest_unigram_tf-idf.joblib')
train_and_show_scores_RFOREST(X_train_bigram, y_train, 'RFOREST, Bigram Counts', 'rforest_bigram_count.joblib')
train_and_show_scores_RFOREST(X_train_bigram_tf_idf, y_train, 'RFOREST, Bigram Tf-Idf', 'rforest_bigram_tf-idf.joblib')


### Testing/Evaluation

X_test = unigram_vectorizer.transform(polar_test['text'].values)
X_test = unigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

rforest_unigram_counts = load('classifiers/rforest_unigram_count.joblib')
score = rforest_unigram_counts.score(X_test, y_test)
print('Random Forest Test Result, Unigram Counts: ', score)

# Predict the class of test set
y_predict = rforest_unigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

rforest_unigram_tfidf = load('classifiers/rforest_unigram_tf-idf.joblib')
score = rforest_unigram_tfidf.score(X_test, y_test)
print('Random Forest Test Result, Unigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = rforest_unigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

X_test = bigram_vectorizer.transform(polar_test['text'].values)
X_test = bigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

rforest_bigram_counts = load('classifiers/rforest_bigram_count.joblib')
score = rforest_bigram_counts.score(X_test, y_test)
print('Random Forest Test Result, Bigram Count: ', score)

# Predict the class of test set
y_predict = rforest_bigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

rforest_bigram_tfidf = load('classifiers/rforest_bigram_tf-idf.joblib')
score = rforest_bigram_tfidf.score(X_test, y_test)
print('Random Forest Test Result, Bigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = rforest_bigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')
```

The Random Forest results with F1, P and R are as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./rforest-classifier.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
RFOREST, Unigram Counts
Train score: 0.83 ; Validation score: 0.56

RFOREST, Unigram Tf-Idf
Train score: 0.83 ; Validation score: 0.57

RFOREST, Bigram Counts
Train score: 0.84 ; Validation score: 0.58

RFOREST, Bigram Tf-Idf
Train score: 0.84 ; Validation score: 0.58

Random Forest Test Result, Unigram Counts:  0.565
Error Rate: 0.43
----------
              precision    recall  f1-score   support

    negative       0.44      0.22      0.30       325
     neutral       0.09      0.02      0.04        92
    positive       0.60      0.84      0.70       583

    accuracy                           0.56      1000
   macro avg       0.38      0.36      0.34      1000
weighted avg       0.50      0.56      0.51      1000


Random Forest Test Result, Unigram Tf-Idf:  0.588
Error Rate: 0.41
----------
              precision    recall  f1-score   support

    negative       0.46      0.23      0.31       325
     neutral       0.43      0.03      0.06        92
    positive       0.61      0.87      0.72       583

    accuracy                           0.59      1000
   macro avg       0.50      0.38      0.36      1000
weighted avg       0.55      0.59      0.53      1000


Random Forest Test Result, Bigram Count:  0.559
Error Rate: 0.44
----------
              precision    recall  f1-score   support

    negative       0.36      0.10      0.16       325
     neutral       0.09      0.01      0.02        92
    positive       0.59      0.90      0.71       583

    accuracy                           0.56      1000
   macro avg       0.35      0.34      0.30      1000
weighted avg       0.47      0.56      0.47      1000


Random Forest Test Result, Bigram Tf-Idf:  0.602
Error Rate: 0.40
----------
              precision    recall  f1-score   support

    negative       0.53      0.21      0.30       325
     neutral       0.17      0.01      0.02        92
    positive       0.62      0.91      0.74       583

    accuracy                           0.60      1000
   macro avg       0.44      0.38      0.35      1000
weighted avg       0.55      0.60      0.53      1000



real	0m30.863s
user	0m30.592s
sys	0m0.766s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ 
```

## SVM Result with F1, P and R

Updated code:  

```python
## Support Vector Machine Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 8 Feb 2023
## Reference:
## https://towardsdatascience.com/building-a-sentiment-classifier-using-scikit-learn-54c8e7c5d2f0
## https://vitalflux.com/accuracy-precision-recall-f1-score-python-example/  
## https://stackoverflow.com/questions/62792001/precision-and-recall-are-the-same-within-a-model
## https://towardsdatascience.com/micro-macro-weighted-averages-of-f1-score-clearly-explained-b603420b292f
## https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html

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

# Import SVM library
from sklearn import svm
from sklearn.metrics import classification_report

def train_and_show_scores_SVM(X: csr_matrix, y: np.array, title: str, model: str) -> None:
    X_train, X_valid, y_train, y_valid = train_test_split(
        X, y, train_size=0.75, stratify=y
    )

    clf = svm.SVC(kernel='linear', C=1)
    clf.fit(X_train, y_train)
    train_score = clf.score(X_train, y_train)
    valid_score = clf.score(X_valid, y_valid)
    print(f'{title}\nTrain score: {round(train_score, 2)} ; Validation score: {round(valid_score, 2)}\n')

    #saving model
    dump(clf, 'classifiers/' + model)

y_train = polar_train['label'].values

train_and_show_scores_SVM(X_train_unigram, y_train, 'SVM, Unigram Counts', 'svm_unigram_count.joblib')
train_and_show_scores_SVM(X_train_unigram_tf_idf, y_train, 'SVM, Unigram Tf-Idf', 'svm_unigram_tf-idf.joblib')
train_and_show_scores_SVM(X_train_bigram, y_train, 'SVM, Bigram Counts', 'svm_bigram_count.joblib')
train_and_show_scores_SVM(X_train_bigram_tf_idf, y_train, 'SVM, Bigram Tf-Idf', 'svm_bigram_tf-idf.joblib')


### Testing/Evaluation

X_test = unigram_vectorizer.transform(polar_test['text'].values)
X_test = unigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

svm_unigram_counts = load('classifiers/svm_unigram_count.joblib')
score = svm_unigram_counts.score(X_test, y_test)
print('SVM Test Result, Unigram Counts: ', score)

# Predict the class of test set
y_predict = svm_unigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')
svm_unigram_tfidf = load('classifiers/svm_unigram_tf-idf.joblib')
score = svm_unigram_tfidf.score(X_test, y_test)
print('SVM Test Result, Unigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = svm_unigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

X_test = bigram_vectorizer.transform(polar_test['text'].values)
X_test = bigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

svm_bigram_counts = load('classifiers/svm_bigram_count.joblib')
score = svm_bigram_counts.score(X_test, y_test)
print('SVM Test Result, Bigram Count: ', score)

# Predict the class of test set
y_predict = svm_bigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

svm_bigram_tfidf = load('classifiers/svm_bigram_tf-idf.joblib')
score = svm_bigram_tfidf.score(X_test, y_test)
print('SVM Test Result, Bigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = svm_bigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')
```

SVM result with F1, P and R:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./svm-classifier.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
SVM, Unigram Counts
Train score: 0.63 ; Validation score: 0.58

SVM, Unigram Tf-Idf
Train score: 0.6 ; Validation score: 0.58

SVM, Bigram Counts
Train score: 0.77 ; Validation score: 0.57

SVM, Bigram Tf-Idf
Train score: 0.69 ; Validation score: 0.59

SVM Test Result, Unigram Counts:  0.586
Error Rate: 0.41
----------
              precision    recall  f1-score   support

    negative       0.62      0.02      0.05       325
     neutral       0.00      0.00      0.00        92
    positive       0.59      0.99      0.74       583

    accuracy                           0.59      1000
   macro avg       0.40      0.34      0.26      1000
weighted avg       0.54      0.59      0.44      1000


SVM Test Result, Unigram Tf-Idf:  0.583
Error Rate: 0.42
----------
              precision    recall  f1-score   support

    negative       0.48      0.09      0.15       325
     neutral       0.00      0.00      0.00        92
    positive       0.59      0.95      0.73       583

    accuracy                           0.58      1000
   macro avg       0.36      0.35      0.29      1000
weighted avg       0.50      0.58      0.47      1000


SVM Test Result, Bigram Count:  0.58
Error Rate: 0.42
----------
              precision    recall  f1-score   support

    negative       0.27      0.01      0.02       325
     neutral       0.00      0.00      0.00        92
    positive       0.58      0.99      0.73       583

    accuracy                           0.58      1000
   macro avg       0.29      0.33      0.25      1000
weighted avg       0.43      0.58      0.43      1000


SVM Test Result, Bigram Tf-Idf:  0.593
Error Rate: 0.41
----------
              precision    recall  f1-score   support

    negative       0.50      0.18      0.27       325
     neutral       1.00      0.01      0.02        92
    positive       0.60      0.91      0.73       583

    accuracy                           0.59      1000
   macro avg       0.70      0.37      0.34      1000
weighted avg       0.61      0.59      0.51      1000



real	0m16.666s
user	0m16.601s
sys	0m0.543s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

## SGD Result with F1, P and R

updated python code:  

```python
## Stochastic Gradient Descent Classifier for Khmer Polarity
## Written by Ye Kyaw Thu, 
## Affiliate Professor, IDRI, CADT, Cambodia
## Used for 4th NLP/AI Workshop, Chiang Mai, Experiment
## Last updated: 8 Feb 2023
## Reference:
## https://towardsdatascience.com/building-a-sentiment-classifier-using-scikit-learn-54c8e7c5d2f0
## https://vitalflux.com/accuracy-precision-recall-f1-score-python-example/  
## https://stackoverflow.com/questions/62792001/precision-and-recall-are-the-same-within-a-model
## https://towardsdatascience.com/micro-macro-weighted-averages-of-f1-score-clearly-explained-b603420b292f
## https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html

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
from sklearn.linear_model import SGDClassifier
from sklearn.metrics import classification_report

def train_and_show_scores_SGD(X: csr_matrix, y: np.array, title: str, model: str) -> None:
    X_train, X_valid, y_train, y_valid = train_test_split(
        X, y, train_size=0.75, stratify=y
    )

    clf = SGDClassifier()
    clf.fit(X_train, y_train)
    train_score = clf.score(X_train, y_train)
    valid_score = clf.score(X_valid, y_valid)
    print(f'{title}\nTrain score: {round(train_score, 2)} ; Validation score: {round(valid_score, 2)}\n')

    #saving model
    dump(clf, 'classifiers/' + model)

y_train = polar_train['label'].values

train_and_show_scores_SGD(X_train_unigram, y_train, 'SGD, Unigram Counts', 'sgd_unigram_count.joblib')
train_and_show_scores_SGD(X_train_unigram_tf_idf, y_train, 'SGD, Unigram Tf-Idf', 'sgd_unigram_tf-idf.joblib')
train_and_show_scores_SGD(X_train_bigram, y_train, 'SGD, Bigram Counts', 'sgd_bigram_count.joblib')
train_and_show_scores_SGD(X_train_bigram_tf_idf, y_train, 'SGD, Bigram Tf-Idf', 'sgd_bigram_tf-idf.joblib')


### Testing/Evaluation

X_test = unigram_vectorizer.transform(polar_test['text'].values)
X_test = unigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

sgd_unigram_counts = load('classifiers/sgd_unigram_count.joblib')
score = sgd_unigram_counts.score(X_test, y_test)
print('SGD Test Result, Unigram Counts: ', score)

# Predict the class of test set
y_predict = sgd_unigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

sgd_unigram_tfidf = load('classifiers/sgd_unigram_tf-idf.joblib')
score = sgd_unigram_tfidf.score(X_test, y_test)
print('SGD Test Result, Unigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = sgd_unigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

X_test = bigram_vectorizer.transform(polar_test['text'].values)
X_test = bigram_tf_idf_transformer.transform(X_test)
y_test = polar_test['label'].values

sgd_bigram_counts = load('classifiers/sgd_bigram_count.joblib')
score = sgd_bigram_counts.score(X_test, y_test)
print('SGD Test Result, Bigram Count: ', score)

# Predict the class of test set
y_predict = sgd_bigram_counts.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')

sgd_bigram_tfidf = load('classifiers/sgd_bigram_tf-idf.joblib')
score = sgd_bigram_tfidf.score(X_test, y_test)
print('SGD Test Result, Bigram Tf-Idf: ', score)

# Predict the class of test set
y_predict = sgd_bigram_tfidf.predict(X_test)

err_rate = (y_predict != y_test).mean()
print('Error Rate: %.2f' % err_rate)
print('----------')
print(classification_report(y_test, y_predict))
print('')
```

SGD result with F1, P and R are as follows:  

```
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$ time python ./sgd-classifier2.py 
mkdir: cannot create directory ‘data_preprocessors’: File exists
mkdir: cannot create directory ‘vectorized_data’: File exists
SGD, Unigram Counts
Train score: 0.63 ; Validation score: 0.59

SGD, Unigram Tf-Idf
Train score: 0.63 ; Validation score: 0.59

SGD, Bigram Counts
Train score: 0.78 ; Validation score: 0.59

SGD, Bigram Tf-Idf
Train score: 0.74 ; Validation score: 0.58

SGD Test Result, Unigram Counts:  0.588
Error Rate: 0.41
----------
              precision    recall  f1-score   support

    negative       0.59      0.05      0.10       325
     neutral       0.20      0.01      0.02        92
    positive       0.59      0.98      0.74       583

    accuracy                           0.59      1000
   macro avg       0.46      0.35      0.28      1000
weighted avg       0.55      0.59      0.46      1000


SGD Test Result, Unigram Tf-Idf:  0.587
Error Rate: 0.41
----------
              precision    recall  f1-score   support

    negative       0.50      0.12      0.19       325
     neutral       0.30      0.03      0.06        92
    positive       0.60      0.94      0.73       583

    accuracy                           0.59      1000
   macro avg       0.47      0.36      0.33      1000
weighted avg       0.54      0.59      0.49      1000


SGD Test Result, Bigram Count:  0.567
Error Rate: 0.43
----------
              precision    recall  f1-score   support

    negative       0.36      0.08      0.14       325
     neutral       0.50      0.04      0.08        92
    positive       0.58      0.92      0.71       583

    accuracy                           0.57      1000
   macro avg       0.48      0.35      0.31      1000
weighted avg       0.50      0.57      0.47      1000


SGD Test Result, Bigram Tf-Idf:  0.583
Error Rate: 0.42
----------
              precision    recall  f1-score   support

    negative       0.45      0.25      0.32       325
     neutral       0.17      0.01      0.02        92
    positive       0.62      0.86      0.72       583

    accuracy                           0.58      1000
   macro avg       0.41      0.37      0.35      1000
weighted avg       0.52      0.58      0.52      1000



real	0m1.609s
user	0m1.678s
sys	0m0.679s
(tabpfn) yekyaw.thu@gpu:~/exp/kh-polar/run-for-f1$
```

## SGD Tuning Result with F1, P and R

updated python code:  

```python

```

SGD Tuning result with F1, P and R:  

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

## Reference

[1] https://vitalflux.com/accuracy-precision-recall-f1-score-python-example/  
[2] https://stackoverflow.com/questions/62792001/precision-and-recall-are-the-same-within-a-model
[3] https://towardsdatascience.com/micro-macro-weighted-averages-of-f1-score-clearly-explained-b603420b292f
[4] https://scikit-learn.org/stable/modules/generated/sklearn.metrics.classification_report.html



