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

## Updating Python Code

--evaluate option မထည့်ပဲ run တဲ့အခါမှာ test output ကို ထုတ်ပေးပေမဲ့ ဖိုင်အနေနဲ့ output ထုတ်ချင်တယ်။ ပြီးတော့ column format ဖြစ်နေတာကို line by line format အဖြစ် ပြောင်းချင်တယ်။  

```python
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
        # Save results to a text file instead of printing to stdout
        output_file = f"{test_file}.results.txt"
        with open(output_file, "w", encoding="utf-8") as f:
            for word, label in zip(sentences, predictions):
                f.write(f"{word}/{label}\n")
        logger.info(f"Test results saved to {output_file}")

```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./models/CRF.model --method CRF
2024-12-07 23:10:44,067 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-07 23:10:44,864 - Preparing features for CRF testing...
2024-12-07 23:10:58,805 - Test results saved to ./data/syl/bone/test.tagged.bone.results.txt

real    0m16.281s
user    0m16.522s
sys     0m6.691s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ll -h ./data/syl/bone/test.
tagged.bone.results.txt
-rw-rw-r-- 1 ye ye 2.0M Dec  7 23:10 ./data/syl/bone/test.tagged.bone.results.txt
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./data/syl/bone/test.tag
ged.bone.results.txt
 143773  143788 2001809 ./data/syl/bone/test.tagged.bone.results.txt
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

compare with input test data filesize:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./data/syl/bone/test.tagged.bone
   5512  143788 1714263 ./data/syl/bone/test.tagged.bone
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

ထွက်လာတဲ့ test output file ကို ဝင်လေ့လာ..  

