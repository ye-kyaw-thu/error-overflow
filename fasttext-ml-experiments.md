# FastText + ML based Sentence Tagging

## Installation of sklearn_crfsuite Library  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ /home/ye/anaconda3/envs/hs-fasttext/bin/python -m pip install sklearn_crfsuite
Collecting sklearn_crfsuite
  Downloading sklearn_crfsuite-0.5.0-py2.py3-none-any.whl.metadata (4.9 kB)
Requirement already satisfied: python-crfsuite>=0.9.7 in /home/ye/.local/lib/python3.10/site-packages (from sklearn_crfsuite) (0.9.11)
Requirement already satisfied: scikit-learn>=0.24.0 in /home/ye/.local/lib/python3.10/site-packages (from sklearn_crfsuite) (1.4.1.post1)
Requirement already satisfied: tabulate>=0.4.2 in /home/ye/.local/lib/python3.10/site-packages (from sklearn_crfsuite) (0.9.0)
Requirement already satisfied: tqdm>=2.0 in /home/ye/.local/lib/python3.10/site-packages (from sklearn_crfsuite) (4.66.2)
Requirement already satisfied: numpy<2.0,>=1.19.5 in /home/ye/.local/lib/python3.10/site-packages (from scikit-learn>=0.24.0->sklearn_crfsuite) (1.24.3)
Requirement already satisfied: scipy>=1.6.0 in /home/ye/.local/lib/python3.10/site-packages (from scikit-learn>=0.24.0->sklearn_crfsuite) (1.12.0)
Requirement already satisfied: joblib>=1.2.0 in /home/ye/.local/lib/python3.10/site-packages (from scikit-learn>=0.24.0->sklearn_crfsuite) (1.3.2)
Requirement already satisfied: threadpoolctl>=2.0.0 in /home/ye/.local/lib/python3.10/site-packages (from scikit-learn>=0.24.0->sklearn_crfsuite) (3.3.0)
Downloading sklearn_crfsuite-0.5.0-py2.py3-none-any.whl (10 kB)
Installing collected packages: sklearn_crfsuite
Successfully installed sklearn_crfsuite-0.5.0

[notice] A new release of pip is available: 24.2 -> 24.3.1
[notice] To update, run: python -m pip install --upgrade pip

```

call --help  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./fasttext-ml.py --help
usage: fasttext-ml.py [-h] [--train TRAIN] [--test TEST] [--real-time REAL_TIME] [--ft-model FT_MODEL]
                      [--model MODEL] [--method {Decision-Tree,Random-Forest,Logistic-Regression,CRF}]
                      [--evaluate]

FastText + ML Models for Burmese Sentence Segmentation.

options:
  -h, --help            show this help message and exit
  --train TRAIN         Train the model. Provide the training corpus file path.
  --test TEST           Test the model. Provide the test corpus file path.
  --real-time REAL_TIME
                        Segment raw text in real-time. Provide the input text.
  --ft-model FT_MODEL   FastText model file (default: fasttext_model.bin).
  --model MODEL         Trained model file (default: model.pkl).
  --method {Decision-Tree,Random-Forest,Logistic-Regression,CRF}, -m {Decision-Tree,Random-Forest,Logistic-Regression,CRF}
                        Choose the classification method (default: Decision-Tree).
  --evaluate            Evaluate the model during testing if reference data is provided.
```

## Training with Decision Tree

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --model ./syl.bone.fasttest.DT.model --method Decision-
Tree
Loading training data...
Training FastText model...
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   36558 lr:  0.000000 avg.loss:  2.305969 ETA:   0h 0m 0s
Preparing features for Decision-Tree...
Training Decision-Tree model...
Saving trained model to ./syl.bone.fasttest.DT.model...
Training completed.

real    1m28.575s
user    4m33.308s
sys     0m6.095s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

testing/evaluation ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --model ./syl.bone.fasttest.DT.model --method Decision-Tree --e
valuate
Loading tagged test data...
Loading FastText and trained model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features for testing...
              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m3.782s
user    0m6.246s
sys     0m4.470s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Train/Test Random Forest  

training ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.p
y --train ./data/syl/bone/train-valid.tagged.bone --model ./syl.bone.fasttest.RF.model --method Random-Forest
Loading training data...
Training FastText model...
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   36544 lr:  0.000000 avg.loss:  2.293172 ETA:   0h 0m 0s
Preparing features...
Training Random-Forest model...
Saving trained model to ./syl.bone.fasttest.RF.model...
Training completed.

real    8m50.897s
user    11m51.048s
sys     0m9.487s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

testing/evaluation ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --model ./syl.bone.fasttest.RF.model --method Random-Forest --evaluate
Loading tagged test data...
Loading FastText and trained model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features...
Predicting...
              precision    recall  f1-score   support

           B       0.57      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m6.329s
user    0m8.985s
sys     0m4.261s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Train/Test Logistic Regression  

training ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --model ./syl.bone.fasttest.RL.model --method Logistic-Regression
Loading training data...
Training FastText model...
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   35950 lr:  0.000000 avg.loss:  2.309337 ETA:   0h 0m 0s
Preparing features...
Training Logistic-Regression model...
Saving trained model to ./syl.bone.fasttest.RL.model...
Training completed.

real    1m2.691s
user    16m19.877s
sys     5m29.185s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

testing/evaluation ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --model ./syl.bone.fasttest.RL.model --method Logistic-Regression --evaluate
Loading tagged test data...
Loading FastText and trained model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features...
Predicting...
              precision    recall  f1-score   support

           B       0.58      0.07      0.12      6861
           E       0.72      0.72      0.72      6829
           N       0.63      0.10      0.17     19728
           O       0.81      0.98      0.89    110355

    accuracy                           0.80    143773
   macro avg       0.68      0.47      0.48    143773
weighted avg       0.77      0.80      0.74    143773


real    0m4.014s
user    0m8.001s
sys     0m6.407s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Train/Test CRF  

training ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --model ./syl.bone.fasttest.CRF.model --method CRF
Loading training data...
Training FastText model...
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   36540 lr:  0.000000 avg.loss:  2.301345 ETA:   0h 0m 0s
Preparing features for CRF...
Training CRF model...
Saving trained model to ./syl.bone.fasttest.CRF.model...
Training completed.

real    6m19.588s
user    8m58.798s
sys     0m29.854s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

testing/evaluation ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --model ./syl.bone.fasttest.CRF.model --method CRF --evaluate
Loading tagged test data...
Loading FastText and trained model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Preparing features for testing...
              precision    recall  f1-score   support

           B       0.90      0.54      0.68      6861
           E       0.90      0.54      0.68      6829
           N       0.85      0.32      0.47     19728
           O       0.85      0.99      0.91    110355

    accuracy                           0.85    143773
   macro avg       0.88      0.60      0.68    143773
weighted avg       0.85      0.85      0.83    143773


real    0m17.536s
user    0m17.702s
sys     0m6.653s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

လက်ရှိအချိန်ထိ CRF model နဲ့က အကောင်းဆုံး ရလဒ်ပဲ။   

Decision Tree = 0.81  
Random Forest = 0.81  
Logistic-Regression = 0.80  
CRF = 0.85 is the best!  

## Train/Test Adaboost



training ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --model syl.bone.adaboost.model --method AdaBoost | tee
 adaboost-training.log
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   26504 lr:  0.000000 avg.loss:  2.301549 ETA:   0h 0m 0s
/home/ye/.local/lib/python3.10/site-packages/sklearn/ensemble/_weight_boosting.py:519: FutureWarning: The SAMME.R algorithm (the default) is deprecated and will be removed in 1.6. Use the SAMME algorithm to circumvent this warning.
  warnings.warn(
Loading training data...
Training FastText model...
Preparing features for AdaBoost...
Training AdaBoost model...
Saving trained model to syl.bone.adaboost.model...
Training completed.

real    9m33.665s
user    12m32.626s
sys     0m6.395s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --model syl.bone.adaboost.model --method AdaBoost --evaluate |
tee adaboost-testing.log
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Loading tagged test data...
Loading FastText and trained model...
Preparing features for testing...
              precision    recall  f1-score   support

           B       0.09      0.00      0.00      6861
           E       0.73      0.56      0.63      6829
           N       0.54      0.11      0.18     19728
           O       0.80      0.98      0.88    110355

    accuracy                           0.79    143773
   macro avg       0.54      0.41      0.42    143773
weighted avg       0.73      0.79      0.73    143773


real    0m5.323s
user    0m6.763s
sys     0m4.673s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Train/Test with Gradient-Boosting  

```

```

```

```

```

```

## Updated the Python Script

HMM ကို ထည့်ဖို့ စဉ်းစားတော့ fasttext feature နဲ့က အဆင်မပြေဘူး။  
--method all ကို ထည့်ခဲ့တယ်။ လက်တွေ့ experiment လုပ်တဲ့အခါမှာက method အားလုံးကို run မှာမို့လို့။ ပြီးတော့ convenient ဖြစ်အောင်လို့ ML method တစ်မျိုးခြင်းစီလည်း run ချင်ရင် run လို့ ရအောင် ထားထားတယ်။ 

Loging feature လည်း ထည့်ခဲ့တယ်။  

```python
import argparse
import os
import fasttext
import numpy as np
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier, AdaBoostClassifier, GradientBoostingClassifier, VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn_crfsuite import CRF
from sklearn_crfsuite.metrics import flat_classification_report
from sklearn.metrics import classification_report
import joblib
import logging


def load_tagged_data(file_path):
    """Load tagged corpus and return sentences and labels."""
    sentences, labels = [], []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            tokens = line.strip().split()
            for token in tokens:
                if "/" in token:
                    word, label = token.rsplit("/", 1)
                    sentences.append(word)
                    labels.append(label)
    return sentences, labels


def load_raw_data(file_path):
    """Load raw text without tags."""
    sentences = []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            sentences.extend(line.strip().split())
    return sentences


def prepare_features(sentences, ft_model):
    """Generate embeddings for sentences using FastText."""
    return np.array([ft_model.get_word_vector(word) for word in sentences])


def prepare_features_for_crf(sentences, ft_model):
    """Prepare features for CRF."""
    return [[{'dim_' + str(i): val for i, val in enumerate(ft_model.get_word_vector(word))} for word in sentences]]


def train_model(train_file, ft_model_file, output_model_file, method, logger):
    """Train the model based on the selected method."""
    logger.info(f"Loading training data for {method}...")
    sentences, labels = load_tagged_data(train_file)

    # Check if the FastText model already exists
    if os.path.exists(ft_model_file):
        logger.info(f"Loading existing FastText model from {ft_model_file}...")
        ft_model = fasttext.load_model(ft_model_file)
    else:
        logger.info(f"Training FastText model for {method}...")
        ft_model = fasttext.train_unsupervised(train_file, model='skipgram')
        ft_model.save_model(ft_model_file)

    logger.info(f"Preparing features for {method}...")
    if method == "CRF":
        X = prepare_features_for_crf(sentences, ft_model)
        y = [labels]
    else:
        X = prepare_features(sentences, ft_model)
        y = np.array(labels)

    logger.info(f"Training {method} model...")
    if method == "Decision-Tree":
        model = DecisionTreeClassifier()
    elif method == "Random-Forest":
        model = RandomForestClassifier()
    elif method == "Logistic-Regression":
        model = LogisticRegression(max_iter=1000)
    elif method == "CRF":
        model = CRF(algorithm='lbfgs', max_iterations=100, all_possible_transitions=True)
    elif method == "AdaBoost":
        model = AdaBoostClassifier(n_estimators=50)
    elif method == "GradientBoosting":
        model = GradientBoostingClassifier()
    elif method == "Voting":
        model = VotingClassifier(estimators=[
            ('rf', RandomForestClassifier()),
            ('lr', LogisticRegression(max_iter=1000)),
            ('dt', DecisionTreeClassifier())
        ], voting='hard')
    else:
        raise ValueError(f"Unsupported method: {method}")

    model.fit(X, y)
    logger.info(f"Saving trained model to {output_model_file}...")
    joblib.dump(model, output_model_file)
    if os.path.exists(output_model_file):
        logger.info(f"Model saved successfully: {output_model_file}")
    else:
        logger.error(f"Failed to save model: {output_model_file}")
    logger.info(f"Training for {method} completed.")


def test_model(test_file, ft_model_file, trained_model_file, evaluate, method, logger):
    """Test the model on the provided test data."""
    logger.info(f"Testing {method} model...")
    if evaluate:
        sentences, labels = load_tagged_data(test_file)
    else:
        sentences = load_raw_data(test_file)
        labels = None

    ft_model = fasttext.load_model(ft_model_file)
    model = joblib.load(trained_model_file)

    logger.info(f"Preparing features for {method} testing...")
    if method == "CRF":
        X = prepare_features_for_crf(sentences, ft_model)
        predictions = model.predict(X)[0]
    else:
        X = prepare_features(sentences, ft_model)
        predictions = model.predict(X)

    if evaluate:
        if method == "CRF":
            logger.info(flat_classification_report([labels], [predictions]))
        else:
            logger.info(classification_report(labels, predictions))
    else:
        for word, label in zip(sentences, predictions):
            logger.info(f"{word}/{label}")


def main():
    parser = argparse.ArgumentParser(description="FastText + ML Models for Sentence Segmentation.")
    parser.add_argument("--train", help="Train the model. Provide the training corpus file path.")
    parser.add_argument("--test", help="Test the model. Provide the test corpus file path.")
    parser.add_argument("--ft-model", default="fasttext_model.bin", help="FastText model file (default: fasttext_model.bin).")
    parser.add_argument("--model", default="model.pkl", help="Trained model file (default: model.pkl).")
    parser.add_argument("--method", "-m", default="Decision-Tree",
                        choices=["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting", "all"],
                        help="Choose the classification method (default: Decision-Tree).")
    parser.add_argument("--evaluate", action="store_true", help="Evaluate the model during testing if reference data is provided.")

    args = parser.parse_args()

    logging.basicConfig(filename="all-training-testing.log" if args.method == "all" else None,
                        level=logging.INFO,
                        format="%(asctime)s - %(message)s")
    logger = logging.getLogger()

    methods = ["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting"] \
        if args.method == "all" else [args.method]

    if args.train:
        for method in methods:
            model_file = f"{method.lower().replace('-', '_')}.model"
            train_model(args.train, args.ft_model, model_file, method, logger)
    elif args.test:
        for method in methods:
            model_file = f"{method.lower().replace('-', '_')}.model"
            test_model(args.test, args.ft_model, model_file, args.evaluate, method, logger)
    else:
        parser.print_help()


if __name__ == "__main__":
    main()


```

Call --help  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./fasttext-ml.py --help
usage: fasttext-ml.py [-h] [--train TRAIN] [--test TEST] [--ft-model FT_MODEL] [--model MODEL]
                      [--method {Decision-Tree,Random-Forest,Logistic-Regression,CRF,AdaBoost,GradientBoosting,Voting,all}]
                      [--evaluate]

FastText + ML Models for Sentence Segmentation.

options:
  -h, --help            show this help message and exit
  --train TRAIN         Train the model. Provide the training corpus file path.
  --test TEST           Test the model. Provide the test corpus file path.
  --ft-model FT_MODEL   FastText model file (default: fasttext_model.bin).
  --model MODEL         Trained model file (default: model.pkl).
  --method {Decision-Tree,Random-Forest,Logistic-Regression,CRF,AdaBoost,GradientBoosting,Voting,all}, -m {Decision-Tree,Random-Forest,Logistic-Regression,CRF,AdaBoost,GradientBoosting,Voting,all}
                        Choose the classification method (default: Decision-Tree).
  --evaluate            Evaluate the model during testing if reference data is provided.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Updating ...  

```python
import argparse
import os
import fasttext
import numpy as np
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier, AdaBoostClassifier, GradientBoostingClassifier, VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn_crfsuite import CRF
from sklearn_crfsuite.metrics import flat_classification_report
from sklearn.metrics import classification_report
import joblib
import logging


def load_tagged_data(file_path):
    """Load tagged corpus and return sentences and labels."""
    sentences, labels = [], []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            tokens = line.strip().split()
            for token in tokens:
                if "/" in token:
                    word, label = token.rsplit("/", 1)
                    sentences.append(word)
                    labels.append(label)
    return sentences, labels


def load_raw_data(file_path):
    """Load raw text without tags."""
    sentences = []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            sentences.extend(line.strip().split())
    return sentences


def prepare_features(sentences, ft_model):
    """Generate embeddings for sentences using FastText."""
    return np.array([ft_model.get_word_vector(word) for word in sentences])


def prepare_features_for_crf(sentences, ft_model):
    """Prepare features for CRF."""
    return [[{'dim_' + str(i): val for i, val in enumerate(ft_model.get_word_vector(word))} for word in sentences]]


def train_model(train_file, ft_model_file, output_model_file, method, logger):
    """Train the model based on the selected method."""
    logger.info(f"Loading training data for {method}...")
    sentences, labels = load_tagged_data(train_file)

    # Check if the FastText model already exists
    if os.path.exists(ft_model_file):
        logger.info(f"Loading existing FastText model from {ft_model_file}...")
        ft_model = fasttext.load_model(ft_model_file)
    else:
        logger.info(f"Training FastText model for {method}...")
        ft_model = fasttext.train_unsupervised(train_file, model='skipgram')
        ft_model.save_model(ft_model_file)

    logger.info(f"Preparing features for {method}...")
    if method == "CRF":
        X = prepare_features_for_crf(sentences, ft_model)
        y = [labels]
    else:
        X = prepare_features(sentences, ft_model)
        y = np.array(labels)

    logger.info(f"Training {method} model...")
    if method == "Decision-Tree":
        model = DecisionTreeClassifier()
    elif method == "Random-Forest":
        model = RandomForestClassifier()
    elif method == "Logistic-Regression":
        model = LogisticRegression(max_iter=1000)
    elif method == "CRF":
        model = CRF(algorithm='lbfgs', max_iterations=100, all_possible_transitions=True)
    elif method == "AdaBoost":
        model = AdaBoostClassifier(n_estimators=50)
    elif method == "GradientBoosting":
        model = GradientBoostingClassifier()
    elif method == "Voting":
        model = VotingClassifier(estimators=[
            ('rf', RandomForestClassifier()),
            ('lr', LogisticRegression(max_iter=1000)),
            ('dt', DecisionTreeClassifier())
        ], voting='hard')
    else:
        raise ValueError(f"Unsupported method: {method}")

    model.fit(X, y)
    logger.info(f"Saving trained model to {output_model_file}...")
    
    # Save model and confirm file creation
    try:
        joblib.dump(model, output_model_file)
        if os.path.exists(output_model_file):
            logger.info(f"Model saved successfully: {output_model_file}")
        else:
            logger.error(f"Failed to save model: {output_model_file}")
    except Exception as e:
        logger.error(f"Error saving model: {e}")

    logger.info(f"Training for {method} completed.")


def test_model(test_file, ft_model_file, trained_model_file, evaluate, method, logger):
    """Test the model on the provided test data."""
    logger.info(f"Testing {method} model...")
    if evaluate:
        sentences, labels = load_tagged_data(test_file)
    else:
        sentences = load_raw_data(test_file)
        labels = None

    ft_model = fasttext.load_model(ft_model_file)
    model = joblib.load(trained_model_file)

    logger.info(f"Preparing features for {method} testing...")
    if method == "CRF":
        X = prepare_features_for_crf(sentences, ft_model)
        predictions = model.predict(X)[0]
    else:
        X = prepare_features(sentences, ft_model)
        predictions = model.predict(X)

    if evaluate:
        if method == "CRF":
            logger.info(flat_classification_report([labels], [predictions]))
        else:
            logger.info(classification_report(labels, predictions))
    else:
        for word, label in zip(sentences, predictions):
            logger.info(f"{word}/{label}")


def main():
    parser = argparse.ArgumentParser(description="FastText + ML Models for Sentence Segmentation.")
    parser.add_argument("--train", help="Train the model. Provide the training corpus file path.")
    parser.add_argument("--test", help="Test the model. Provide the test corpus file path.")
    parser.add_argument("--ft-model", default="fasttext_model.bin", help="FastText model file (default: fasttext_model.bin).")
    parser.add_argument("--model", default="model.pkl", help="Trained model file (default: model.pkl).")
    parser.add_argument("--method", "-m", default="Decision-Tree",
                        choices=["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting", "all"],
                        help="Choose the classification method (default: Decision-Tree).")
    parser.add_argument("--evaluate", action="store_true", help="Evaluate the model during testing if reference data is provided.")

    args = parser.parse_args()

    logging.basicConfig(filename="all-training-testing.log" if args.method == "all" else None,
                        level=logging.INFO,
                        format="%(asctime)s - %(message)s")
    logger = logging.getLogger()

    # Check for a single method or 'all'
    if args.method == "all":
        methods = ["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting"]
    else:
        methods = [args.method]

    if args.train:
        for method in methods:
            model_file = f"models/{method}.model"  # Save models to 'models' directory
            train_model(args.train, args.ft_model, model_file, method, logger)
    elif args.test:
        for method in methods:
            model_file = f"models/{method}.model"  # Load models from 'models' directory
            test_model(args.test, args.ft_model, model_file, args.evaluate, method, logger)
    else:
        parser.print_help()


if __name__ == "__main__":
    main()


```

## Training/Testing with All Methods  


```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --method all
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   33269 lr:  0.000000 avg.loss:  2.287360 ETA:   0h 0m 0s
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
/home/ye/.local/lib/python3.10/site-packages/sklearn/ensemble/_weight_boosting.py:519: FutureWarning: The SAMME.R algorithm (the default) is deprecated and will be removed in 1.6. Use the SAMME algorithm to circumvent this warning.
  warnings.warn(
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
/home/ye/.local/lib/python3.10/site-packages/sklearn/ensemble/_weight_boosting.py:519: FutureWarning: The SAMME.R algorithm (the default) is deprecated and will be removed in 1.6. Use the SAMME algorithm to circumvent this warning.
  warnings.warn(
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.


real    169m28.234s
user    196m16.358s
sys     17m21.675s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$

```

Checked output modles:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models$ ll *.model -h
-rw-rw-r-- 1 ye ye  36K Dec  7 15:54 AdaBoost.model
-rw-rw-r-- 1 ye ye  48K Dec  7 15:46 CRF.model
-rw-rw-r-- 1 ye ye 615K Dec  7 15:26 Decision-Tree.model
-rw-rw-r-- 1 ye ye 699K Dec  7 18:03 GradientBoosting.model
-rw-rw-r-- 1 ye ye 4.0K Dec  7 15:40 Logistic-Regression.model
-rw-rw-r-- 1 ye ye  56M Dec  7 15:39 Random-Forest.model
-rw-rw-r-- 1 ye ye  57M Dec  7 18:13 Voting.model
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models$
```

log file ထဲမှာက အောက်ပါအတိုင်း ...  

```
2024-12-07 15:24:29,814 - Loading training data for Decision-Tree...
2024-12-07 15:24:30,465 - Training FastText model for Decision-Tree...
2024-12-07 15:24:38,945 - Preparing features for Decision-Tree...
2024-12-07 15:24:49,919 - Training Decision-Tree model...
2024-12-07 15:26:17,240 - Saving trained model to models/Decision-Tree.model...
2024-12-07 15:26:17,243 - Model saved successfully: models/Decision-Tree.model
2024-12-07 15:26:17,243 - Training for Decision-Tree completed.
2024-12-07 15:26:17,431 - Loading training data for Random-Forest...
2024-12-07 15:26:18,083 - Loading existing FastText model from fasttext_model.bin...
2024-12-07 15:26:18,798 - Preparing features for Random-Forest...
2024-12-07 15:26:29,081 - Training Random-Forest model...
2024-12-07 15:39:01,017 - Saving trained model to models/Random-Forest.model...
2024-12-07 15:39:01,187 - Model saved successfully: models/Random-Forest.model
2024-12-07 15:39:01,187 - Training for Random-Forest completed.
2024-12-07 15:39:01,321 - Loading training data for Logistic-Regression...
2024-12-07 15:39:01,968 - Loading existing FastText model from fasttext_model.bin...
2024-12-07 15:39:02,711 - Preparing features for Logistic-Regression...
2024-12-07 15:39:13,238 - Training Logistic-Regression model...
2024-12-07 15:40:31,767 - Saving trained model to models/Logistic-Regression.model...
2024-12-07 15:40:31,770 - Model saved successfully: models/Logistic-Regression.model
2024-12-07 15:40:31,771 - Training for Logistic-Regression completed.
2024-12-07 15:40:31,958 - Loading training data for CRF...
2024-12-07 15:40:32,604 - Loading existing FastText model from fasttext_model.bin...
2024-12-07 15:40:33,309 - Preparing features for CRF...
2024-12-07 15:41:44,764 - Training CRF model...
2024-12-07 15:46:35,034 - Saving trained model to models/CRF.model...
2024-12-07 15:46:35,044 - Model saved successfully: models/CRF.model
2024-12-07 15:46:35,044 - Training for CRF completed.
2024-12-07 15:46:43,882 - Loading training data for AdaBoost...
2024-12-07 15:46:44,523 - Loading existing FastText model from fasttext_model.bin...
2024-12-07 15:46:44,853 - Preparing features for AdaBoost...
2024-12-07 15:46:55,028 - Training AdaBoost model...
2024-12-07 15:54:45,248 - Saving trained model to models/AdaBoost.model...
2024-12-07 15:54:45,333 - Model saved successfully: models/AdaBoost.model
2024-12-07 15:54:45,333 - Training for AdaBoost completed.
2024-12-07 15:54:45,401 - Loading training data for GradientBoosting...
2024-12-07 15:54:46,047 - Loading existing FastText model from fasttext_model.bin...
2024-12-07 15:54:46,653 - Preparing features for GradientBoosting...
2024-12-07 15:54:56,652 - Training GradientBoosting model...
2024-12-07 18:03:26,718 - Saving trained model to models/GradientBoosting.model...
2024-12-07 18:03:26,802 - Model saved successfully: models/GradientBoosting.model
2024-12-07 18:03:26,802 - Training for GradientBoosting completed.
2024-12-07 18:03:26,879 - Loading training data for Voting...
2024-12-07 18:03:27,535 - Loading existing FastText model from fasttext_model.bin...
2024-12-07 18:03:28,207 - Preparing features for Voting...
2024-12-07 18:03:39,047 - Training Voting model...
2024-12-07 18:13:56,651 - Saving trained model to models/Voting.model...
2024-12-07 18:13:56,820 - Model saved successfully: models/Voting.model
2024-12-07 18:13:56,820 - Training for Voting completed.

```

Testing with --method all option ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/train-valid.tagged.bone --method all --evaluate | tee testing.log
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.

real    5m46.305s
user    5m38.024s
sys     0m31.756s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

testing time ကတော့ method ၇မျိုးစလုံးလုပ်တာ၊ ၅မိနစ်ကြာတာမို့ လက်တွေ့ သုံးလို့ ရလိမ့်မယ်။  

```
2024-12-07 18:35:51,710 - Testing Decision-Tree model...
2024-12-07 18:35:53,126 - Preparing features for Decision-Tree testing...
2024-12-07 18:36:12,791 -               precision    recall  f1-score   support

           B       0.58      0.19      0.29     62900
           E       0.71      0.77      0.74     62591
           N       0.61      0.19      0.29    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.53      0.55   1334843
weighted avg       0.78      0.81      0.77   1334843

2024-12-07 18:36:12,960 - Testing Random-Forest model...
2024-12-07 18:36:14,531 - Preparing features for Random-Forest testing...
2024-12-07 18:36:56,061 -               precision    recall  f1-score   support

           B       0.58      0.19      0.28     62900
           E       0.71      0.77      0.74     62591
           N       0.61      0.19      0.29    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.53      0.55   1334843
weighted avg       0.78      0.81      0.77   1334843

2024-12-07 18:36:56,226 - Testing Logistic-Regression model...
2024-12-07 18:36:57,583 - Preparing features for Logistic-Regression testing...

2024-12-07 18:37:17,323 -               precision    recall  f1-score   support

           B       0.61      0.05      0.10     62900
           E       0.72      0.72      0.72     62591
           N       0.60      0.11      0.19    180095
           O       0.81      0.97      0.89   1029257

    accuracy                           0.80   1334843
   macro avg       0.69      0.47      0.47   1334843
weighted avg       0.77      0.80      0.75   1334843

2024-12-07 18:37:18,881 - Preparing features for CRF testing...
2024-12-07 18:39:32,315 -               precision    recall  f1-score   support

           B       0.90      0.53      0.67     62900
           E       0.90      0.53      0.67     62591
           N       0.85      0.32      0.47    180095
           O       0.85      0.99      0.91   1029257

    accuracy                           0.85   1334843
   macro avg       0.88      0.59      0.68   1334843
weighted avg       0.86      0.85      0.83   1334843

2024-12-07 18:39:36,823 - Testing AdaBoost model...
2024-12-07 18:39:37,872 - Preparing features for AdaBoost testing...
2024-12-07 18:40:06,895 -               precision    recall  f1-score   support

           B       0.55      0.06      0.11     62900
           E       0.72      0.67      0.69     62591
           N       0.61      0.08      0.14    180095
           O       0.81      0.98      0.89   1029257

    accuracy                           0.80   1334843
   macro avg       0.67      0.45      0.46   1334843
weighted avg       0.77      0.80      0.74   1334843

2024-12-07 18:40:06,961 - Testing GradientBoosting model...
2024-12-07 18:40:08,051 - Preparing features for GradientBoosting testing...
2024-12-07 18:40:45,186 -               precision    recall  f1-score   support

           B       0.56      0.16      0.26     62900
           E       0.71      0.76      0.74     62591
           N       0.63      0.17      0.26    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.51      0.54   1334843
weighted avg       0.78      0.81      0.77   1334843

2024-12-07 18:40:45,290 - Testing Voting model...
2024-12-07 18:40:46,720 - Preparing features for Voting testing...
2024-12-07 18:41:36,684 -               precision    recall  f1-score   support

           B       0.58      0.19      0.28     62900
           E       0.71      0.77      0.74     62591
           N       0.61      0.19      0.29    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.53      0.55   1334843
weighted avg       0.78      0.81      0.77   1334843
```

## Preparing a Shell Script  

လက်တွေ့ experiment လုပ်ဖို့က shell script ရေးထားမှ ပိုအဆင်ပြေတာမို့လို့ bash shell script ကိုလည်း ပြင်ဆင်ခဲ့တယ်။  

```bash
#!/bin/bash

# Define paths for input and output
TRAIN_FILE="./data/syl/bone/train-valid.tagged.bone"
TEST_FILE="./data/syl/bone/test.tagged.bone"
FT_MODEL="./models/fasttext-features.bin"
MODELS_DIR="./models"

# List of methods
METHODS=("Decision-Tree" "Random-Forest" "Logistic-Regression" "CRF" "AdaBoost" "GradientBoosting" "Voting")

# Loop through each method and run training and testing
for METHOD in "${METHODS[@]}"; do
    echo "Starting training and testing for method: $METHOD"

    # Define model file name based on the method
    MODEL_FILE="${MODELS_DIR}/${METHOD}.model"

    # Train
    echo "Training for method: $METHOD"
    time python ./fasttext-ml.py --train "$TRAIN_FILE" --ft-model "$FT_MODEL" --model "$MODEL_FILE" --method "$METHOD"

    # Test
    echo "Testing for method: $METHOD"
    time python ./fasttext-ml.py --test "$TEST_FILE" --ft-model "$FT_MODEL" --model "$MODEL_FILE" --method "$METHOD" --evaluate

    echo "Completed training and testing for method: $METHOD"
    echo "---------------------------------------------"
done

echo "All training and testing completed."

```

ရှေ့မှာလည်း ML experiment တွေက ငါတို့ အများကြီး လုပ်ခဲ့ကြတယ်။ သို့သော် tool က လိုနေတာမို့ ထပ် experiment  လုပ်ဖြစ်ခဲ့တယ်။   
ဒီ experiments အရ sentence segmentation အတွက် ML method တွေအကြားမှာ CRF က strong အဖြစ်ဆုံးပဲ။ Accuracy 0.85 ရတယ်။  