```
$ head ./data/syl/bone/test.tagged.bone.results.txt
ရင်/B/O
ဘတ်/O/O
အောင့်/O/O
လာ/O/O
ရင်/O/O
သ/N/O
တိ/N/O
ထား/N/O
ပါ/E/O
ဘယ်/B/O
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ ဖြစ်နေသေး  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./models/CRF.model --method CRF
2024-12-07 23:25:23,124 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-07 23:25:23,917 - Preparing features for CRF testing...
2024-12-07 23:30:21,420 - Test results saved to ./data/syl/bone/test.tagged.bone.results.txt

real    5m4.544s
user    4m57.805s
sys     0m13.659s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Check the test output file:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./data/syl/bone/test.tagged.bone.results.txt
ရင်/B/O ဘတ်/O/O အောင့်/O/O လာ/O/O ရင်/O/O သ/N/O တိ/N/O ထား/N/O ပါ/E/O
ဘယ်/B/N လောက်/O/E နောက်/N/B ကျ/N/O သ/N/O လဲ/E/O
ကြို/B/O ပို့/O/O ဘတ်စ်/O/O ကား/O/O က/O/O အ/O/O ဆင်/O/O အ/N/O ပြေ/N/O ဆုံး/N/O ပဲ/E/O
အဲ/B/O ဒီ/O/O အ/O/O ဖွဲ့/O/O ရဲ့/O/O ဥက္ကဋ္ဌ/O/O ဖြစ်/O/O တဲ့/O/O ယို/O/O ကို/O/O ယာ/O/O မာ့/O/O အာ/O/O ကိ/O/O ဟီ/O/O တို/O/O YokoyamaAkihito/O/O က/O/O တ/O/O ခြား/O/O နိုင်/O/O ငံ/O/O တွေ/O/O မှာ/O/O ဖြစ်/O/O ပွား/O/O တဲ့/O/O လူ/O/O နာ/O/O တွေ/O/O ရဲ့/O/O အ/O/O ဆုတ်/O/O လုပ်/O/O ဆောင်/O/O ပုံ/O/O တွေ/O/O က/O/O ဗိုင်း/O/O ရပ်စ်/O/O ကူး/O/O စက်/O/O ခံ/O/O ရ/O/O ပြီး/O/O ကု/O/O သ/O/O လိုက်/O/O လို့/O/O ရော/O/O ဂါ/O/O ပိုး/O/O မ/O/O ရှိ/O/O တော့/O/O ဘူး/O/O လို့/O/O စစ်/O/O ဆေး/O/O ပြီး/O/O နောက်/O/O မှာ/O/O တောင်/O/O မှ/O/O အ/O/O ဆုတ်/O/O က/O/O အ/O/O ပြည့်/O/O အ/O/O ဝ/O/O ပုံ/O/O မှန်/O/O ပြန်/O/O ဖြစ်/O/O မ/O/O လာ/O/O တဲ့/O/O လူ/O/O နာ/O/O တွေ/O/O အ/O/O များ/O/O အ/O/O ပြား/O/O တွေ့/O/O ရ/O/O တယ်/O/O လို့/N/O ပြော/N/O ပါ/N/O တယ်/E/O
အ/B/N ဆင့်/O/N အေ/O/E ဝင်/O/B ငွေ/O/O ခွန်/O/O ကို/O/O လ/O/O စာ/O/O မှ/N/O ဖြတ်/N/O တောက်/N/O သည်/E/O
လို/B/E ကီ/O/B က/O/O အတ်/O/O ဂါ/O/O ဒါ/O/O လို/O/O ကီ/O/O ရဲ့/O/O မျက်/O/O လုံး/O/O တွေ/O/O ကို/O/O သေ/O/O ချာ/O/O တည့်/O/O တည့်/O/O ကြည့်/O/O ရင်း/O/O ငါ/N/O က/N/O လို/N/O ကီ/E/O
ခင်/B/E ဗျား/O/B ကြိုက်/O/O တဲ့/O/O အ/O/O ရောင်/N/O က/N/O ဘာ/N/O လဲ/E/O
သူ/B/O သီ/O/O ချင်း/O/O ဆို/O/O တတ်/O/O သ/O/O လို/O/O က/O/O လည်း/N/O က/N/O တတ်/N/O သည်/E/O
ထို့/B/O ကြောင့်/O/O ဥ/O/O ပါယ်/O/O ဂို့/O/O ဟု/O/O ခေါ်/O/O ကာ/O/O ကာ/O/O လ/O/O ကြာ/O/O သော်/O/O ဥ/O/O ပါယ်/O/O ဂို့/O/O မှ/O/O ပ/O/O ဂိုး/O/O ဟု/O/O ပြောင်း/O/O လဲ/O/O ခေါ်/N/O လာ/N/O ကြ/N/O သည်/E/O
ဒီ/B/E နေ့/O/B ခင်/O/O ဗျား/O/O ဘယ်/O/O လို/O/O ဖြစ်/N/O နေ/N/N တာ/N/E လဲ/E/B
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Debugging ...  

```
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-07 23:58:01,183 - Preparing features for Decision-Tree testing...
Sentence: ['ရင်/B', 'ဘတ်/O', 'အောင့်/O', 'လာ/O', 'ရင်/O', 'သ/N', 'တိ/N', 'ထား/N', 'ပါ/E']
Tags: ['O' 'B' 'O' 'O' 'B' 'O' 'O' 'O' 'O']
Sentence: ['ဘယ်/B', 'လောက်/O', 'နောက်/N', 'ကျ/N', 'သ/N', 'လဲ/E']
Tags: ['E' 'O' 'O' 'O' 'O' 'O']
```

## Debugged on File Loading, Feature Extractions

code ကို အစအဆုံး ပြန်ဖတ်ကြည့်ပြီး ကြားထဲမှာ file loading, splitting word, tag, feature extraction အပိုင်းတွေကို အကုန် ပြန်ပြင်ရေးခဲ့ရ။ လက်ရှိ အချိန်ထိ updated လုပ်ထားခဲ့တဲ့ code က အောက်ပါအတိုင်း...  

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


#def load_tagged_data(file_path):
#    """Load tagged corpus and return sentences and labels."""
#    sentences, labels = [], []
#    with open(file_path, "r", encoding="utf-8") as f:
#        for line in f:
#            tokens = line.strip().split()
#            for token in tokens:
#                if "/" in token:
#                    word, label = token.rsplit("/", 1)
#                    sentences.append(word)
#                    labels.append(label)
#    return sentences, labels

#def load_tagged_data(file_path):
#    """
#    Load tagged corpus and return sentences and labels for each line.
#    Each sentence is a list of words, and each label is a list of corresponding tags.
#    """
#    sentences, labels = [], []
#    with open(file_path, "r", encoding="utf-8") as f:
#        for line in f:
#            line_sentences = []
#            line_labels = []
#            tokens = line.strip().split()
#            for token in tokens:
#                if "/" in token:
#                    word, label = token.rsplit("/", 1)
#                    line_sentences.append(word)
#                    line_labels.append(label)
#            if line_sentences and line_labels:  # Avoid empty lines
#                sentences.append(line_sentences)
#                labels.append(line_labels)
#    return sentences, labels

def load_tagged_data(filepath):
    """Load tagged data and return sentences and labels."""
    sentences = []
    labels = []

    with open(filepath, 'r', encoding='utf-8') as file:
        for line in file:
            line = line.strip()
            if not line:
                continue

            words, tags = [], []
            for token in line.split():
                word, tag = token.rsplit('/', 1)  # Split word and tag
                words.append(word)
                tags.append(tag)
            
            sentences.append(words)
            labels.append(tags)

    return sentences, labels


def load_raw_data(file_path):
    """Load raw text without tags."""
    sentences = []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            sentences.extend(line.strip().split())
    return sentences


#def prepare_features(sentences, ft_model):
#    """Generate embeddings for sentences using FastText."""
#    return np.array([ft_model.get_word_vector(word) for word in sentences])

#def prepare_features(sentences, ft_model):
#    """Generate embeddings for sentences using FastText."""
    # Flatten the list of sentences (list of lists of words) into a single list of words
#    flat_sentences = [word for sentence in sentences for word in sentence]
#    return np.array([ft_model.get_word_vector(word) for word in flat_sentences])

def prepare_features(sentences, ft_model):
    """Prepare feature vectors for each word in the sentences."""
    features = []
    for sentence in sentences:
        for word in sentence:
            features.append(ft_model.get_word_vector(word))  # Word-level features
    return features

#def prepare_features_for_crf(sentences, ft_model):
#    """Prepare features for CRF."""
#    return [[{'dim_' + str(i): val for i, val in enumerate(ft_model.get_word_vector(word))} for word in sentences]]

def prepare_features_for_crf(sentences, ft_model):
    # Ensure sentences is a list of lists (tokenized sentences)
    return [
        [{'dim_' + str(i): val for i, val in enumerate(ft_model.get_word_vector(word))} for word in sentence]
        for sentence in sentences
    ]

def flatten_labels(labels):
    """Flatten sentence-level labels into a single sequence for word-level alignment."""
    return [label for sentence_labels in labels for label in sentence_labels]

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
        y = labels  # No flattening needed for CRF
    else:
        X = prepare_features(sentences, ft_model)
        y = flatten_labels(labels)  # Flatten labels for other models

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

    # Train the model
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


#def test_model(test_file, ft_model_file, trained_model_file, evaluate, method, logger):
#    """Test the model on the provided test data."""
#    logger.info(f"Testing {method} model...")
#    sentences, labels = load_tagged_data(test_file)
#    if evaluate:
#        sentences, labels = load_tagged_data(test_file)
#    else:
#        sentences = load_raw_data(test_file)
#        labels = None

#    ft_model = fasttext.load_model(ft_model_file)
#    model = joblib.load(trained_model_file)

#    logger.info(f"Preparing features for {method} testing...")
#    if method == "CRF":
#        X = prepare_features_for_crf(sentences, ft_model)
#        predictions = model.predict(X)[0]
#    else:
#        X = prepare_features(sentences, ft_model)
#        predictions = model.predict(X)

#    if evaluate:
#        if method == "CRF":
#            logger.info(flat_classification_report([labels], [predictions]))
#        else:
#            logger.info(classification_report(labels, predictions))
#    else:
#        for word, label in zip(sentences, predictions):
#            logger.info(f"{word}/{label}")

def test_model(test_file, ft_model_file, trained_model_file, evaluate, method, logger):
    """Test the model on the provided test data."""
    logger.info(f"Testing {method} model...")
    
    # Load data
    if evaluate:
        sentences, labels = load_tagged_data(test_file)
    else:
        sentences = load_raw_data(test_file)
        labels = None

    # Load FastText model and trained ML model
    ft_model = fasttext.load_model(ft_model_file)
    model = joblib.load(trained_model_file)

    logger.info(f"Preparing features for {method} testing...")
    if method == "CRF":
        X = prepare_features_for_crf(sentences, ft_model)
        predictions = model.predict(X)  # CRF predictions remain structured (list of sequences)
        
        if evaluate:
            # Ensure both labels and predictions are sequences of sequences
            logger.info("Calculating evaluation metrics for CRF...")
            report = flat_classification_report(labels, predictions)
            logger.info("\n" + report)
        else:
            logger.info("CRF predictions generated.")
    else:
        X = prepare_features(sentences, ft_model)
        predictions = model.predict(X)

        if evaluate:
            logger.info("Calculating evaluation metrics for non-CRF model...")
            flat_labels = flatten_labels(labels)  # Flatten labels for evaluation
            logger.info(classification_report(flat_labels, predictions))
        else:
            logger.info(f"{method} predictions generated.")

    logger.info(f"Testing for {method} completed.")


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

ဝမ်းသာစရာကောင်းတာက CRF ရဲ့ ရလဒ်လည်း 0.91 အထိ တက်လာပြီ။ :)  


```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./Decision-Tree.model --method Decision-Tree --evaluate
2024-12-08 04:51:41,191 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 04:51:42,025 - Preparing features for Decision-Tree testing...
2024-12-08 04:51:43,125 - Calculating evaluation metrics for non-CRF model...
2024-12-08 04:51:44,036 -               precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773

2024-12-08 04:51:44,037 - Testing for Decision-Tree completed.

real    0m3.773s
user    0m6.301s
sys     0m4.413s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./CRF.model --method CRF --evaluate
2024-12-08 04:56:40,427 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 04:56:41,266 - Preparing features for CRF testing...
2024-12-08 04:56:54,681 - Calculating evaluation metrics for CRF...
2024-12-08 04:56:55,658 -
              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.47      0.63     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773

2024-12-08 04:56:55,658 - Testing for CRF completed.

real    0m16.891s
user    0m17.968s
sys     0m5.863s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Coding/Updating for Predicted Result Saving as File

တော်တော်လေး ပြင်လိုက်တယ်။ Resuls for Decision-Tree:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./Decision-Tree.model --method Decision-Tree --evaluate
2024-12-08 05:15:36,047 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 05:15:36,881 - Preparing features for Decision-Tree testing...
2024-12-08 05:15:38,005 - Saving predictions to predictions_Decision-Tree.txt...
2024-12-08 05:15:38,149 - Predictions saved successfully.
              precision    recall  f1-score   support

           B     0.5571    0.1876    0.2807      6861
           E     0.7088    0.7720    0.7390      6829
           N     0.6030    0.1841    0.2820     19728
           O     0.8262    0.9583    0.8874    110355

    accuracy                         0.8065    143773
   macro avg     0.6738    0.5255    0.5473    143773
weighted avg     0.7772    0.8065    0.7683    143773


real    0m3.979s
user    0m6.357s
sys     0m4.563s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$

```

test input, predicted output နှစ်ဖိုင်ရဲ့ လိုင်းအရေအတွက်လည်း တူသွားပြီ။  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc predictions_Decision-Tre
e.txt
   5512  143788 1719775 predictions_Decision-Tree.txt

```

line by line print လုပ်ပေးတယ်။  

```
$ head ./predictions_Decision-Tree.txt
ရင်/O ဘတ်/O အောင့်/O လာ/O ရင်/O သ/O တိ/O ထား/O ပါ/N
ဘယ်/O လောက်/O နောက်/O ကျ/O သ/O လဲ/E
ကြို/O ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/O ပြေ/O ဆုံး/O ပဲ/O
အဲ/B ဒီ/O အ/O ဖွဲ့/O ရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တဲ့/O ယို/O ကို/O ယာ/O မာ့/O အာ/O ကိ/O ဟီ/O တို/O YokoyamaAkihito/O က/O တ/O ခြား/O နိုင်/O ငံ/O တွေ/O မှာ/O ဖြစ်/O ပွား/O တဲ့/O လူ/O နာ/O တွေ/O ရဲ့/O အ/O ဆုတ်/O လုပ်/O ဆောင်/O ပုံ/O တွေ/O က/O ဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O ခံ/O ရ/O ပြီး/O ကု/O သ/O လိုက်/N လို့/O ရော/O ဂါ/O ပိုး/O မ/O ရှိ/O တော့/O ဘူး/E လို့/O စစ်/O ဆေး/O ပြီး/O နောက်/O မှာ/O တောင်/O မှ/O အ/O ဆုတ်/O က/O အ/O ပြည့်/O အ/O ဝ/O ပုံ/O မှန်/O ပြန်/O ဖြစ်/O မ/O လာ/O တဲ့/O လူ/O နာ/O တွေ/O အ/O များ/O အ/O ပြား/O တွေ့/O ရ/O တယ်/E လို့/O ပြော/N ပါ/N တယ်/E
အ/O ဆင့်/O အေ/O ဝင်/O ငွေ/O ခွန်/O ကို/O လ/O စာ/O မှ/O ဖြတ်/O တောက်/O သည်/E
လို/O ကီ/O က/O အတ်/O ဂါ/O ဒါ/B လို/O ကီ/O ရဲ့/O မျက်/O လုံး/O တွေ/O ကို/O သေ/O ချာ/O တည့်/O တည့်/O ကြည့်/O ရင်း/O ငါ/O က/O လို/O ကီ/O
ခင်/B ဗျား/O ကြိုက်/N တဲ့/O အ/O ရောင်/O က/O ဘာ/O လဲ/E
သူ/O သီ/O ချင်း/O ဆို/O တတ်/O သ/O လို/O က/O လည်း/O က/O တတ်/O သည်/E
ထို့/B ကြောင့်/O ဥ/O ပါယ်/O ဂို့/O ဟု/O ခေါ်/O ကာ/O ကာ/O လ/O ကြာ/O သော်/O ဥ/O ပါယ်/O ဂို့/O မှ/O ပ/O ဂိုး/O ဟု/O ပြောင်း/O လဲ/E ခေါ်/O လာ/O ကြ/N သည်/E
ဒီ/O နေ့/O ခင်/B ဗျား/O ဘယ်/O လို/O ဖြစ်/O နေ/O တာ/O လဲ/E
```

တခြား method တွေ အားလုံးအတွက် မစမ်းကြည့်ရသေးပေမဲ့ CRF အတွက်တော့ စမ်းကြည့်မယ်။  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./CRF.model --method CRF --evaluate
2024-12-08 05:19:24,734 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 05:19:25,570 - Preparing features for CRF testing...
2024-12-08 05:19:39,065 - Saving predictions to predictions_CRF.txt...
2024-12-08 05:19:39,094 - Predictions saved successfully.
              precision    recall  f1-score   support

           B     0.9884    0.8575    0.9183      6861
           E     0.9874    0.8581    0.9182      6829
           N     0.9371    0.4692    0.6253     19728
           O     0.8991    0.9941    0.9442    110355

    accuracy                         0.9091    143773
   macro avg     0.9530    0.7947    0.8515    143773
weighted avg     0.9128    0.9091    0.8980    143773


real    0m17.127s
user    0m18.108s
sys     0m5.959s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

predicted file ကို စစ်ကြည့်ခဲ့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc predictions_CRF.txt
  5512 143773 784663 predictions_CRF.txt
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

သို့သော် လက်ရှိ CRF output က အောက်ပါအတိုင်း list နဲ့ ထုတ်တယ်။ အဆင်မပြေသေးဘူး ...   

```
ရင်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဘတ်/['B', 'O', 'O', 'O', 'N', 'E'] အောင့်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] လာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ရင်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] သ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တိ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ထား/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပါ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] 
ဘယ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လောက်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] နောက်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ကျ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'N', 'E'] သ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] လဲ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] 
ကြို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ပို့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဘတ်စ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကား/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဆင်/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပြေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဆုံး/['B', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပဲ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] 
အဲ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဒီ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဖွဲ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ရဲ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဥက္ကဋ္ဌ/['B', 'O', 'O', 'O', 'O', 'N', 'E'] ဖြစ်/['B', 'N', 'N', 'N', 'E'] တဲ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ယို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ကို/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ယာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] မာ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] အာ/['B', 'N', 'N', 'N', 'N', 'E'] ကိ/['B', 'N', 'N', 'N', 'N', 'E'] ဟီ/['B', 'O', 'O', 'O', 'N', 'E'] တို/['B', 'O', 'O', 'N', 'E'] YokoyamaAkihito/['B', 'O', 'O', 'O', 'O', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'N', 'E'] တ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ခြား/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] နိုင်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ငံ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] တွေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] မှာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဖြစ်/['B', 'O', 'O', 'N', 'N', 'E'] ပွား/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တဲ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] လူ/['B', 'O', 'O', 'O', 'O', 'N', 'E'] နာ/['B', 'O', 'O', 'O', 'O', 'N', 'E'] တွေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ရဲ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဆုတ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လုပ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဆောင်/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပုံ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] တွေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'N', 'E'] ဗိုင်း/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ရပ်စ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကူး/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] စက်/['B', 'O', 'O', 'N', 'E'] ခံ/['B', 'O', 'O', 'O', 'O', 'N', 'E'] ရ/['B', 'N', 'N', 'N', 'E'] ပြီး/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကု/['B', 'O', 'O', 'O', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] သ/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] လိုက်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လို့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'N', 'E'] ရော/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ဂါ/['B', 'N', 'N', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'N', 'N', 'N', 'E'] ပိုး/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] မ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O'] ရှိ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] တော့/['B', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဘူး/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လို့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] စစ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဆေး/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပြီး/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] နောက်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] မှာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တောင်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] မှ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဆုတ်/['B', 'N', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ပြည့်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'N', 'E'] ဝ/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပုံ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] မှန်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ပြန်/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဖြစ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] မ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တဲ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လူ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] နာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] တွေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] များ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ပြား/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တွေ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ရ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တယ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လို့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပြော/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ပါ/['B', 'O', 'O', 'O', 'N', 'E'] တယ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] 
အ/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဆင့်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] အေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဝင်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ငွေ/['B', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'N', 'N', 'N', 'E'] ခွန်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ကို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] လ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] စာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] မှ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဖြတ်/['B', 'N', 'N', 'N', 'E'] တောက်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] သည်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] 
လို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကီ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] အတ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ဂါ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဒါ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] လို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ကီ/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ရဲ့/['B', 'O', 'O', 'N', 'N', 'E'] မျက်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လုံး/['B', 'N', 'E'] တွေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ကို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] သေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E', 'B', 'E'] ချာ/['B', 'O', 'O', 'O', 'N', 'N', 'E'] တည့်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တည့်/['B', 'O', 'O', 'O', 'O', 'N', 'E'] ကြည့်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ရင်း/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ငါ/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ကီ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] 
ခင်/['B', 'N', 'N', 'N', 'E'] ဗျား/['B', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ကြိုက်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တဲ့/['B', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] အ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ရောင်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဘာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] လဲ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] 
သူ/['B', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] သီ/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ချင်း/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဆို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] တတ်/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] သ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] လို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လည်း/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] က/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] တတ်/['B', 'N', 'N', 'E', 'B', 'N', 'E', 'B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] သည်/['B', 'N', 'N', 'E'] 
ထို့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကြောင့်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'N', 'E'] ဥ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပါယ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဂို့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဟု/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ခေါ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ကြာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] သော်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဥ/['B', 'N', 'E'] ပါယ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဂို့/['B', 'O', 'O', 'O', 'O', 'N', 'E'] မှ/['B', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဂိုး/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဟု/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ပြောင်း/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] လဲ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] ခေါ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] လာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ကြ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] သည်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] 
ဒီ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] နေ့/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ခင်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဗျား/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] ဘယ်/['B', 'O', 'O', 'N', 'E'] လို/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] ဖြစ်/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] နေ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'E'] တာ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'E'] လဲ/['B', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'O', 'N', 'N', 'N', 'E'] 

```

## Updating the Code

```python
def test_model(test_file, ft_model_file, trained_model_file, evaluate, method, output_file, logger):
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
        predictions = model.predict(X)
    else:
        X = prepare_features(sentences, ft_model)
        predictions = model.predict(X)

    # Ensure predictions are human-readable
    logger.info(f"Saving predictions to {output_file}...")
    with open(output_file, 'w', encoding='utf-8') as f:
        for sentence, sentence_predictions in zip(sentences, predictions):
            if method == "CRF":
                # CRF predictions are already sentence-aligned
                formatted_sentence = " ".join(f"{word}/{tag}" for word, tag in zip(sentence, sentence_predictions))
            else:
                # Flattened predictions, need to realign to sentences
                formatted_sentence = " ".join(f"{word}/{tag}" for word, tag in zip(sentence, sentence_predictions[:len(sentence)]))
            f.write(f"{formatted_sentence}\n")

    logger.info(f"Predictions saved successfully.")

    # Calculate and display metrics if labels are provided
    if evaluate and labels:
        flattened_true = flatten_labels(labels)
        flattened_predictions = (
            predictions if method != "CRF" else flatten_labels(predictions)
        )

        if method == "CRF":
            report = flat_classification_report(labels, predictions)
        else:
            report = classification_report(flattened_true, flattened_predictions)

        logger.info(f"Evaluation Results:\n{report}")
        print(report)

```

Run testing for DT and CRF again and check predicted output files:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./Decision-Tree.model --method Decision-Tree --evaluate
2024-12-08 05:35:44,424 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 05:35:45,258 - Preparing features for Decision-Tree testing...
2024-12-08 05:35:46,389 - Saving predictions to predictions_Decision-Tree.txt...
2024-12-08 05:35:46,400 - Predictions saved successfully.
2024-12-08 05:35:47,318 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773

              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m3.822s
user    0m6.355s
sys     0m4.407s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./data/syl/bone/test.tagged.bone
   5512  143788 1714263 ./data/syl/bone/test.tagged.bone
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./predictions_Decision-Tree.txt
 5512  5512 64240 ./predictions_Decision-Tree.txt
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./predictions_Decision-Tree.txt
ရင်/O
ဘယ်/O
ကြို/O
အဲ/O
အ/O
လို/O
ခင်/O
သူ/O
ထို့/N
ဒီ/O
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Testing for CRF:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./CRF.model --method CRF --evaluate
2024-12-08 05:38:25,665 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 05:38:26,501 - Preparing features for CRF testing...
2024-12-08 05:38:39,674 - Saving predictions to predictions_CRF.txt...
2024-12-08 05:38:39,726 - Predictions saved successfully.
2024-12-08 05:38:40,711 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.47      0.63     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773

              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.47      0.63     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773


real    0m16.716s
user    0m17.699s
sys     0m5.957s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc predictions_CRF.txt
   5512  143788 1714263 predictions_CRF.txt
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head predictions_CRF.txt
ရင်/B ဘတ်/O အောင့်/O လာ/O ရင်/O သ/O တိ/O ထား/N ပါ/E
ဘယ်/B လောက်/O နောက်/O ကျ/O သ/N လဲ/E
ကြို/B ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/O ပြေ/N ဆုံး/N ပဲ/E
အဲ/B ဒီ/O အ/O ဖွဲ့/O ရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တဲ့/O ယို/O ကို/O ယာ/O မာ့/O အာ/O ကိ/O ဟီ/O တို/O YokoyamaAkihito/O က/O တ/O ခြား/O နိုင်/O ငံ/O တွေ/O မှာ/O ဖြစ်/O ပွား/O တဲ့/O လူ/O နာ/O တွေ/O ရဲ့/O အ/O ဆုတ်/O လုပ်/O ဆောင်/O ပုံ/O တွေ/O က/O ဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O ခံ/O ရ/O ပြီး/O ကု/O သ/O လိုက်/O လို့/O ရော/O ဂါ/O ပိုး/O မ/O ရှိ/O တော့/O ဘူး/O လို့/O စစ်/O ဆေး/O ပြီး/O နောက်/O မှာ/O တောင်/O မှ/O အ/O ဆုတ်/O က/O အ/O ပြည့်/O အ/O ဝ/O ပုံ/O မှန်/O ပြန်/O ဖြစ်/O မ/O လာ/O တဲ့/O လူ/O နာ/O တွေ/O အ/O များ/O အ/O ပြား/O တွေ့/O ရ/O တယ်/O လို့/O ပြော/N ပါ/N တယ်/E
အ/B ဆင့်/O အေ/O ဝင်/O ငွေ/O ခွန်/O ကို/O လ/O စာ/O မှ/O ဖြတ်/O တောက်/N သည်/E
လို/B ကီ/O က/O အတ်/O ဂါ/O ဒါ/O လို/O ကီ/O ရဲ့/O မျက်/O လုံး/O တွေ/O ကို/O သေ/O ချာ/O တည့်/O တည့်/O ကြည့်/O ရင်း/O ငါ/O က/O လို/N ကီ/E
ခင်/B ဗျား/O ကြိုက်/O တဲ့/O အ/O ရောင်/O က/O ဘာ/N လဲ/E
သူ/B သီ/O ချင်း/O ဆို/O တတ်/O သ/O လို/O က/O လည်း/O က/O တတ်/N သည်/E
ထို့/B ကြောင့်/O ဥ/O ပါယ်/O ဂို့/O ဟု/O ခေါ်/O ကာ/O ကာ/O လ/O ကြာ/O သော်/O ဥ/O ပါယ်/O ဂို့/O မှ/O ပ/O ဂိုး/O ဟု/O ပြောင်း/O လဲ/O ခေါ်/N လာ/N ကြ/N သည်/E
ဒီ/B နေ့/O ခင်/O ဗျား/O ဘယ်/O လို/O ဖြစ်/O နေ/O တာ/N လဲ/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Debugging the Code  

Version 1.0 တော့ ရလာပြီ။  

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

def load_tagged_data(filepath):
    """Load tagged data and return sentences and labels."""
    sentences = []
    labels = []

    with open(filepath, 'r', encoding='utf-8') as file:
        for line in file:
            line = line.strip()
            if not line:
                continue

            words, tags = [], []
            for token in line.split():
                word, tag = token.rsplit('/', 1)  # Split word and tag
                words.append(word)
                tags.append(tag)
            
            sentences.append(words)
            labels.append(tags)

    return sentences, labels


def load_raw_data(file_path):
    """Load raw text without tags."""
    sentences = []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            sentences.extend(line.strip().split())
    return sentences

def prepare_features(sentences, ft_model):
    """Prepare feature vectors for each word in the sentences."""
    features = []
    for sentence in sentences:
        for word in sentence:
            features.append(ft_model.get_word_vector(word))  # Word-level features
    return features

def prepare_features_for_crf(sentences, ft_model):
    """Prepare features for CRF."""
    return [
        [{'dim_' + str(i): val for i, val in enumerate(ft_model.get_word_vector(word))} for word in sentence]
        for sentence in sentences
    ]

def flatten_labels(labels):
    """Flatten sentence-level labels into a single sequence for word-level alignment."""
    return [label for sentence_labels in labels for label in sentence_labels]

def train_model(train_file, ft_model_file, output_model_file, method, logger):
    """Train the model based on the selected method."""
    logger.info(f"Loading training data for {method}...")
    sentences, labels = load_tagged_data(train_file)

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
        y = labels
    else:
        X = prepare_features(sentences, ft_model)
        y = flatten_labels(labels)

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
    logger.info(f"Training for {method} completed.")

def test_model(test_file, ft_model_file, trained_model_file, evaluate, method, output_file, logger):
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
        predictions = model.predict(X)
    else:
        X = prepare_features(sentences, ft_model)
        predictions = model.predict(X)

        # Realign flat predictions to sentence structure
        sentence_lengths = [len(sentence) for sentence in sentences]
        predictions = [predictions[start:start + length] for start, length in zip(np.cumsum([0] + sentence_lengths[:-1]), sentence_lengths)]

    # Ensure predictions are human-readable
    logger.info(f"Saving predictions to {output_file}...")
    with open(output_file, 'w', encoding='utf-8') as f:
        for sentence, sentence_predictions in zip(sentences, predictions):
            formatted_sentence = " ".join(f"{word}/{tag}" for word, tag in zip(sentence, sentence_predictions))
            f.write(f"{formatted_sentence}\n")

    logger.info(f"Predictions saved successfully.")

    # Calculate and display metrics if labels are provided
    if evaluate and labels:
        flattened_true = flatten_labels(labels)
        flattened_predictions = flatten_labels(predictions)  # Ensure flattening here as well

        # Ensure that flattened_true and flattened_predictions have the same length
        if len(flattened_true) != len(flattened_predictions):
            logger.error(f"Length mismatch: true labels ({len(flattened_true)}) vs predictions ({len(flattened_predictions)})")
            raise ValueError(f"Length mismatch: true labels and predictions have different lengths!")

        if method == "CRF":
            report = flat_classification_report(labels, predictions)
        else:
            report = classification_report(flattened_true, flattened_predictions)

        logger.info(f"Evaluation Results:\n{report}")
        print(report)


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
    parser.add_argument("--output", help="Specify the output file for predictions.")

    args = parser.parse_args()

    logging.basicConfig(filename="all-training-testing.log" if args.method == "all" else None,
                        level=logging.INFO,
                        format="%(asctime)s - %(message)s")
    logger = logging.getLogger()

    if args.method == "all":
        methods = ["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting"]
    else:
        methods = [args.method]

    if args.train:
        for method in methods:
            model_file = f"models/{method}.model"
            train_model(args.train, args.ft_model, model_file, method, logger)
    elif args.test:
        for method in methods:
            model_file = f"models/{method}.model"
            default_output_file = f"predictions_{method}.txt"
            output_file = args.output or default_output_file
            test_model(args.test, args.ft_model, model_file, args.evaluate, method, output_file, logger)
    else:
        parser.print_help()


if __name__ == "__main__":
    main()


```

Testing Results with Version 1.0 Code:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./Decision-Tree.model --method Decision-Tree --evaluate
2024-12-08 05:59:55,706 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 05:59:56,541 - Preparing features for Decision-Tree testing...
2024-12-08 05:59:57,692 - Saving predictions to predictions_Decision-Tree.txt...
2024-12-08 05:59:57,799 - Predictions saved successfully.
2024-12-08 05:59:58,833 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773

              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m4.064s
user    0m6.595s
sys     0m4.407s
```

Check predicted file of Decision-Tree:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head predictions_Decision-Tree.txt
ရင်/O ဘတ်/O အောင့်/O လာ/O ရင်/O သ/O တိ/O ထား/O ပါ/N
ဘယ်/O လောက်/O နောက်/O ကျ/O သ/O လဲ/E
ကြို/O ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/O ပြေ/O ဆုံး/O ပဲ/O
အဲ/B ဒီ/O အ/O ဖွဲ့/O ရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တဲ့/O ယို/O ကို/O ယာ/O မာ့/O အာ/O ကိ/O ဟီ/O တို/O YokoyamaAkihito/O က/O တ/O ခြား/O နိုင်/O ငံ/O တွေ/O မှာ/O ဖြစ်/O ပွား/O တဲ့/O လူ/O နာ/O တွေ/O ရဲ့/O အ/O ဆုတ်/O လုပ်/O ဆောင်/O ပုံ/O တွေ/O က/O ဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O ခံ/O ရ/O ပြီး/O ကု/O သ/O လိုက်/N လို့/O ရော/O ဂါ/O ပိုး/O မ/O ရှိ/O တော့/O ဘူး/E လို့/O စစ်/O ဆေး/O ပြီး/O နောက်/O မှာ/O တောင်/O မှ/O အ/O ဆုတ်/O က/O အ/O ပြည့်/O အ/O ဝ/O ပုံ/O မှန်/O ပြန်/O ဖြစ်/O မ/O လာ/O တဲ့/O လူ/O နာ/O တွေ/O အ/O များ/O အ/O ပြား/O တွေ့/O ရ/O တယ်/E လို့/O ပြော/N ပါ/N တယ်/E
အ/O ဆင့်/O အေ/O ဝင်/O ငွေ/O ခွန်/O ကို/O လ/O စာ/O မှ/O ဖြတ်/O တောက်/O သည်/E
လို/O ကီ/O က/O အတ်/O ဂါ/O ဒါ/B လို/O ကီ/O ရဲ့/O မျက်/O လုံး/O တွေ/O ကို/O သေ/O ချာ/O တည့်/O တည့်/O ကြည့်/O ရင်း/O ငါ/O က/O လို/O ကီ/O
ခင်/B ဗျား/O ကြိုက်/N တဲ့/O အ/O ရောင်/O က/O ဘာ/O လဲ/E
သူ/O သီ/O ချင်း/O ဆို/O တတ်/O သ/O လို/O က/O လည်း/O က/O တတ်/O သည်/E
ထို့/B ကြောင့်/O ဥ/O ပါယ်/O ဂို့/O ဟု/O ခေါ်/O ကာ/O ကာ/O လ/O ကြာ/O သော်/O ဥ/O ပါယ်/O ဂို့/O မှ/O ပ/O ဂိုး/O ဟု/O ပြောင်း/O လဲ/E ခေါ်/O လာ/O ကြ/N သည်/E
ဒီ/O နေ့/O ခင်/B ဗျား/O ဘယ်/O လို/O ဖြစ်/O နေ/O တာ/O လဲ/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Test Run for CRF (အမွှေစိန်):  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./CRF.model --method CRF --evaluate
2024-12-08 06:01:41,183 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 06:01:42,019 - Preparing features for CRF testing...
2024-12-08 06:01:55,137 - Saving predictions to predictions_CRF.txt...
2024-12-08 06:01:55,189 - Predictions saved successfully.
2024-12-08 06:01:56,175 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.47      0.63     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773

              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.47      0.63     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773


real    0m16.658s
user    0m17.855s
sys     0m5.742s
```

CRF method ရဲ့ရလဒ်ဖိုင်ကိုလည်း စစ်ကြည့်ခဲ့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head predictions_CRF.txt
ရင်/B ဘတ်/O အောင့်/O လာ/O ရင်/O သ/O တိ/O ထား/N ပါ/E
ဘယ်/B လောက်/O နောက်/O ကျ/O သ/N လဲ/E
ကြို/B ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/O ပြေ/N ဆုံး/N ပဲ/E
အဲ/B ဒီ/O အ/O ဖွဲ့/O ရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တဲ့/O ယို/O ကို/O ယာ/O မာ့/O အာ/O ကိ/O ဟီ/O တို/O YokoyamaAkihito/O က/O တ/O ခြား/O နိုင်/O ငံ/O တွေ/O မှာ/O ဖြစ်/O ပွား/O တဲ့/O လူ/O နာ/O တွေ/O ရဲ့/O အ/O ဆုတ်/O လုပ်/O ဆောင်/O ပုံ/O တွေ/O က/O ဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O ခံ/O ရ/O ပြီး/O ကု/O သ/O လိုက်/O လို့/O ရော/O ဂါ/O ပိုး/O မ/O ရှိ/O တော့/O ဘူး/O လို့/O စစ်/O ဆေး/O ပြီး/O နောက်/O မှာ/O တောင်/O မှ/O အ/O ဆုတ်/O က/O အ/O ပြည့်/O အ/O ဝ/O ပုံ/O မှန်/O ပြန်/O ဖြစ်/O မ/O လာ/O တဲ့/O လူ/O နာ/O တွေ/O အ/O များ/O အ/O ပြား/O တွေ့/O ရ/O တယ်/O လို့/O ပြော/N ပါ/N တယ်/E
အ/B ဆင့်/O အေ/O ဝင်/O ငွေ/O ခွန်/O ကို/O လ/O စာ/O မှ/O ဖြတ်/O တောက်/N သည်/E
လို/B ကီ/O က/O အတ်/O ဂါ/O ဒါ/O လို/O ကီ/O ရဲ့/O မျက်/O လုံး/O တွေ/O ကို/O သေ/O ချာ/O တည့်/O တည့်/O ကြည့်/O ရင်း/O ငါ/O က/O လို/N ကီ/E
ခင်/B ဗျား/O ကြိုက်/O တဲ့/O အ/O ရောင်/O က/O ဘာ/N လဲ/E
သူ/B သီ/O ချင်း/O ဆို/O တတ်/O သ/O လို/O က/O လည်း/O က/O တတ်/N သည်/E
ထို့/B ကြောင့်/O ဥ/O ပါယ်/O ဂို့/O ဟု/O ခေါ်/O ကာ/O ကာ/O လ/O ကြာ/O သော်/O ဥ/O ပါယ်/O ဂို့/O မှ/O ပ/O ဂိုး/O ဟု/O ပြောင်း/O လဲ/O ခေါ်/N လာ/N ကြ/N သည်/E
ဒီ/B နေ့/O ခင်/O ဗျား/O ဘယ်/O လို/O ဖြစ်/O နေ/O တာ/N လဲ/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Adding One More Facility

Online testing or Testing with Raw data အတွက် code ကို update လုပ်ခဲ့တယ်။  

အရင်ဆုံး tag မပါတဲ့ test data ဖိုင်ကို ပြင်ဆင်ခဲ့တယ်။  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ perl ./mk-wordtag.pl ./data/syl/bone/test.tagged.bone "\/" w > ./data/syl/bone/test.tagged.bone.word
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./data/syl/bone/test.tagged.bone.word
ရင် ဘတ် အောင့် လာ ရင် သ တိ ထား ပါ
ဘယ် လောက် နောက် ကျ သ လဲ
ကြို ပို့ ဘတ်စ် ကား က အ ဆင် အ ပြေ ဆုံး ပဲ
အဲ ဒီ အ ဖွဲ့ ရဲ့ ဥက္ကဋ္ဌ ဖြစ် တဲ့ ယို ကို ယာ မာ့ အာ ကိ ဟီ တို YokoyamaAkihito က တ ခြား နိုင် ငံ တွေ မှာ ဖြစ် ပွား တဲ့ လူ နာ တွေ ရဲ့ အ ဆုတ် လုပ် ဆောင် ပုံ တွေ က ဗိုင်း ရပ်စ် ကူး စက် ခံ ရ ပြီး ကု သ လိုက် လို့ ရော ဂါ ပိုး မ ရှိ တော့ ဘူး လို့ စစ် ဆေး ပြီး နောက် မှာ တောင် မှ အ ဆုတ် က အ ပြည့် အ ဝ ပုံ မှန် ပြန် ဖြစ် မ လာ တဲ့ လူ နာ တွေ အ များ အ ပြား တွေ့ ရ တယ် လို့ ပြော ပါ တယ်
အ ဆင့် အေ ဝင် ငွေ ခွန် ကို လ စာ မှ ဖြတ် တောက် သည်
လို ကီ က အတ် ဂါ ဒါ လို ကီ ရဲ့ မျက် လုံး တွေ ကို သေ ချာ တည့် တည့် ကြည့် ရင်း ငါ က လို ကီ
ခင် ဗျား ကြိုက် တဲ့ အ ရောင် က ဘာ လဲ
သူ သီ ချင်း ဆို တတ် သ လို က လည်း က တတ် သည်
ထို့ ကြောင့် ဥ ပါယ် ဂို့ ဟု ခေါ် ကာ ကာ လ ကြာ သော် ဥ ပါယ် ဂို့ မှ ပ ဂိုး ဟု ပြောင်း လဲ ခေါ် လာ ကြ သည်
ဒီ နေ့ ခင် ဗျား ဘယ် လို ဖြစ် နေ တာ လဲ
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

code ကို update လုပ်ခဲ့...  

```python
"""
This code is designed for well-studied machine learning-based sequence-to-sequence tagging tasks. It can be used for various NLP tasks such as POS tagging, NER tagging, word segmentation, and sentence breaking.

Written by Ye Kyaw Thu, Lab Leader, Language Understanding Lab., Myanmar.
Last updated: 8 Dec 2024

How to run:

For training:
  time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --ft-model ./fasttext_model.bin --model ./Decision-Tree.model --method Decision-Tree

For testing/evaluation with tagged data:
  time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./Decision-Tree.model --method Decision-Tree --evaluate

For testing with raw data:
  time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./Decision-Tree.model --method Decision-Tree --raw_test --output prediction_DT.txt

For training with all 7 machine learning methods:
  time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --ft-model ./fasttext_model.bin --method all

For testing with all methods:
  time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --method all --evaluate
"""

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

def load_tagged_data(filepath):
    """Load tagged data and return sentences and labels."""
    sentences = []
    labels = []

    with open(filepath, 'r', encoding='utf-8') as file:
        for line in file:
            line = line.strip()
            if not line:
                continue

            words, tags = [], []
            for token in line.split():
                word, tag = token.rsplit('/', 1)  # Split word and tag
                words.append(word)
                tags.append(tag)
            
            sentences.append(words)
            labels.append(tags)

    return sentences, labels


def load_raw_data(file_path):
    """Load raw text without tags."""
    sentences = []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            sentences.append(line.strip().split())  # Split words by space
    return sentences

def prepare_features(sentences, ft_model):
    """Prepare feature vectors for each word in the sentences."""
    features = []
    for sentence in sentences:
        for word in sentence:
            features.append(ft_model.get_word_vector(word))  # Word-level features
    return features

def prepare_features_for_crf(sentences, ft_model):
    """Prepare features for CRF."""
    return [
        [{'dim_' + str(i): val for i, val in enumerate(ft_model.get_word_vector(word))} for word in sentence]
        for sentence in sentences
    ]

def flatten_labels(labels):
    """Flatten sentence-level labels into a single sequence for word-level alignment."""
    return [label for sentence_labels in labels for label in sentence_labels]

def train_model(train_file, ft_model_file, output_model_file, method, logger):
    """Train the model based on the selected method."""
    logger.info(f"Loading training data for {method}...")
    sentences, labels = load_tagged_data(train_file)

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
        y = labels
    else:
        X = prepare_features(sentences, ft_model)
        y = flatten_labels(labels)

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
    logger.info(f"Training for {method} completed.")

def test_model(test_file, ft_model_file, trained_model_file, evaluate, raw_test, method, output_file, logger):
    """Test the model on the provided test data."""
    logger.info(f"Testing {method} model...")

    if evaluate:
        sentences, labels = load_tagged_data(test_file)
    elif raw_test:
        sentences = load_raw_data(test_file)
        labels = None
    else:
        sentences, labels = load_raw_data(test_file), None  # Default case when no evaluation is required

    ft_model = fasttext.load_model(ft_model_file)
    model = joblib.load(trained_model_file)

    logger.info(f"Preparing features for {method} testing...")
    if method == "CRF":
        X = prepare_features_for_crf(sentences, ft_model)
        predictions = model.predict(X)
    else:
        X = prepare_features(sentences, ft_model)
        predictions = model.predict(X)

        # Realign flat predictions to sentence structure
        sentence_lengths = [len(sentence) for sentence in sentences]
        predictions = [predictions[start:start + length] for start, length in zip(np.cumsum([0] + sentence_lengths[:-1]), sentence_lengths)]

    # Ensure predictions are human-readable
    logger.info(f"Saving predictions to {output_file}...")
    with open(output_file, 'w', encoding='utf-8') as f:
        for sentence, sentence_predictions in zip(sentences, predictions):
            formatted_sentence = " ".join(f"{word}/{tag}" for word, tag in zip(sentence, sentence_predictions))
            f.write(f"{formatted_sentence}\n")

    logger.info(f"Predictions saved successfully.")

    # Calculate and display metrics if labels are provided
    if evaluate and labels:
        flattened_true = flatten_labels(labels)
        flattened_predictions = flatten_labels(predictions)  # Ensure flattening here as well

        # Ensure that flattened_true and flattened_predictions have the same length
        if len(flattened_true) != len(flattened_predictions):
            logger.error(f"Length mismatch: true labels ({len(flattened_true)}) vs predictions ({len(flattened_predictions)})")
            raise ValueError(f"Length mismatch: true labels and predictions have different lengths!")

        if method == "CRF":
            report = flat_classification_report(labels, predictions)
        else:
            report = classification_report(flattened_true, flattened_predictions)

        logger.info(f"Evaluation Results:\n{report}")
        print(report)


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
    parser.add_argument("--raw_test", action="store_true", help="Test the model with raw input (no tags).")
    parser.add_argument("--output", help="Specify the output file for predictions.")

    args = parser.parse_args()

    logging.basicConfig(filename="all-training-testing.log" if args.method == "all" else None,
                        level=logging.INFO,
                        format="%(asctime)s - %(message)s")
    logger = logging.getLogger()

    if args.method == "all":
        methods = ["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting"]
    else:
        methods = [args.method]

    if args.train:
        for method in methods:
            model_file = f"models/{method}.model"
            train_model(args.train, args.ft_model, model_file, method, logger)
    elif args.test:
        for method in methods:
            model_file = f"models/{method}.model"
            default_output_file = f"predictions_{method}.txt"
            output_file = args.output or default_output_file
            test_model(args.test, args.ft_model, model_file, args.evaluate, args.raw_test, method, output_file, logger)
    else:
        parser.print_help()


if __name__ == "__main__":
    main()

```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone.word --ft-model ./fasttext_model.bin --model ./Decision-Tree.mo
del --method Decision-Tree --raw_test --output prediction-raw-DT.txt
2024-12-08 06:26:14,326 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-08 06:26:15,112 - Preparing features for Decision-Tree testing...
2024-12-08 06:26:16,267 - Saving predictions to prediction-raw-DT.txt...
2024-12-08 06:26:16,369 - Predictions saved successfully.

real    0m2.954s
user    0m5.404s
sys     0m4.491s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Check the predicted output file with raw test data (i.e word only).  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./prediction-raw-DT.txt
   5512  143788 1714263 ./prediction-raw-DT.txt
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./prediction-raw-DT.txt
ရင်/O ဘတ်/O အောင့်/O လာ/O ရင်/O သ/O တိ/O ထား/O ပါ/N
ဘယ်/O လောက်/O နောက်/O ကျ/O သ/O လဲ/E
ကြို/O ပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/O ပြေ/O ဆုံး/O ပဲ/O
အဲ/B ဒီ/O အ/O ဖွဲ့/O ရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တဲ့/O ယို/O ကို/O ယာ/O မာ့/O အာ/O ကိ/O ဟီ/O တို/O YokoyamaAkihito/O က/O တ/O ခြား/O နိုင်/O ငံ/O တွေ/O မှာ/O ဖြစ်/O ပွား/O တဲ့/O လူ/O နာ/O တွေ/O ရဲ့/O အ/O ဆုတ်/O လုပ်/O ဆောင်/O ပုံ/O တွေ/O က/O ဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O ခံ/O ရ/O ပြီး/O ကု/O သ/O လိုက်/N လို့/O ရော/O ဂါ/O ပိုး/O မ/O ရှိ/O တော့/O ဘူး/E လို့/O စစ်/O ဆေး/O ပြီး/O နောက်/O မှာ/O တောင်/O မှ/O အ/O ဆုတ်/O က/O အ/O ပြည့်/O အ/O ဝ/O ပုံ/O မှန်/O ပြန်/O ဖြစ်/O မ/O လာ/O တဲ့/O လူ/O နာ/O တွေ/O အ/O များ/O အ/O ပြား/O တွေ့/O ရ/O တယ်/E လို့/O ပြော/N ပါ/N တယ်/E
အ/O ဆင့်/O အေ/O ဝင်/O ငွေ/O ခွန်/O ကို/O လ/O စာ/O မှ/O ဖြတ်/O တောက်/O သည်/E
လို/O ကီ/O က/O အတ်/O ဂါ/O ဒါ/B လို/O ကီ/O ရဲ့/O မျက်/O လုံး/O တွေ/O ကို/O သေ/O ချာ/O တည့်/O တည့်/O ကြည့်/O ရင်း/O ငါ/O က/O လို/O ကီ/O
ခင်/B ဗျား/O ကြိုက်/N တဲ့/O အ/O ရောင်/O က/O ဘာ/O လဲ/E
သူ/O သီ/O ချင်း/O ဆို/O တတ်/O သ/O လို/O က/O လည်း/O က/O တတ်/O သည်/E
ထို့/B ကြောင့်/O ဥ/O ပါယ်/O ဂို့/O ဟု/O ခေါ်/O ကာ/O ကာ/O လ/O ကြာ/O သော်/O ဥ/O ပါယ်/O ဂို့/O မှ/O ပ/O ဂိုး/O ဟု/O ပြောင်း/O လဲ/E ခေါ်/O လာ/O ကြ/N သည်/E
ဒီ/O နေ့/O ခင်/B ဗျား/O ဘယ်/O လို/O ဖြစ်/O နေ/O တာ/O လဲ/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Training/Testing with --method all

```
time python ./fasttext-ml.py --train ./data/syl/bone/train-valid.tagged.bone --ft-model ./models/fasttext_model.bin --method all
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --method all --evaluate | tee test-all.log
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Checked log file:  

```
2024-12-08 20:21:48,833 - Testing Decision-Tree model...
2024-12-08 20:21:49,641 - Preparing features for Decision-Tree testing...
2024-12-08 20:21:50,763 - Saving predictions to predictions_Decision-Tree.txt...
2024-12-08 20:21:50,871 - Predictions saved successfully.
2024-12-08 20:21:51,930 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.06      0.10      0.07      6861
           E       0.12      0.06      0.08      6829
           N       0.12      0.07      0.09     19728
           O       0.77      0.81      0.79    110355

    accuracy                           0.64    143773
   macro avg       0.27      0.26      0.26    143773
weighted avg       0.61      0.64      0.62    143773

2024-12-08 20:21:52,007 - Testing Random-Forest model...
2024-12-08 20:21:52,909 - Preparing features for Random-Forest testing...
2024-12-08 20:21:56,370 - Saving predictions to predictions_Random-Forest.txt...
2024-12-08 20:21:56,484 - Predictions saved successfully.
2024-12-08 20:21:57,505 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.63      0.01      0.01      6861
           E       0.76      0.00      0.01      6829
           N       0.00      0.00      0.00     19728
           O       0.77      1.00      0.87    110355

    accuracy                           0.77    143773
   macro avg       0.54      0.25      0.22    143773
weighted avg       0.66      0.77      0.67    143773

2024-12-08 20:21:57,598 - Testing Logistic-Regression model...
2024-12-08 20:21:58,366 - Preparing features for Logistic-Regression testing...
2024-12-08 20:21:59,504 - Saving predictions to predictions_Logistic-Regression.txt...
2024-12-08 20:21:59,669 - Predictions saved successfully.
2024-12-08 20:22:00,697 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.06      0.01      0.01      6861
           E       0.00      0.00      0.00      6829
           N       0.17      0.01      0.01     19728
           O       0.77      0.98      0.86    110355

    accuracy                           0.76    143773
   macro avg       0.25      0.25      0.22    143773
weighted avg       0.61      0.76      0.66    143773

2024-12-08 20:22:00,770 - Testing CRF model...
2024-12-08 20:22:01,564 - Preparing features for CRF testing...
2024-12-08 20:22:14,647 - Saving predictions to predictions_CRF.txt...
2024-12-08 20:22:14,697 - Predictions saved successfully.
2024-12-08 20:22:15,688 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.97      0.80      0.88      6861
           E       0.97      0.78      0.86      6829
           N       0.95      0.30      0.45     19728
           O       0.87      1.00      0.93    110355

    accuracy                           0.88    143773
   macro avg       0.94      0.72      0.78    143773
weighted avg       0.89      0.88      0.86    143773

2024-12-08 20:22:16,244 - Testing AdaBoost model...
2024-12-08 20:22:17,069 - Preparing features for AdaBoost testing...
2024-12-08 20:22:19,159 - Saving predictions to predictions_AdaBoost.txt...
2024-12-08 20:22:19,266 - Predictions saved successfully.
2024-12-08 20:22:20,298 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.01      0.00      0.01      6861
           E       0.00      0.00      0.00      6829
           N       0.33      0.00      0.00     19728
           O       0.76      0.97      0.86    110355

    accuracy                           0.75    143773
   macro avg       0.28      0.24      0.22    143773
weighted avg       0.63      0.75      0.66    143773

2024-12-08 20:22:20,370 - Testing GradientBoosting model...
2024-12-08 20:22:21,164 - Preparing features for GradientBoosting testing...
2024-12-08 20:22:24,165 - Saving predictions to predictions_GradientBoosting.txt...
2024-12-08 20:22:24,274 - Predictions saved successfully.
2024-12-08 20:22:25,301 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.09      0.02      0.04      6861
           E       0.47      0.00      0.01      6829
           N       0.05      0.00      0.00     19728
           O       0.77      0.99      0.86    110355

    accuracy                           0.76    143773
   macro avg       0.35      0.25      0.23    143773
weighted avg       0.62      0.76      0.67    143773

2024-12-08 20:22:25,386 - Testing Voting model...
2024-12-08 20:22:26,242 - Preparing features for Voting testing...
2024-12-08 20:22:30,839 - Saving predictions to predictions_Voting.txt...
2024-12-08 20:22:30,946 - Predictions saved successfully.
2024-12-08 20:22:31,969 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.19      0.01      0.02      6861
           E       0.29      0.00      0.01      6829
           N       0.13      0.00      0.00     19728
           O       0.77      1.00      0.87    110355

    accuracy                           0.77    143773
   macro avg       0.34      0.25      0.22    143773
weighted avg       0.63      0.77      0.67    143773

```

## To Do

Plan to add RDR and train/test again.

