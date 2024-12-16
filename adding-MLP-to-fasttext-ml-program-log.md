# Adding MLP and Updating

## Updating Python Code

--evaluate ကိုလည်း ဖြုတ်လိုက်တယ်။ --test ဆိုတာပဲ ထားပြီး၊ --raw နဲ့ control လုပ်ဖို့ ပြောင်းရေးခဲ့တယ်။  
## --help

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./fasttext-ml.py --help
usage: fasttext-ml.py [-h] [--train TRAIN] [--test TEST] [--ft-model FT_MODEL] [--model MODEL]
                      [--method {Decision-Tree,Random-Forest,Logistic-Regression,CRF,AdaBoost,GradientBoosting,Voting,MLP,all}]
                      [--raw] [--output OUTPUT]

FastText + ML Models for Sentence Segmentation.

options:
  -h, --help            show this help message and exit
  --train TRAIN         Train the model. Provide the training corpus file path.
  --test TEST           Test the model. Provide the test corpus file path.
  --ft-model FT_MODEL   FastText model file (default: fasttext_model.bin).
  --model MODEL         Trained model file (default: model.pkl).
  --method {Decision-Tree,Random-Forest,Logistic-Regression,CRF,AdaBoost,GradientBoosting,Voting,MLP,all}, -m {Decision-Tree,Random-Forest,Logistic-Regression,CRF,AdaBoost,GradientBoosting,Voting,MLP,all}
                        Choose the classification method (default: Decision-Tree).
  --raw                 Test the model with raw input (no tags).
  --output OUTPUT       Specify the output file for predictions.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Testing with MLP

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.py --test ./data/syl/bone/test.tagged.bone --ft-model ./fasttext_model.bin --model ./models/MLP.model --me
thod MLP --output a.out
2024-12-12 21:56:23,137 - Testing MLP model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 21:56:23,949 - Preparing features for MLP testing...
2024-12-12 21:56:26,412 - Saving predictions to a.out...
2024-12-12 21:56:26,555 - Predictions saved successfully.
2024-12-12 21:56:27,593 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.17      0.26      6861
           E       0.71      0.77      0.74      6829
           N       0.58      0.21      0.30     19728
           O       0.83      0.95      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.52      0.55    143773
weighted avg       0.77      0.81      0.77    143773


real    0m5.393s
user    0m30.071s
sys     0m20.347s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Run All Methods with BONE  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./run-all.sh | tee run-all-
12Dec.log
Starting training and testing for method: Decision-Tree
Training for method: Decision-Tree
2024-12-12 22:06:29,519 - Loading training data for Decision-Tree...
2024-12-12 22:06:30,229 - Training FastText model for Decision-Tree...
Read 1M words
Number of words:  4482
Number of labels: 0
Progress: 100.0% words/sec/thread:   37144 lr:  0.000000 avg.loss:  2.304370 ETA:   0h 0m 0s
2024-12-12 22:06:38,028 - Preparing features for Decision-Tree...
2024-12-12 22:06:47,509 - Training Decision-Tree model...
2024-12-12 22:07:46,957 - Saving trained model to models/Decision-Tree.model...
2024-12-12 22:07:46,960 - Training for Decision-Tree completed.

real    1m18.938s
user    4m20.458s
sys     0m6.240s
Testing for method: Decision-Tree
2024-12-12 22:07:48,451 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:07:49,270 - Preparing features for Decision-Tree testing...
2024-12-12 22:07:50,382 - Saving predictions to ./models/Decision-Tree.hyp...
2024-12-12 22:07:50,490 - Predictions saved successfully.
2024-12-12 22:07:51,534 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m4.005s
user    0m6.709s
sys     0m4.235s
Completed training and testing for method: Decision-Tree
---------------------------------------------
Starting training and testing for method: Random-Forest
Training for method: Random-Forest
2024-12-12 22:07:52,456 - Loading training data for Random-Forest...
2024-12-12 22:07:53,166 - Loading existing FastText model from ./models/fasttext-features.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:07:53,944 - Preparing features for Random-Forest...
2024-12-12 22:08:02,938 - Training Random-Forest model...
2024-12-12 22:15:29,493 - Saving trained model to models/Random-Forest.model...
2024-12-12 22:15:29,707 - Training for Random-Forest completed.

real    7m38.680s
user    7m38.708s
sys     0m6.867s
Testing for method: Random-Forest
2024-12-12 22:15:31,136 - Testing Random-Forest model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:15:32,078 - Preparing features for Random-Forest testing...
2024-12-12 22:15:35,477 - Saving predictions to ./models/Random-Forest.hyp...
2024-12-12 22:15:35,587 - Predictions saved successfully.
2024-12-12 22:15:36,625 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m6.431s
user    0m9.143s
sys     0m4.226s
Completed training and testing for method: Random-Forest
---------------------------------------------
Starting training and testing for method: Logistic-Regression
Training for method: Logistic-Regression
2024-12-12 22:15:37,572 - Loading training data for Logistic-Regression...
2024-12-12 22:15:38,281 - Loading existing FastText model from ./models/fasttext-features.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:15:39,013 - Preparing features for Logistic-Regression...
2024-12-12 22:15:49,779 - Training Logistic-Regression model...
2024-12-12 22:16:31,629 - Saving trained model to models/Logistic-Regression.model...
2024-12-12 22:16:31,632 - Training for Logistic-Regression completed.

real    0m55.590s
user    13m19.517s
sys     5m15.338s
Testing for method: Logistic-Regression
2024-12-12 22:16:33,158 - Testing Logistic-Regression model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:16:33,969 - Preparing features for Logistic-Regression testing...
2024-12-12 22:16:35,152 - Saving predictions to ./models/Logistic-Regression.hyp...
2024-12-12 22:16:35,313 - Predictions saved successfully.
2024-12-12 22:16:36,349 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.55      0.09      0.16      6861
           E       0.72      0.73      0.72      6829
           N       0.56      0.13      0.21     19728
           O       0.81      0.97      0.88    110355

    accuracy                           0.80    143773
   macro avg       0.66      0.48      0.49    143773
weighted avg       0.76      0.80      0.75    143773


real    0m4.121s
user    0m8.680s
sys     0m6.354s
Completed training and testing for method: Logistic-Regression
---------------------------------------------
Starting training and testing for method: CRF
Training for method: CRF
2024-12-12 22:16:37,276 - Loading training data for CRF...
2024-12-12 22:16:37,980 - Loading existing FastText model from ./models/fasttext-features.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:16:38,711 - Preparing features for CRF...
2024-12-12 22:17:47,012 - Training CRF model...
2024-12-12 22:22:46,010 - Saving trained model to models/CRF.model...
2024-12-12 22:22:46,028 - Training for CRF completed.

real    6m18.815s
user    6m3.701s
sys     0m22.023s
Testing for method: CRF
2024-12-12 22:22:56,096 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:22:56,913 - Preparing features for CRF testing...
2024-12-12 22:23:10,000 - Saving predictions to ./models/CRF.hyp...
2024-12-12 22:23:10,052 - Predictions saved successfully.
2024-12-12 22:23:11,034 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.45      0.61     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773


real    0m16.560s
user    0m17.839s
sys     0m5.659s
Completed training and testing for method: CRF
---------------------------------------------
Starting training and testing for method: AdaBoost
Training for method: AdaBoost
2024-12-12 22:23:12,653 - Loading training data for AdaBoost...
2024-12-12 22:23:13,358 - Loading existing FastText model from ./models/fasttext-features.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:23:14,088 - Preparing features for AdaBoost...
2024-12-12 22:23:23,120 - Training AdaBoost model...
/home/ye/.local/lib/python3.10/site-packages/sklearn/ensemble/_weight_boosting.py:519: FutureWarning: The SAMME.R algorithm (the default) is deprecated and will be removed in 1.6. Use the SAMME algorithm to circumvent this warning.
  warnings.warn(
2024-12-12 22:29:24,763 - Saving trained model to models/AdaBoost.model...
2024-12-12 22:29:24,856 - Training for AdaBoost completed.

real    6m13.629s
user    6m12.915s
sys     0m7.611s
Testing for method: AdaBoost
2024-12-12 22:29:26,283 - Testing AdaBoost model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:29:27,109 - Preparing features for AdaBoost testing...
2024-12-12 22:29:29,241 - Saving predictions to ./models/AdaBoost.hyp...
2024-12-12 22:29:29,352 - Predictions saved successfully.
2024-12-12 22:29:30,375 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.02      0.00      0.00      6861
           E       0.71      0.63      0.67      6829
           N       0.62      0.07      0.13     19728
           O       0.80      0.98      0.88    110355

    accuracy                           0.79    143773
   macro avg       0.54      0.42      0.42    143773
weighted avg       0.73      0.79      0.73    143773


real    0m5.039s
user    0m7.625s
sys     0m4.353s
Completed training and testing for method: AdaBoost
---------------------------------------------
Starting training and testing for method: GradientBoosting
Training for method: GradientBoosting
2024-12-12 22:29:31,319 - Loading training data for GradientBoosting...
2024-12-12 22:29:32,021 - Loading existing FastText model from ./models/fasttext-features.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:29:32,753 - Preparing features for GradientBoosting...
2024-12-12 22:29:42,232 - Training GradientBoosting model...
2024-12-13 00:32:13,244 - Saving trained model to models/GradientBoosting.model...
2024-12-13 00:32:13,332 - Training for GradientBoosting completed.

real    122m43.434s
user    122m35.050s
sys     0m14.631s
Testing for method: GradientBoosting
2024-12-13 00:32:14,754 - Testing GradientBoosting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-13 00:32:15,587 - Preparing features for GradientBoosting testing...
2024-12-13 00:32:18,616 - Saving predictions to ./models/GradientBoosting.hyp...
2024-12-13 00:32:18,727 - Predictions saved successfully.
2024-12-13 00:32:19,756 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.17      0.26      6861
           E       0.71      0.77      0.74      6829
           N       0.62      0.16      0.26     19728
           O       0.82      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.52      0.54    143773
weighted avg       0.78      0.81      0.76    143773


real    0m5.941s
user    0m8.636s
sys     0m4.244s
Completed training and testing for method: GradientBoosting
---------------------------------------------
Starting training and testing for method: Voting
Training for method: Voting
2024-12-13 00:32:20,695 - Loading training data for Voting...
2024-12-13 00:32:21,397 - Loading existing FastText model from ./models/fasttext-features.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-13 00:32:22,127 - Preparing features for Voting...
2024-12-13 00:32:31,480 - Training Voting model...
2024-12-13 00:41:40,065 - Saving trained model to models/Voting.model...
2024-12-13 00:41:40,260 - Training for Voting completed.

real    9m21.024s
user    21m13.427s
sys     4m47.556s
Testing for method: Voting
2024-12-13 00:41:41,722 - Testing Voting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-13 00:41:42,661 - Preparing features for Voting testing...
2024-12-13 00:41:47,320 - Saving predictions to ./models/Voting.hyp...
2024-12-13 00:41:47,428 - Predictions saved successfully.
2024-12-13 00:41:48,463 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m7.666s
user    0m12.171s
sys     0m6.410s
Completed training and testing for method: Voting
---------------------------------------------
Starting training and testing for method: MLP
Training for method: MLP
2024-12-13 00:41:49,385 - Loading training data for MLP...
2024-12-13 00:41:50,085 - Loading existing FastText model from ./models/fasttext-features.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-13 00:41:50,818 - Preparing features for MLP...
2024-12-13 00:41:59,919 - Training MLP model...
2024-12-13 01:05:26,140 - Saving trained model to models/MLP.model...
2024-12-13 01:05:26,257 - Training for MLP completed.

real    23m38.294s
user    405m1.300s
sys     343m59.228s
Testing for method: MLP
2024-12-13 01:05:27,680 - Testing MLP model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-13 01:05:28,495 - Preparing features for MLP testing...
2024-12-13 01:05:30,997 - Saving predictions to ./models/MLP.hyp...
2024-12-13 01:05:31,138 - Predictions saved successfully.
2024-12-13 01:05:32,180 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.16      0.25      6861
           E       0.71      0.77      0.74      6829
           N       0.61      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.52      0.54    143773
weighted avg       0.78      0.81      0.77    143773


real    0m5.427s
user    0m29.930s
sys     0m21.574s
Completed training and testing for method: MLP
---------------------------------------------
All training and testing completed.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Coding ABC Tagger  

```python
import argparse
import fasttext
import numpy as np
import random
from sklearn.metrics import accuracy_score

# Define the Artificial Bee Colony (ABC) algorithm
class ABC_POS_Tagger:
    def __init__(self, embedding_dim, num_bees, max_iter, pos_tags):
        self.embedding_dim = embedding_dim
        self.num_bees = num_bees
        self.max_iter = max_iter
        self.pos_tags = pos_tags

    def initialize_population(self):
        return [np.random.uniform(-1, 1, self.embedding_dim) for _ in range(self.num_bees)]

    def fitness(self, weights, train_data):
        correct = 0
        total = 0
        for sentence, tags in train_data:
            predictions = self.predict(sentence, weights)
            correct += sum(p == t for p, t in zip(predictions, tags))
            total += len(tags)
        return correct / total

    def predict(self, sentence, weights):
        return [self.pos_tags[np.argmax(np.dot(weights, word))] for word in sentence]

    def optimize(self, train_data):
        population = self.initialize_population()
        fitness_values = [self.fitness(w, train_data) for w in population]
        best_solution = population[np.argmax(fitness_values)]
        best_fitness = max(fitness_values)

        for iteration in range(self.max_iter):
            new_population = []
            for bee in population:
                partner = random.choice(population)
                phi = np.random.uniform(-1, 1, self.embedding_dim)
                candidate = bee + phi * (bee - partner)
                candidate_fitness = self.fitness(candidate, train_data)
                if candidate_fitness > self.fitness(bee, train_data):
                    new_population.append(candidate)
                else:
                    new_population.append(bee)

            population = new_population
            fitness_values = [self.fitness(w, train_data) for w in population]

            if max(fitness_values) > best_fitness:
                best_solution = population[np.argmax(fitness_values)]
                best_fitness = max(fitness_values)

        return best_solution

# Utility functions
def load_data(file_path, ft_model):
    data = []
    with open(file_path, "r", encoding="utf-8") as f:
        for line in f:
            words, tags = zip(*[pair.rsplit("/", 1) for pair in line.strip().split()])
            word_embeddings = [ft_model.get_word_vector(word) for word in words]
            data.append((word_embeddings, tags))
    return data

def test_model(test_data, weights, pos_tags):
    correct = 0
    total = 0
    predictions = []
    for sentence, tags in test_data:
        pred = [pos_tags[np.argmax(np.dot(weights, word))] for word in sentence]
        predictions.extend(pred)
        correct += sum(p == t for p, t in zip(pred, tags))
        total += len(tags)
    return accuracy_score(predictions, [tag for _, tags in test_data for tag in tags])

def main():
    parser = argparse.ArgumentParser(description="POS Tagger using ABC Algorithm.")
    parser.add_argument("--train", help="Training data file (word/tag format).", required=True)
    parser.add_argument("--test", help="Testing data file (word/tag format).", required=True)
    parser.add_argument("--ft-model", help="FastText model file.", required=True)
    parser.add_argument("--output", help="Output file for results.", required=False, default="output.txt")
    parser.add_argument("--num-bees", type=int, default=20, help="Number of bees in the colony.")
    parser.add_argument("--max-iter", type=int, default=100, help="Maximum number of iterations.")

    args = parser.parse_args()

    # Load FastText model
    ft_model = fasttext.load_model(args.ft_model)

    # Load training and testing data
    train_data = load_data(args.train, ft_model)
    test_data = load_data(args.test, ft_model)

    # Extract unique POS tags from the training data
    pos_tags = sorted({tag for _, tags in train_data for tag in tags})
    embedding_dim = len(train_data[0][0][0])

    # Initialize and train the ABC POS Tagger
    abc_tagger = ABC_POS_Tagger(embedding_dim, args.num_bees, args.max_iter, pos_tags)
    best_weights = abc_tagger.optimize(train_data)

    # Test the model
    accuracy = test_model(test_data, best_weights, pos_tags)
    print(f"Accuracy: {accuracy * 100:.2f}%")

    # Save results
    with open(args.output, "w") as f:
        f.write(f"Accuracy: {accuracy * 100:.2f}%\n")

if __name__ == "__main__":
    main()

```

call --help  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./abc-tagger.py --help
usage: abc-tagger.py [-h] --train TRAIN --test TEST --ft-model FT_MODEL [--output OUTPUT]
                     [--num-bees NUM_BEES] [--max-iter MAX_ITER]

POS Tagger using ABC Algorithm.

options:
  -h, --help           show this help message and exit
  --train TRAIN        Training data file (word/tag format).
  --test TEST          Testing data file (word/tag format).
  --ft-model FT_MODEL  FastText model file.
  --output OUTPUT      Output file for results.
  --num-bees NUM_BEES  Number of bees in the colony.
  --max-iter MAX_ITER  Maximum number of iterations.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Very long to train ...  လက်တွေ့မှာ သုံးဖို့ ခက်နိုင်တာနဲ့ အချိန်ပေး study/develop လုပ်မှ ဖြစ်မှာမို့ ခဏ နားထားခဲ့...  

## Adding HMM  

HMM က မထည့်လို့ မဖြစ်ဘူးလေ ...  

```python
import argparse
import os
import fasttext
import numpy as np
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier, AdaBoostClassifier, GradientBoostingClassifier, VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.neural_network import MLPClassifier
from sklearn_crfsuite import CRF
from sklearn_crfsuite.metrics import flat_classification_report
from sklearn.metrics import classification_report
from hmmlearn import hmm
#from sklearn.preprocessing import LabelEncoder
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

def encode_labels(labels, label_mapping):
    """Encode labels into numeric values."""
    return [[label_mapping[label] for label in sentence_labels] for sentence_labels in labels]

def decode_labels(encoded_labels, label_mapping):
    """Decode numeric labels back to original tags."""
    reverse_mapping = {v: k for k, v in label_mapping.items()}
    return [[reverse_mapping[label] for label in sentence_labels] for sentence_labels in encoded_labels]

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
    elif method == "HMM":
        X = prepare_features(sentences, ft_model)
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
    elif method == "MLP":
        model = MLPClassifier(hidden_layer_sizes=(100,), max_iter=500, random_state=42)
    elif method == "HMM":
        label_mapping = {label: idx for idx, label in enumerate(set(flatten_labels(labels)))}
        encoded_labels = encode_labels(labels, label_mapping)
        lengths = [len(sentence) for sentence in sentences]
        model = hmm.MultinomialHMM(n_components=len(label_mapping), n_iter=100, verbose=True)
        model.startprob_ = np.ones(len(label_mapping)) / len(label_mapping)
        model.transmat_ = np.ones((len(label_mapping), len(label_mapping))) / len(label_mapping)
        model.fit(np.array(flatten_labels(encoded_labels)).reshape(-1, 1), lengths)
        model.label_mapping = label_mapping
    else:
        raise ValueError(f"Unsupported method: {method}")

    model.fit(X, y)
    logger.info(f"Saving trained model to {output_model_file}...")
    joblib.dump(model, output_model_file)
    logger.info(f"Training for {method} completed.")

def test_model(test_file, ft_model_file, trained_model_file, raw_test, method, output_file, logger):
    """Test the model on the provided test data."""
    logger.info(f"Testing {method} model...")

    if raw_test:
        sentences = load_raw_data(test_file)
        labels = None
    else:
        sentences, labels = load_tagged_data(test_file)

    ft_model = fasttext.load_model(ft_model_file)
    model = joblib.load(trained_model_file)

    logger.info(f"Preparing features for {method} testing...")
    if method == "CRF":
        X = prepare_features_for_crf(sentences, ft_model)
        predictions = model.predict(X)
    elif method == "HMM":
        X = prepare_features(sentences, ft_model)
        lengths = [len(sentence) for sentence in sentences]
        encoded_predictions = model.predict(np.array(X).reshape(-1, 1), lengths)
        predictions = decode_labels(encoded_predictions, model.label_mapping)
    else:
        X = prepare_features(sentences, ft_model)
        predictions = model.predict(X)

        # Realign flat predictions to sentence structure
        #sentence_lengths = [len(sentence) for sentence in sentences]
        #predictions = [predictions[start:start + length] for start, length in zip(np.cumsum([0] + sentence_lengths[:-1]), sentence_lengths)]
        # Realign flat predictions to sentence structure
        sentence_lengths = [len(sentence) for sentence in sentences]
        start_idx = 0
        realigned_predictions = []

        for length in sentence_lengths:
            realigned_predictions.append(predictions[start_idx:start_idx + length])
            start_idx += length

        predictions = realigned_predictions

    logger.info(f"Saving predictions to {output_file}...")
    #with open(output_file, 'w', encoding='utf-8') as f:
    #    for sentence, sentence_predictions in zip(sentences, predictions):
    #        formatted_sentence = " ".join(f"{word}/{tag}" for word, tag in zip(sentence, sentence_predictions))
    #        f.write(f"{formatted_sentence}\n")
    with open(output_file, 'w', encoding='utf-8') as f:
        for sentence, sentence_predictions in zip(sentences, predictions):
            formatted_sentence = " ".join(f"{word}/{tag}" for word, tag in zip(sentence, sentence_predictions))
            f.write(f"{formatted_sentence}\n")

    logger.info(f"Predictions saved successfully.")

    if not raw_test:
        flattened_true = flatten_labels(labels)
        flattened_predictions = flatten_labels(predictions)

        #if len(flattened_true) != len(flattened_predictions):
        #    logger.error(f"Length mismatch: true labels ({len(flattened_true)}) vs predictions ({len(flattened_predictions)})")
        #    raise ValueError(f"Length mismatch: true labels and predictions have different lengths!")

        if len(flattened_true) != len(flattened_predictions):
            logger.error(f"Length mismatch: true labels ({len(flattened_true)}) vs predictions ({len(flattened_predictions)})")
            for i, (t, p) in enumerate(zip(flattened_true, flattened_predictions)):
                print(f"Index {i}: True={t}, Predicted={p}")
            raise ValueError("Length mismatch detected!")

        if method == "CRF":
            report = flat_classification_report(labels, predictions)
        else:
            report = classification_report(flattened_true, flattened_predictions)

        logger.info(f"Evaluation Results:\n{report}")

def main():
    parser = argparse.ArgumentParser(description="FastText + ML Models for Sentence Segmentation.")
    parser.add_argument("--train", help="Train the model. Provide the training corpus file path.")
    parser.add_argument("--test", help="Test the model. Provide the test corpus file path.")
    parser.add_argument("--ft-model", default="fasttext_model.bin", help="FastText model file (default: fasttext_model.bin).")
    parser.add_argument("--model", default="model.pkl", help="Trained model file (default: model.pkl).")
    parser.add_argument("--method", "-m", default="CRF",
                        choices=["Decision-Tree", "Random-Forest", "Logistic-Regression", "HMM", "CRF", "AdaBoost", "GradientBoosting", "Voting", "MLP", "all"],
                        help="Choose the classification method (default: CRF).")
    parser.add_argument("--raw", action="store_true", help="Test the model with raw input (no tags).")
    parser.add_argument("--output", help="Specify the output file for predictions.")

    args = parser.parse_args()

    logging.basicConfig(filename="all-training-testing.log" if args.method == "all" else None,
                        level=logging.INFO,
                        format="%(asctime)s - %(message)s")
    logger = logging.getLogger()

    if args.method == "all":
        methods = ["Decision-Tree", "Random-Forest", "Logistic-Regression", "HMM", "CRF", "AdaBoost", "GradientBoosting", "Voting", "MLP"]
    else:
        methods = [args.method]

    if args.train:
        for method in methods:
            model_file = f"models/{method}.model"
            train_model(args.train, args.ft_model, model_file, method, logger)
    elif args.test or args.raw:
        raw_mode = args.raw  # True if raw, False otherwise
        for method in methods:
            model_file = f"models/{method}.model"
            default_output_file = f"predictions_{method}.txt"
            output_file = args.output or default_output_file
            test_model(
                test_file=args.test,
                ft_model_file=args.ft_model,
                trained_model_file=model_file,
                raw_test=raw_mode,
                method=method,
                output_file=output_file,
                logger=logger
            )
    else:
        parser.print_help()


if __name__ == "__main__":
    main()


```

CRF ကို default အဖြစ်ထားလိုက်ပြီ။  
--help  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./fasttext-ml.py --help
usage: fasttext-ml.py [-h] [--train TRAIN] [--test TEST] [--ft-model FT_MODEL] [--model MODEL]
                      [--method {Decision-Tree,Random-Forest,Logistic-Regression,HMM,CRF,AdaBoost,GradientBoosting,Voting,MLP,all}]
                      [--raw] [--output OUTPUT]

FastText + ML Models for Sentence Segmentation.

options:
  -h, --help            show this help message and exit
  --train TRAIN         Train the model. Provide the training corpus file path.
  --test TEST           Test the model. Provide the test corpus file path.
  --ft-model FT_MODEL   FastText model file (default: fasttext_model.bin).
  --model MODEL         Trained model file (default: model.pkl).
  --method {Decision-Tree,Random-Forest,Logistic-Regression,HMM,CRF,AdaBoost,GradientBoosting,Voting,MLP,all}, -m {Decision-Tree,Random-Forest,Logistic-Regression,HMM,CRF,AdaBoost,GradientBoosting,Voting,MLP,all}
                        Choose the classification method (default: CRF).
  --raw                 Test the model with raw input (no tags).
  --output OUTPUT       Specify the output file for predictions.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Training with HMM ...  

```
         1      -0.00000000             +nan
         2      -0.00000000      +0.00000000
Traceback (most recent call last):
  File "/home/ye/data/hello-sayarwon/coding/model-based/./fasttext-ml.py", line 274, in <module>
    main()
  File "/home/ye/data/hello-sayarwon/coding/model-based/./fasttext-ml.py", line 253, in main
    train_model(args.train, args.ft_model, model_file, method, logger)
  File "/home/ye/data/hello-sayarwon/coding/model-based/./fasttext-ml.py", line 147, in train_model
    model.fit(X, y)
  File "/home/ye/.local/lib/python3.10/site-packages/hmmlearn/base.py", line 480, in fit
    self._init(X, lengths)
  File "/home/ye/.local/lib/python3.10/site-packages/hmmlearn/hmm.py", line 919, in _init
    super()._init(X, lengths=None)
  File "/home/ye/.local/lib/python3.10/site-packages/hmmlearn/base.py", line 928, in _init
    self._check_and_set_n_features(X)
  File "/home/ye/.local/lib/python3.10/site-packages/hmmlearn/_emissions.py", line 317, in _check_and_set_n_features
    super()._check_and_set_n_features(X)
  File "/home/ye/.local/lib/python3.10/site-packages/hmmlearn/base.py", line 539, in _check_and_set_n_features
    raise ValueError(
ValueError: Unexpected number of dimensions, got 100 but expected 1

real    1m28.958s
user    2m3.713s
sys     0m12.191s
```

HMM Tagger ကို word2vec, fasttext embedding နဲ့ implementation လုပ်တာက ဖြစ်နိုင်ပေမဲ့ လက်တွေ့ ဖြေရှင်းရတဲ့ ပြဿနာက HMM ရဲ့ observation က categorical or have fixed dimensionality နဲ့သွားတာ။ ဆိုလိုတာက "a sequence of scalar or categorical values" နဲ့ အလုပ်လုပ်တယ်။ ဒါပေမဲ့ လက်ရှိ fasttext embedding က "100-dimensional embeddings" ဖြစ်နေတယ်။ အဲဒါကို ညှိပေးဖို့ လိုအပ်တယ်။  

## Changed with pomegranate Library  

hmmlearn library အစား pomegranate ကို သုံးကြည့်မယ်။  

```
pip install pomegranate
```

```
Downloading numba-0.60.0-cp310-cp310-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (3.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 3.7/3.7 MB 37.0 MB/s eta 0:00:00
Using cached typing_extensions-4.12.2-py3-none-any.whl (37 kB)
Downloading llvmlite-0.43.0-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (43.9 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 43.9/43.9 MB 100.2 MB/s eta 0:00:00
Building wheels for collected packages: apricot-select
  Building wheel for apricot-select (setup.py) ... done
  Created wheel for apricot-select: filename=apricot_select-0.6.1-py3-none-any.whl size=48764 sha256=b0875904d0dbaeb4b82b00c9c9c91f6166f978c41961ea7415aa8e8c63af09ef
  Stored in directory: /home/ye/.cache/pip/wheels/df/d8/f9/4d62b7272bff772a126a52e507212c2fd33c0b8416d9389665
Successfully built apricot-select
Installing collected packages: typing-extensions, llvmlite, numba, apricot-select, pomegranate
  Attempting uninstall: typing-extensions
    Found existing installation: typing_extensions 4.3.0
    Uninstalling typing_extensions-4.3.0:
      Successfully uninstalled typing_extensions-4.3.0
ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
tensorflow 2.13.0 requires typing-extensions<4.6.0,>=3.6.6, but you have typing-extensions 4.12.2 which is incompatible.
Successfully installed apricot-select-0.6.1 llvmlite-0.43.0 numba-0.60.0 pomegranate-1.1.1 typing-extensions-4.12.2

[notice] A new release of pip is available: 24.2 -> 24.3.1
[notice] To update, run: /usr/bin/python3 -m pip install --upgrade pip
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

When I run, got following error:  

```
  File "/home/ye/data/hello-sayarwon/coding/model-based/./fasttext-ml.py", line 12, in <module>
    from pomegranate import HiddenMarkovModel, DiscreteDistribution
ImportError: cannot import name 'HiddenMarkovModel' from 'pomegranate' (/home/ye/.local/lib/python3.10/site-packages/pomegranate/__init__.py)

real    0m0.862s
user    0m3.950s
sys     0m3.580s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

စစ်ကြည့်တော့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ pip show pomegranate

Name: pomegranate
Version: 1.1.1
Summary: A PyTorch implementation of probabilistic models.
Home-page: https://github.com/jmschrei/torchegranate
Author: Jacob Schreiber
Author-email: jmschreiber91@gmail.com
License: LICENSE.txt
Location: /home/ye/.local/lib/python3.10/site-packages
Requires: apricot-select, networkx, numpy, scikit-learn, scipy, torch
Required-by:
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

လက်ရှိ ဗားရှင်းက pytorch နဲ့ သုံးတဲ့ကောင်၊ ငါလိုချင်တာက original version ဒါကြောင့် library ကို ဖျက်ပြီး ဗားရှင်းအတိအကျကို ပြန် install လုပ်ခဲ့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ pip uninstall pomegranate
Found existing installation: pomegranate 1.1.1
Uninstalling pomegranate-1.1.1:
  Would remove:
    /home/ye/.local/lib/python3.10/site-packages/pomegranate-1.1.1.dist-info/*
    /home/ye/.local/lib/python3.10/site-packages/pomegranate/*
Proceed (Y/n)?
  Successfully uninstalled pomegranate-1.1.1
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Installation လုပ်တော့ error တက်...  

```
          super().run_setup(setup_script=setup_script)
        File "/tmp/pip-build-env-0br1ndag/overlay/local/lib/python3.10/dist-packages/setuptools/build_meta.py", line 320, in run_setup
          exec(code, locals())
        File "<string>", line 61, in <module>
        File "/tmp/pip-build-env-0br1ndag/overlay/local/lib/python3.10/dist-packages/Cython/Build/Dependencies.py", line 1154, in cythonize
          cythonize_one(*args)
        File "/tmp/pip-build-env-0br1ndag/overlay/local/lib/python3.10/dist-packages/Cython/Build/Dependencies.py", line 1321, in cythonize_one
          raise CompileError(None, pyx_file)
      Cython.Compiler.Errors.CompileError: pomegranate/utils.pyx
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.

[notice] A new release of pip is available: 24.2 -> 24.3.1
[notice] To update, run: /usr/bin/python3 -m pip install --upgrade pip
error: subprocess-exited-with-error

× Getting requirements to build wheel did not run successfully.
│ exit code: 1
╰─> See above for output.

note: This error originates from a subprocess, and is likely not a problem with pip.
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ pip install --upgrade pip
Defaulting to user installation because normal site-packages is not writeable
Requirement already satisfied: pip in /home/ye/.local/lib/python3.10/site-packages (24.2)

Collecting pip
  Downloading pip-24.3.1-py3-none-any.whl.metadata (3.7 kB)
Downloading pip-24.3.1-py3-none-any.whl (1.8 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.8/1.8 MB 21.6 MB/s eta 0:00:00
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 24.2
    Uninstalling pip-24.2:
      Successfully uninstalled pip-24.2
Successfully installed pip-24.3.1
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
          self.run_setup()
        File "/tmp/pip-build-env-_uzundji/overlay/local/lib/python3.10/dist-packages/setuptools/build_meta.py", line 522, in run_setup
          super().run_setup(setup_script=setup_script)
        File "/tmp/pip-build-env-_uzundji/overlay/local/lib/python3.10/dist-packages/setuptools/build_meta.py", line 320, in run_setup
          exec(code, locals())
        File "<string>", line 61, in <module>
        File "/tmp/pip-build-env-_uzundji/overlay/local/lib/python3.10/dist-packages/Cython/Build/Dependencies.py", line 1154, in cythonize
          cythonize_one(*args)
        File "/tmp/pip-build-env-_uzundji/overlay/local/lib/python3.10/dist-packages/Cython/Build/Dependencies.py", line 1321, in cythonize_one
          raise CompileError(None, pyx_file)
      Cython.Compiler.Errors.CompileError: pomegranate/utils.pyx
      [end of output]

  note: This error originates from a subprocess, and is likely not a problem with pip.
error: subprocess-exited-with-error

× Getting requirements to build wheel did not run successfully.
│ exit code: 1
╰─> See above for output.

note: This error originates from a subprocess, and is likely not a problem with pip.
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

HMM က CRF လောက် ရလဒ်မကောင်းတာက သေချာတယ်။ ပြီးတော့ fasttext embedding နဲ့ သုံးဖို့ ဆိုရင် user တွေအနေနဲ့ တခြား library ကိုလည်း သုံးရမှာမို့လို့ HMM ကို မထည့်ဖို့ ဆုံးဖြတ်လိုက်တယ်။  
```

## Supporting word2vec

gensim နဲ့ ဆောက်ထားတဲ့ word2vec ကို sklearn ကနေ ခေါ်သုံးတာမှာ အရမ်းအဆင်မပြေလို့ ... flair ကို သုံးကြည့်ခဲ့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ pip install flair
...
...
...
cb943f6abd277663554918f8f31cdfb94ac3816b9357f8a3fe30319bc1
  Stored in directory: /home/ye/.cache/pip/wheels/4c/96/18/b9201cc3e8b47b02b510460210cfd832ccf10c0c4dd0522962
  Building wheel for intervaltree (setup.py) ... done
  Created wheel for intervaltree: filename=intervaltree-3.1.0-py2.py3-none-any.whl size=26095 sha256=a1dc935499e9a8d2540de553ef84b1cf63e8c3336d674575be0328fedf0dc0dd
  Stored in directory: /home/ye/.cache/pip/wheels/fa/80/8c/43488a924a046b733b64de3fac99252674c892a4c3801c0a61
Successfully built langdetect pptree sqlitedict wikipedia-api intervaltree
Installing collected packages: sqlitedict, sortedcontainers, pptree, soupsieve, semver, segtok, safetensors, PySocks, more-itertools, langdetect, jsonlines, jmespath, intervaltree, ftfy, deprecated, conllu, wikipedia-api, huggingface-hub, botocore, bioc, beautifulsoup4, s3transfer, mpld3, gdown, pytorch-revgrad, boto3, accelerate, transformer-smaller-training-vocab, flair
  Attempting uninstall: safetensors
    Found existing installation: safetensors 0.4.2
    Uninstalling safetensors-0.4.2:
      Successfully uninstalled safetensors-0.4.2
  Attempting uninstall: huggingface-hub
    Found existing installation: huggingface-hub 0.20.3
    Uninstalling huggingface-hub-0.20.3:
      Successfully uninstalled huggingface-hub-0.20.3
Successfully installed PySocks-1.7.1 accelerate-1.2.1 beautifulsoup4-4.12.3 bioc-2.1 boto3-1.35.81 botocore-1.35.81 conllu-4.5.3 deprecated-1.2.15 flair-0.14.0 ftfy-6.3.1 gdown-5.2.0 huggingface-hub-0.26.5 intervaltree-3.1.0 jmespath-1.0.1 jsonlines-4.0.0 langdetect-1.0.9 more-itertools-10.5.0 mpld3-0.5.10 pptree-3.1 pytorch-revgrad-0.2.0 s3transfer-0.10.4 safetensors-0.4.5 segtok-1.5.11 semver-3.0.2 sortedcontainers-2.4.0 soupsieve-2.6 sqlitedict-2.1.0 transformer-smaller-training-vocab-0.4.0 wikipedia-api-0.7.1
```

flair library နဲ့စမ်းတာလည်း အဆင်မပြေဘူး။  

## Double Model  

error correction ကိုပဲ နောက်ထပ် မော်ဒယ် ထပ်ဆောက်ပြီး run ကြည့်ဖို့ ပြင်ဆင်ခဲ့...  

```bash
#!/bin/bash

# Define paths for input and output
TEST_FILE="./data/syl/bone/train-valid.tagged.bone"
FT_MODEL="./models/fasttext/fasttext-features.bin"
MODELS_DIR="./models/fasttext/"

# List of methods
METHODS=("Decision-Tree" "Random-Forest" "Logistic-Regression" "CRF" "AdaBoost" "GradientBoosting" "Voting" "MLP")

# Loop through each method and run training and testing
for METHOD in "${METHODS[@]}"; do

    # Define model file name based on the method
    MODEL_FILE="${MODELS_DIR}/${METHOD}.model"
    echo $MODEL_FILE;
    # Test
    echo "Testing with training data for method: $METHOD"
    time python ./fasttext-ml.version2.py --test "$TEST_FILE" --ft-model "$FT_MODEL" --model "$MODEL_FILE" --method "$METHOD" --output "${MODELS_DIR}/dummy/${METHOD}.train.hyp"

    echo "Completed testing with training data for method: $METHOD"
    echo "---------------------------------------------"
done

echo "All testing with training data completed."


```

Running Log ...  

```
./models/fasttext//Decision-Tree.model
Testing with training data for method: Decision-Tree
Completed testing with training data for method: Decision-Tree
---------------------------------------------
./models/fasttext//Random-Forest.model
Testing with training data for method: Random-Forest
Completed testing with training data for method: Random-Forest
---------------------------------------------
./models/fasttext//Logistic-Regression.model
Testing with training data for method: Logistic-Regression
Completed testing with training data for method: Logistic-Regression
---------------------------------------------
./models/fasttext//CRF.model
Testing with training data for method: CRF
Completed testing with training data for method: CRF
---------------------------------------------
./models/fasttext//AdaBoost.model
Testing with training data for method: AdaBoost
Completed testing with training data for method: AdaBoost
---------------------------------------------
./models/fasttext//GradientBoosting.model
Testing with training data for method: GradientBoosting
Completed testing with training data for method: GradientBoosting
---------------------------------------------
./models/fasttext//Voting.model
Testing with training data for method: Voting
Completed testing with training data for method: Voting
---------------------------------------------
./models/fasttext//MLP.model
Testing with training data for method: MLP
Completed testing with training data for method: MLP
---------------------------------------------
All testing with training data completed.

```

Check the testing result with training data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./fasttext.test-train.
sh | tee prepare_dummy.log
./models/fasttext//Decision-Tree.model
Testing with training data for method: Decision-Tree
2024-12-15 08:55:06,076 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` obje
ct which is very similar.
2024-12-15 08:55:07,526 - Preparing features for Decision-Tree testing...
2024-12-15 08:55:17,971 - Saving predictions to ./models/fasttext//dummy/Decision-Tree.train.hyp...
2024-12-15 08:55:19,002 - Predictions saved successfully.
2024-12-15 08:55:29,299 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.58      0.19      0.29     62900
           E       0.71      0.77      0.74     62591
           N       0.61      0.19      0.29    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.53      0.55   1334843
weighted avg       0.78      0.81      0.77   1334843


real    0m24.768s
user    0m26.086s
sys     0m5.395s
Completed testing with training data for method: Decision-Tree
---------------------------------------------
./models/fasttext//Random-Forest.model
Testing with training data for method: Random-Forest
2024-12-15 08:55:30,820 - Testing Random-Forest model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 08:55:32,397 - Preparing features for Random-Forest testing...
2024-12-15 08:56:06,144 - Saving predictions to ./models/fasttext//dummy/Random-Forest.train.hyp...
2024-12-15 08:56:07,170 - Predictions saved successfully.
2024-12-15 08:56:17,440 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.58      0.19      0.28     62900
           E       0.71      0.77      0.74     62591
           N       0.61      0.19      0.29    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.53      0.55   1334843
weighted avg       0.78      0.81      0.77   1334843


real    0m48.132s
user    0m48.500s
sys     0m6.419s
Completed testing with training data for method: Random-Forest
---------------------------------------------
./models/fasttext//Logistic-Regression.model
Testing with training data for method: Logistic-Regression
2024-12-15 08:56:18,953 - Testing Logistic-Regression model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 08:56:20,401 - Preparing features for Logistic-Regression testing...
2024-12-15 08:56:31,098 - Saving predictions to ./models/fasttext//dummy/Logistic-Regression.train.hyp...
2024-12-15 08:56:32,074 - Predictions saved successfully.
2024-12-15 08:56:42,363 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.09      0.15     62900
           E       0.72      0.73      0.72     62591
           N       0.56      0.13      0.21    180095
           O       0.82      0.97      0.89   1029257

    accuracy                           0.80   1334843
   macro avg       0.66      0.48      0.49   1334843
weighted avg       0.77      0.80      0.75   1334843


real    0m24.892s
user    0m31.020s
sys     0m8.550s
Completed testing with training data for method: Logistic-Regression
---------------------------------------------
./models/fasttext//CRF.model
Testing with training data for method: CRF
2024-12-15 08:56:43,845 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 08:56:45,306 - Preparing features for CRF testing...
2024-12-15 08:59:04,428 - Saving predictions to ./models/fasttext//dummy/CRF.train.hyp...
2024-12-15 08:59:04,905 - Predictions saved successfully.
2024-12-15 08:59:14,693 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.99      0.85      0.92     62900
           E       0.99      0.85      0.92     62591
           N       0.93      0.45      0.61    180095
           O       0.90      0.99      0.94   1029257

    accuracy                           0.91   1334843
   macro avg       0.95      0.79      0.85   1334843
weighted avg       0.91      0.91      0.90   1334843


real    2m39.173s
user    2m27.023s
sys     0m18.924s
Completed testing with training data for method: CRF
---------------------------------------------
./models/fasttext//AdaBoost.model
Testing with training data for method: AdaBoost
2024-12-15 08:59:23,036 - Testing AdaBoost model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 08:59:24,501 - Preparing features for AdaBoost testing...
2024-12-15 08:59:48,024 - Saving predictions to ./models/fasttext//dummy/AdaBoost.train.hyp...
2024-12-15 08:59:49,163 - Predictions saved successfully.
2024-12-15 08:59:59,355 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.03      0.00      0.00     62900
           E       0.72      0.63      0.67     62591
           N       0.64      0.08      0.13    180095
           O       0.80      0.98      0.88   1029257

    accuracy                           0.80   1334843
   macro avg       0.55      0.42      0.42   1334843
weighted avg       0.74      0.80      0.73   1334843


real    0m37.906s
user    0m37.940s
sys     0m6.555s
Completed testing with training data for method: AdaBoost
---------------------------------------------
./models/fasttext//GradientBoosting.model
Testing with training data for method: GradientBoosting
2024-12-15 09:00:00,963 - Testing GradientBoosting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 09:00:02,437 - Preparing features for GradientBoosting testing...
2024-12-15 09:00:31,744 - Saving predictions to ./models/fasttext//dummy/GradientBoosting.train.hyp...
2024-12-15 09:00:32,815 - Predictions saved successfully.
2024-12-15 09:00:43,321 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.17      0.26     62900
           E       0.71      0.76      0.74     62591
           N       0.63      0.17      0.26    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.52      0.54   1334843
weighted avg       0.78      0.81      0.77   1334843


real    0m44.007s
user    0m44.977s
sys     0m5.640s
Completed testing with training data for method: GradientBoosting
---------------------------------------------
./models/fasttext//Voting.model
Testing with training data for method: Voting
2024-12-15 09:00:44,929 - Testing Voting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` obje
ct which is very similar.
2024-12-15 09:00:46,509 - Preparing features for Voting testing...
2024-12-15 09:01:29,949 - Saving predictions to ./models/fasttext//dummy/Voting.train.hyp...
2024-12-15 09:01:30,966 - Predictions saved successfully.
2024-12-15 09:01:41,160 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.58      0.19      0.28     62900
           E       0.71      0.77      0.74     62591
           N       0.61      0.19      0.29    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.53      0.55   1334843
weighted avg       0.78      0.81      0.77   1334843


real    0m57.799s
user    1m2.405s
sys     0m10.065s
Completed testing with training data for method: Voting
---------------------------------------------
./models/fasttext//MLP.model
Testing with training data for method: MLP
2024-12-15 09:01:42,746 - Testing MLP model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 09:01:44,196 - Preparing features for MLP testing...
2024-12-15 09:02:07,357 - Saving predictions to ./models/fasttext//dummy/MLP.train.hyp...
2024-12-15 09:02:08,407 - Predictions saved successfully.
2024-12-15 09:02:18,697 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.16      0.25     62900
           E       0.71      0.76      0.73     62591
           N       0.61      0.19      0.29    180095
           O       0.83      0.96      0.89   1029257

    accuracy                           0.81   1334843
   macro avg       0.68      0.52      0.54   1334843
weighted avg       0.78      0.81      0.77   1334843


real    0m37.620s
user    3m49.188s
sys     2m20.861s
Completed testing with training data for method: MLP
---------------------------------------------
All testing with training data completed.

real    7m14.301s
user    10m27.143s
sys     3m22.414s
```

Check the predicted output file with training data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ wc *
    50081   1334906  15924599 AdaBoost.train.hyp
    50081   1334906  15924599 CRF.train.hyp
    50081   1334906  15924599 Decision-Tree.train.hyp
    50081   1334906  15924599 GradientBoosting.train.hyp
    50081   1334906  15924599 Logistic-Regression.train.hyp
    50081   1334906  15924599 MLP.train.hyp
    50081   1334906  15924599 Random-Forest.train.hyp
    50081   1334906  15924599 Voting.train.hyp
   400648  10679248 127396792 total
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ head *.hyp
==> AdaBoost.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/O
ဈေး/O က/O များ/O လှ/O ချေ/O လား/E
သူ/O ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/E ထင်/O တယ်/E
ဘာ/O ကြောင့်/O လဲ/E ဆို/O စမ်း/O ပါ/N ဦး/O
စိတ်/O ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/O ပြန်/O ပြီ/O
၁/O ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/O ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/E တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/O ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/O ခြင်း/O ဖြစ်/O သည်/E ဟု/O တွေး/O ယူ/O ခဲ့/O ဖူး/O လေ/O သည်/E
ဂင်မ်/O ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/O တယ်/E
အ/O အေး/O မိ/O မယ်/O
ဧည့်/O လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/O လို့/O ရ/O လား/E
မှန်/O တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/O ရင်း/O ကောက်/O မော့/O လိုက်/O သည်/E ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/O လိုက်/O ရ/O သည်/E

==> CRF.train.hyp <==
နား/B လည်/N ပါ/N ပြီ/E
ဈေး/B က/O များ/O လှ/O ချေ/N လား/E
သူ/B ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/O ထင်/N တယ်/E
ဘာ/B ကြောင့်/O လဲ/O ဆို/O စမ်း/O ပါ/N ဦး/E
စိတ်/B ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/N ပြန်/N ပြီ/E
၁/B ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/O ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/O တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/O ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/O ခြင်း/O ဖြစ်/O သည်/O ဟု/O တွေး/O ယူ/N ခဲ့/N ဖူး/N လေ/N သည်/E
ဂင်မ်/B ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/N တယ်/E
အ/B အေး/N မိ/N မယ်/E
ဧည့်/B လမ်း/O ညွှန်/O ရော/O ထည့်/N ပေး/N လို့/N ရ/N လား/E
မှန်/B တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/O ရင်း/O ကောက်/O မော့/O လိုက်/O သည်/O ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/N လိုက်/N ရ/N သည်/E

==> Decision-Tree.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E
ဈေး/O က/O များ/O လှ/O ချေ/E လား/E
သူ/O ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/E ထင်/N တယ်/E
ဘာ/O ကြောင့်/O လဲ/E ဆို/O စမ်း/O ပါ/N ဦး/O
စိတ်/O ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/N ပြန်/O ပြီ/E
၁/O ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/B ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/E တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/N ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/N ခြင်း/O ဖြစ်/O သည်/E ဟု/O တွေး/O ယူ/O ခဲ့/N ဖူး/O လေ/O သည်/E
ဂင်မ်/O ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/N တယ်/E
အ/O အေး/O မိ/O မယ်/E
ဧည့်/O လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/N လို့/O ရ/O လား/E
မှန်/O တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/N ရင်း/O ကောက်/O မော့/O လိုက်/N သည်/E ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/O လိုက်/N ရ/O သည်/E

==> GradientBoosting.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E
ဈေး/O က/O များ/O လှ/O ချေ/E လား/E
သူ/O ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/E ထင်/O တယ်/E
ဘာ/O ကြောင့်/O လဲ/E ဆို/O စမ်း/O ပါ/N ဦး/O
စိတ်/O ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/N ပြန်/O ပြီ/E
၁/O ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/B ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/E တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/N ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/N ခြင်း/O ဖြစ်/O သည်/E ဟု/O တွေး/O ယူ/O ခဲ့/N ဖူး/O လေ/O သည်/E
ဂင်မ်/O ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/O တယ်/E
အ/O အေး/O မိ/O မယ်/E
ဧည့်/O လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/N လို့/O ရ/O လား/E
မှန်/O တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/O ရင်း/O ကောက်/O မော့/O လိုက်/O သည်/E ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/O လိုက်/O ရ/O သည်/E

==> Logistic-Regression.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/O
ဈေး/O က/O များ/O လှ/O ချေ/O လား/E
သူ/O ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/E ထင်/N တယ်/E
ဘာ/O ကြောင့်/O လဲ/E ဆို/O စမ်း/O ပါ/N ဦး/O
စိတ်/O ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/N ပြန်/O ပြီ/O
၁/O ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/O ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/E တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/N ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/N ခြင်း/O ဖြစ်/O သည်/E ဟု/O တွေး/O ယူ/O ခဲ့/N ဖူး/O လေ/O သည်/E
ဂင်မ်/O ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/O တယ်/E
အ/O အေး/O မိ/O မယ်/E
ဧည့်/O လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/O လို့/O ရ/O လား/E
မှန်/O တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/O ရင်း/O ကောက်/O မော့/O လိုက်/O သည်/E ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/O လိုက်/O ရ/O သည်/E

==> MLP.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E
ဈေး/O က/O များ/O လှ/O ချေ/E လား/E
သူ/O ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/E ထင်/N တယ်/E
ဘာ/O ကြောင့်/O လဲ/E ဆို/O စမ်း/O ပါ/N ဦး/O
စိတ်/O ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/N ပြန်/O ပြီ/E
၁/O ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/B ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/E တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/N ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/N ခြင်း/O ဖြစ်/O သည်/E ဟု/O တွေး/O ယူ/O ခဲ့/N ဖူး/O လေ/O သည်/E
ဂင်မ်/O ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/N တယ်/E
အ/O အေး/O မိ/O မယ်/E
ဧည့်/O လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/N လို့/O ရ/O လား/E
မှန်/O တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/N ရင်း/O ကောက်/O မော့/O လိုက်/N သည်/E ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/O လိုက်/N ရ/O သည်/E

==> Random-Forest.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E
ဈေး/O က/O များ/O လှ/O ချေ/E လား/E
သူ/O ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/E ထင်/N တယ်/E
ဘာ/O ကြောင့်/O လဲ/E ဆို/O စမ်း/O ပါ/N ဦး/O
စိတ်/O ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/N ပြန်/O ပြီ/E
၁/O ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/B ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/E တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/N ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/N ခြင်း/O ဖြစ်/O သည်/E ဟု/O တွေး/O ယူ/O ခဲ့/N ဖူး/O လေ/O သည်/E
ဂင်မ်/O ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/N တယ်/E
အ/O အေး/O မိ/O မယ်/E
ဧည့်/O လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/N လို့/O ရ/O လား/E
မှန်/O တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/N ရင်း/O ကောက်/O မော့/O လိုက်/N သည်/E ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/O လိုက်/N ရ/O သည်/E

==> Voting.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E
ဈေး/O က/O များ/O လှ/O ချေ/E လား/E
သူ/O ဒီ/O နေ့/O နည်း/O နည်း/O ပင်/O ပန်း/O နေ/O တယ်/E ထင်/N တယ်/E
ဘာ/O ကြောင့်/O လဲ/E ဆို/O စမ်း/O ပါ/N ဦး/O
စိတ်/O ကောက်/O တဲ့/O စ/O ကား/O မျိုး/O ပြော/N ပြန်/O ပြီ/E
၁/O ၆/O ရာ/O စု/O နှစ်/O တွင်/O ရော/O မ/O ပန်း/O ချီ/O ကျော်/O က/O ဝိ/O လီ/O ယို/O နာ/O ဒို/O ဒါ/B ဗင်း/O ချိ/O က/O ပင်/O လယ်/O ခ/O ရု/O များ/O ရှိ/O ရာ/O လက်/O ရှိ/O ကုန်း/O မြင့်/O များ/O သည်/E တစ်/O ကြိမ်/O က/O ပင်/O လယ်/O အောက်/O တွင်/O ရှိ/O ခဲ့/N ၍/O နောက်/O မှ/O မြေ/O မြင့်/O တက်/O လာ/O ခဲ့/N ခြင်း/O ဖြစ်/O သည်/E ဟု/O တွေး/O ယူ/O ခဲ့/N ဖူး/O လေ/O သည်/E
ဂင်မ်/O ချီ/O သိပ်/O ပြီး/O နောက်/O ဂင်မ်/O ချီ/O အိုး/O ကို/O မြေ/O ကြီး/O ထဲ/O မြုပ်/O လိုက်/N တယ်/E
အ/O အေး/O မိ/O မယ်/E
ဧည့်/O လမ်း/O ညွှန်/O ရော/O ထည့်/O ပေး/N လို့/O ရ/O လား/E
မှန်/O တင်/O ခုံ/O ဘေး/O က/O အ/O ရက်/O ပု/O လင်း/O ကို/O ထုတ်/O ယူ/O လိုက်/N ရင်း/O ကောက်/O မော့/O လိုက်/N သည်/E ပု/O လင်း/O ပြန်/O အ/O သိမ်း/O မှာ/O အ/O ပြာ/O ရောင်/O ဝတ်/O စုံ/O ကို/O မြင်/O လိုက်/N ရ/O သည်/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$

```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ sentence breaking ကိစ္စမှာ ဆိုရင် CRF မော်ဒယ် ကလွဲရင် ကျန်တဲ့ ML model အများစုက \E tag ကို ခန့်မှန်းပေးနိုင်ပေမဲ့ စာကြောင်းအစဖြစ်တဲ့ \B ကို လုံးဝ မခန့်မှန်းနိုင်ကြဘူး။ အဲဒါကိုတော့ မော်ဒယ်နှစ်ခု ထပ်ပြီး error-correction လုပ်ရင် ရလဒ်က ပိုကောင်းလာမယ်လို့ ယူဆတယ်။  

N ကိုပါ လုပ်ပေးနိုင်ရင် ရလဒ်က တော်တော်တက်လာမယ်။  

## Preparing tag-tag training/testing data  

tag input, tag output မော်ဒယ်ဆောက်ဖို့အတွက် ဒေတာ အရင်ပြင်ဆင်ရမယ်။  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy  



```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <folder_path> <file_extension>"
    exit 1
fi

# Assign arguments to variables
FOLDER_PATH=$1
FILE_EXTENSION=$2

# Check if the folder exists
if [ ! -d "$FOLDER_PATH" ]; then
    echo "Error: Folder $FOLDER_PATH does not exist."
    exit 1
fi

# Process files with the specified extension in the folder
for FILE in "$FOLDER_PATH"/*."$FILE_EXTENSION"; do
    # Check if the file exists
    if [ -f "$FILE" ]; then
        OUTPUT_FILE="${FILE}.tag"
        echo "Processing: $FILE -> $OUTPUT_FILE"
        ./mk-wordtag.pl "$FILE" "\\/" t > "$OUTPUT_FILE"
    else
        echo "No files with extension .$FILE_EXTENSION found in $FOLDER_PATH."
    fi
done


```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./prepare-traindata-tags.sh ./models/fasttext/dummy/ hyp
Processing: ./models/fasttext/dummy//AdaBoost.train.hyp -> ./models/fasttext/dummy//AdaBoost.train.hyp.tag
Processing: ./models/fasttext/dummy//CRF.train.hyp -> ./models/fasttext/dummy//CRF.train.hyp.tag
Processing: ./models/fasttext/dummy//Decision-Tree.train.hyp -> ./models/fasttext/dummy//Decision-Tree.train.hyp.tag
Processing: ./models/fasttext/dummy//GradientBoosting.train.hyp -> ./models/fasttext/dummy//GradientBoosting.train.hyp.tag
Processing: ./models/fasttext/dummy//Logistic-Regression.train.hyp -> ./models/fasttext/dummy//Logistic-Regression.train.hyp.tag
Processing: ./models/fasttext/dummy//MLP.train.hyp -> ./models/fasttext/dummy//MLP.train.hyp.tag
Processing: ./models/fasttext/dummy//Random-Forest.train.hyp -> ./models/fasttext/dummy//Random-Forest.train.hyp.tag
Processing: ./models/fasttext/dummy//Voting.train.hyp -> ./models/fasttext/dummy//Voting.train.hyp.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Check output files:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ wc *.tag
   50081  1334843  2669686 AdaBoost.train.hyp.tag
   50081  1334843  2669686 CRF.train.hyp.tag
   50081  1334843  2669686 Decision-Tree.train.hyp.tag
   50081  1334843  2669686 GradientBoosting.train.hyp.tag
   50081  1334843  2669686 Logistic-Regression.train.hyp.tag
   50081  1334843  2669686 MLP.train.hyp.tag
   50081  1334843  2669686 Random-Forest.train.hyp.tag
   50081  1334843  2669686 Voting.train.hyp.tag
  400648 10678744 21357488 total
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ head CRF.train.hyp.tag
B N N E
B O O O N E
B O O O O O O O O N E
B O O O O N E
B O O O O O N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N N E
B O O O O O O O O O O O O N E
B N N E
B O O O N N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ head ./MLP.train.hyp.tag
O O N E
O O O O E E
O O O O O O O O E N E
O O E O O N O
O O O O O O N O E
O O O O O O O O O O O O O O O O O B O O O O O O O O O O O O O O O E O O O O O O O O N O O O O O O O N O O E O O O N O O E
O O O O O O O O O O O O O N E
O O O E
O O O O O N O O E
O O O O O O O O O O O O N O O O N E O O O O O O O O O O O O O N O E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ head Random-Forest.train.hyp.tag
O O N E
O O O O E E
O O O O O O O O E N E
O O E O O N O
O O O O O O N O E
O O O O O O O O O O O O O O O O O B O O O O O O O O O O O O O O O E O O O O O O O O N O O O O O O O N O O E O O O N O O E
O O O O O O O O O O O O O N E
O O O E
O O O O O N O O E
O O O O O O O O O O O O N O O O N E O O O O O O O O O O O O O N O E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$
```

## Prepare Reference Tags  

Training ဖိုင်ကနေ reference tag တွေပဲ ဆွဲထုတ်...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ perl ./mk-wordtag.pl ./data/syl/bone/train-valid.tagged.bone "\/" t > ./models/fasttext/dummy/train-valid.tagged.bone.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

check filesize:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ wc train-valid.tagged.bone.tag
  50081 1334843 2669686 train-valid.tagged.bone.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$
```

check output tags ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ head train-valid.tagged.bone.tag
B N N E
B O N N N E
B O O O O O O N N N E
B O O N N N E
B O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O O O O O O N N N E
B N N E
B O O O O N N N E
B O O O O O O O O O O O O O N N N E B O O O O O O O O O O O N N N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$
```

Make reference tag for test data:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ perl ./mk-wordtag.pl ./data/syl/bone/test.tagged.bone "\/" t > ./models/fasttext/dummy/test.tagged.bone.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Check filesize:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ wc ./test.tagged.bone.tag
  5512 143773 287546 ./test.tagged.bone.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ head ./test.tagged.bone.tag
B O O O O N N N E
B O N N N E
B O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O N N N E
B O O O O N N N E
B O O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O N N N E
```

## Make Pair for Tag-Tag Training Process  

လုပ်ရမှာက အောက်ပါအတိုင်း ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ perl ./mk-pair.pl ./models/fasttext/dummy/CRF.train.hyp.tag ./models/fasttext/dummy/train-valid.tagged.bone.tag > ./models/fasttext/dummy/CRF.tag.pair
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./models/fasttext/dummy/CRF.tag.pair
B/B N/N N/N E/E
B/B O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B N/N N/N E/E
B/B O/O O/O O/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N O/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

writing a shell script:  

```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [ "$#" -ne 2 ]; then
    echo "Usage: $0 <folder_path> <file_extension>"
    exit 1
fi

# Assign arguments to variables
FOLDER_PATH=$1
FILE_EXTENSION=$2

# Check if the folder exists
if [ ! -d "$FOLDER_PATH" ]; then
    echo "Error: Folder $FOLDER_PATH does not exist."
    exit 1
fi

# Process files with the specified extension in the folder
for FILE in "$FOLDER_PATH"/*."$FILE_EXTENSION"; do
    # Check if the file exists
    if [ -f "$FILE" ]; then
        OUTPUT_FILE="${FILE}.tag"
        echo "Processing: $FILE -> $OUTPUT_FILE"
        perl ./mk-wordtag.pl "$FILE" "\\/" t > "$OUTPUT_FILE"
    else
        echo "No files with extension .$FILE_EXTENSION found in $FOLDER_PATH."
    fi
done

```

```
perl ./mk-pair.pl ./models/fasttext/dummy/CRF.train.hyp.tag ./models/fasttext/dummy/train-valid.tagged.bone.tag > ./models/fasttext/dummy/CRF.tag.pair

(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ls ./models/fasttext/dummy/*.hyp.tag
./models/fasttext/dummy/AdaBoost.train.hyp.tag
./models/fasttext/dummy/CRF.train.hyp.tag
./models/fasttext/dummy/Decision-Tree.train.hyp.tag
./models/fasttext/dummy/GradientBoosting.train.hyp.tag
./models/fasttext/dummy/Logistic-Regression.train.hyp.tag
./models/fasttext/dummy/MLP.train.hyp.tag
./models/fasttext/dummy/Random-Forest.train.hyp.tag
./models/fasttext/dummy/Voting.train.hyp.tag
```

shell script ပြင်ဆင်...  

```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <folder_path> <input_extension> <output_extension> <reference_file>"
    exit 1
fi

# Assign arguments to variables
FOLDER_PATH=$1
INPUT_EXTENSION=$2
OUTPUT_EXTENSION=$3
REFERENCE_FILE=$4

# Check if the folder exists
if [ ! -d "$FOLDER_PATH" ]; then
    echo "Error: Folder $FOLDER_PATH does not exist."
    exit 1
fi

# Check if the reference file exists
if [ ! -f "$REFERENCE_FILE" ]; then
    echo "Error: Reference file $REFERENCE_FILE does not exist."
    exit 1
fi

# Process files with the specified input extension in the folder
for FILE in "$FOLDER_PATH"/*."$INPUT_EXTENSION"; do
    # Check if the file exists
    if [ -f "$FILE" ]; then
        OUTPUT_FILE="${FILE%.$INPUT_EXTENSION}.$OUTPUT_EXTENSION"
        echo "Processing: $FILE -> $OUTPUT_FILE"
        perl ./mk-pair.pl "$FILE" "$REFERENCE_FILE" > "$OUTPUT_FILE"
    else
        echo "No files with extension .$INPUT_EXTENSION found in $FOLDER_PATH."
    fi
done

```

Running the shell script ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ chmod +x make-pair.sh
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./make-pair.sh ./models/fasttext/dummy/ hyp.tag tag.pair ./models/fasttext/dummy/train-valid.tagged.bone.tag
Processing: ./models/fasttext/dummy//AdaBoost.train.hyp.tag -> ./models/fasttext/dummy//AdaBoost.train.tag.pair
Processing: ./models/fasttext/dummy//CRF.train.hyp.tag -> ./models/fasttext/dummy//CRF.train.tag.pair
Processing: ./models/fasttext/dummy//Decision-Tree.train.hyp.tag -> ./models/fasttext/dummy//Decision-Tree.train.tag.pair
Processing: ./models/fasttext/dummy//GradientBoosting.train.hyp.tag -> ./models/fasttext/dummy//GradientBoosting.train.tag.pair
Processing: ./models/fasttext/dummy//Logistic-Regression.train.hyp.tag -> ./models/fasttext/dummy//Logistic-Regression.train.tag.pair
Processing: ./models/fasttext/dummy//MLP.train.hyp.tag -> ./models/fasttext/dummy//MLP.train.tag.pair
Processing: ./models/fasttext/dummy//Random-Forest.train.hyp.tag -> ./models/fasttext/dummy//Random-Forest.train.tag.pair
Processing: ./models/fasttext/dummy//Voting.train.hyp.tag -> ./models/fasttext/dummy//Voting.train.tag.pair
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Check output files ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ head *.tag.pair
==> AdaBoost.train.tag.pair <==
O/B O/N N/N O/E
O/B O/O O/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/N E/N O/N E/E
O/B O/O E/O O/N O/N N/N O/E
O/B O/O O/O O/O O/O O/N O/N O/N O/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E
O/B O/N O/N O/E
O/B O/O O/O O/O O/O O/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E

==> CRF.train.tag.pair <==
B/B N/N N/N E/E
B/B O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B N/N N/N E/E
B/B O/O O/O O/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N O/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N N/N E/E

==> Decision-Tree.train.tag.pair <==
O/B O/N N/N E/E
O/B O/O O/N O/N E/N E/E
O/B O/O O/O O/O O/O O/O O/O O/N E/N N/N E/E
O/B O/O E/O O/N O/N N/N O/E
O/B O/O O/O O/O O/O O/N N/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O B/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O E/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
O/B O/N O/N E/E
O/B O/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/N O/N N/N E/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N O/N E/E

==> GradientBoosting.train.tag.pair <==
O/B O/N N/N E/E
O/B O/O O/N O/N E/N E/E
O/B O/O O/O O/O O/O O/O O/O O/N E/N O/N E/E
O/B O/O E/O O/N O/N N/N O/E
O/B O/O O/O O/O O/O O/N N/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O B/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O E/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E
O/B O/N O/N E/E
O/B O/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E

==> Logistic-Regression.train.tag.pair <==
O/B O/N N/N O/E
O/B O/O O/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/N E/N N/N E/E
O/B O/O E/O O/N O/N N/N O/E
O/B O/O O/O O/O O/O O/N N/N O/N O/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O E/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E
O/B O/N O/N E/E
O/B O/O O/O O/O O/O O/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E

==> MLP.train.tag.pair <==
O/B O/N N/N E/E
O/B O/O O/N O/N E/N E/E
O/B O/O O/O O/O O/O O/O O/O O/N E/N N/N E/E
O/B O/O E/O O/N O/N N/N O/E
O/B O/O O/O O/O O/O O/N N/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O B/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O E/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
O/B O/N O/N E/E
O/B O/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/N O/N N/N E/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N O/N E/E

==> Random-Forest.train.tag.pair <==
O/B O/N N/N E/E
O/B O/O O/N O/N E/N E/E
O/B O/O O/O O/O O/O O/O O/O O/N E/N N/N E/E
O/B O/O E/O O/N O/N N/N O/E
O/B O/O O/O O/O O/O O/N N/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O B/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O E/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
O/B O/N O/N E/E
O/B O/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/N O/N N/N E/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N O/N E/E

==> Voting.train.tag.pair <==
O/B O/N N/N E/E
O/B O/O O/N O/N E/N E/E
O/B O/O O/O O/O O/O O/O O/O O/N E/N N/N E/E
O/B O/O E/O O/N O/N N/N O/E
O/B O/O O/O O/O O/O O/N N/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O B/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/O E/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
O/B O/N O/N E/E
O/B O/O O/O O/O O/O N/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O O/O O/N O/N N/N E/E O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N O/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$

```

tag-tag training data ပြင်ဆင်တာ ပြီး။  

## Train ML-Models with Tag-Tag Dataset

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy$ wc *.tag.pair
   50081  1334843  5339372 AdaBoost.train.tag.pair
   50081  1334843  5339372 CRF.train.tag.pair
   50081  1334843  5339372 Decision-Tree.train.tag.pair
   50081  1334843  5339372 GradientBoosting.train.tag.pair
   50081  1334843  5339372 Logistic-Regression.train.tag.pair
   50081  1334843  5339372 MLP.train.tag.pair
   50081  1334843  5339372 Random-Forest.train.tag.pair
   50081  1334843  5339372 Voting.train.tag.pair
  400648 10678744 42714976 total
```

prepare a new shell script for training tat-tag models ...  
ဒီတခါတော့ training data က ၈ ဖိုင် ရှိသွားလိမ့်မယ်။ 
တကယ်က အကောင်းဆုံး မော်ဒယ်က CRF ပဲမို့လို့ CRF မော်ဒယ်က ထွက်လာတဲ့ prediction tag တွေကိုပဲ ပြင်တာက ရလဒ်ပိုကောင်းနိုင်တယ်။  
Experiment အနေနဲ့ကတော့ အားလုံးကို လုပ်ကြည့်ခြင်းအားဖြင့် ML model stacking က ဘယ်လောက် အလုပ်လုပ်ပေးတယ်ဆိုတာကိုတော့ မော်ဒယ် တစ်ခုချင်းစီအတွက် ရလဒ်ထွက်လာလိမ့်မယ်။  

baseline ရော error-correction ရောကို မော်ဒယ် မကစားတော့ပဲ အတူတူထားသွားမယ်။ အဲဒါကြောင့် run မယ့် ပုံစံက အောက်ပါအတိုင်း ဖြစ်လိမ့်မယ်။  

Adaboost-Adaboost  
CRF-CRF  
DecisionTree-DecisionTree
GB-GB  
LR-LR    
MLP-MLP  
RF-RF  
Voting-Voting  

Training Data Path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy  

Python Program Path:
/home/ye/data/hello-sayarwon/coding/model-based   

ft-model Path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/fasttext-features.bin   

time python ./fasttext-ml.version2.py --train "$TRAIN_FILE" --ft-model "$FT_MODEL" --model "$MODEL_FILE" --method "$METHOD"  

Output Model Path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models  

time python ./fasttext-ml.version2.py --train /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/AdaBoost.train.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/fasttext-features.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/AdaBoost.tag.model --method AdaBoost  

time python ./fasttext-ml.version2.py --train /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/CRF.train.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/fasttext-features.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.tag.model --method CRF  


```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [ "$#" -ne 4 ]; then
    echo "Usage: $0 <training_data_path> <training_file_extension> <ft_model_path> <output_model_path>"
    exit 1
fi

# Assign arguments to variables
TRAINING_DATA_PATH=$1
TRAINING_FILE_EXTENSION=$2
FT_MODEL_PATH=$3
OUTPUT_MODEL_PATH=$4

# Check if the training data path exists
if [ ! -d "$TRAINING_DATA_PATH" ]; then
    echo "Error: Training data path $TRAINING_DATA_PATH does not exist."
    exit 1
fi

# Check if the ft-model file exists
if [ ! -f "$FT_MODEL_PATH" ]; then
    echo "Error: ft-model file $FT_MODEL_PATH does not exist."
    exit 1
fi

# Create the output model path if it does not exist
if [ ! -d "$OUTPUT_MODEL_PATH" ]; then
    mkdir -p "$OUTPUT_MODEL_PATH"
fi

# Loop through files with the specified extension in the training data path
for FILE in "$TRAINING_DATA_PATH"/*."$TRAINING_FILE_EXTENSION"; do
    if [ -f "$FILE" ]; then
        # Extract the method name from the file name
        BASENAME=$(basename "$FILE")
        METHOD_NAME=$(echo "$BASENAME" | cut -d'.' -f1)
        
        # Construct the output model file name
        OUTPUT_MODEL_FILE="$OUTPUT_MODEL_PATH/$METHOD_NAME.tag.model"
        
        # Run the Python script
        echo "Running: time python ./fasttext-ml.version2.py --train $FILE --ft-model $FT_MODEL_PATH --model $OUTPUT_MODEL_FILE --method $METHOD_NAME"
        time python ./fasttext-ml.version2.py --train "$FILE" --ft-model "$FT_MODEL_PATH" --model "$OUTPUT_MODEL_FILE" --method "$METHOD_NAME"
    else
        echo "No files with extension .$TRAINING_FILE_EXTENSION found in $TRAINING_DATA_PATH."
    fi
done

```

ပြဿနာက လက်ရှိ training data မှာက tag/tag ဖြစ်ပြီး ပထမ tag တွေက model တစ်မျိုးစီရဲ့ 1st prediction ရလဒ်တွေမို့လို့ မှားတာတွေလည်း ရှိတယ်။ အဲဒါကြောင့် reference tag နဲ့ပဲ tag-fasttext model ကို ပြင်ပြီး run တာက ပိုသဘာဝကျလိမ့်မယ်။  

Build error-correction models ...  
*** သတိထားရမှာက feature က အသစ်ဆောက်မှ ရလိမ့်မယ်။ fasttext model path ကို မပေးမိအောင် သတိထားရမယ်။ fasttext_model.bin ကလည်း လက်ရှိ python script ကို run တဲ့ path အောက်မှာ ရှိမနေဖို့ အရေးကြီးတယ်။   

အထက်က bash shell script မှာ --ft-model နဲ့ ဆိုင်တာတွေကို ဖြုတ်တာ လုပ်ခဲ့တယ်။ updated bash shell script က အောက်ပါအတိုင်း...  

```bash
#!/bin/bash

# Check if the correct number of arguments is provided
if [ "$#" -ne 3 ]; then
    echo "Usage: $0 <training_data_path> <training_file_extension> <output_model_path>"
    exit 1
fi

# Assign arguments to variables
TRAINING_DATA_PATH=$1
TRAINING_FILE_EXTENSION=$2
OUTPUT_MODEL_PATH=$3

# Check if the training data path exists
if [ ! -d "$TRAINING_DATA_PATH" ]; then
    echo "Error: Training data path $TRAINING_DATA_PATH does not exist."
    exit 1
fi

# Create the output model path if it does not exist
if [ ! -d "$OUTPUT_MODEL_PATH" ]; then
    mkdir -p "$OUTPUT_MODEL_PATH"
fi

# Loop through files with the specified extension in the training data path
for FILE in "$TRAINING_DATA_PATH"/*."$TRAINING_FILE_EXTENSION"; do
    if [ -f "$FILE" ]; then
        # Extract the method name from the file name
        BASENAME=$(basename "$FILE")
        METHOD_NAME=$(echo "$BASENAME" | cut -d'.' -f1)
        
        # Construct the output model file name
        OUTPUT_MODEL_FILE="$OUTPUT_MODEL_PATH/$METHOD_NAME.tag.model"
        
        # Run the Python script
        echo "Running: time python ./fasttext-ml.version2.py --train $FILE --model $OUTPUT_MODEL_FILE --method $METHOD_NAME"
        time python ./fasttext-ml.version2.py --train "$FILE" --model "$OUTPUT_MODEL_FILE" --method "$METHOD_NAME"
    else
        echo "No files with extension .$TRAINING_FILE_EXTENSION found in $TRAINING_DATA_PATH."
    fi
done
```

## Building a Tag Fasttext Model 

```python
import argparse
import fasttext
import logging
import os

def train_fasttext_model(input_file, output_file, model_type, dim, epoch, lr, ws, logger):
    """Train and save a FastText model."""
    if not os.path.exists(input_file):
        logger.error(f"Input file '{input_file}' does not exist.")
        raise FileNotFoundError(f"Input file '{input_file}' does not exist.")

    logger.info(f"Starting FastText model training with model_type={model_type}, dim={dim}, epoch={epoch}, lr={lr}, ws={ws}...")

    model = fasttext.train_unsupervised(
        input=input_file,
        model=model_type,
        dim=dim,
        epoch=epoch,
        lr=lr,
        ws=ws
    )

    logger.info(f"Saving FastText model to '{output_file}'...")
    model.save_model(output_file)
    logger.info("FastText model training completed successfully.")

def main():
    parser = argparse.ArgumentParser(description="Build a FastText model from word-segmented text.")
    parser.add_argument("--input", required=True, help="Path to the training text file (word-segmented UTF-8).")
    parser.add_argument("--output", default="fasttext_model.bin", help="Filename for saving the FastText model (default: fasttext_model.bin).")
    parser.add_argument("--model", choices=["skipgram", "cbow"], default="skipgram", help="Model type: skipgram or cbow (default: skipgram).")
    parser.add_argument("--dim", type=int, default=100, help="Dimensionality of word vectors (default: 100).")
    parser.add_argument("--epoch", type=int, default=5, help="Number of epochs (default: 5).")
    parser.add_argument("--lr", type=float, default=0.05, help="Learning rate (default: 0.05).")
    parser.add_argument("--ws", type=int, default=5, help="Context window size (default: 5).")

    args = parser.parse_args()

    logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(message)s")
    logger = logging.getLogger()

    try:
        train_fasttext_model(
            input_file=args.input,
            output_file=args.output,
            model_type=args.model,
            dim=args.dim,
            epoch=args.epoch,
            lr=args.lr,
            ws=args.ws,
            logger=logger
        )
    except Exception as e:
        logger.error(f"An error occurred: {e}")

if __name__ == "__main__":
    main()

```


call help ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./build-fasttext-model.py --help
usage: build-fasttext-model.py [-h] --input INPUT [--output OUTPUT] [--model {skipgram,cbow}]
                               [--dim DIM] [--epoch EPOCH] [--lr LR] [--ws WS]

Build a FastText model from word-segmented text.

options:
  -h, --help            show this help message and exit
  --input INPUT         Path to the training text file (word-segmented UTF-8).
  --output OUTPUT       Filename for saving the FastText model (default: fasttext_model.bin).
  --model {skipgram,cbow}
                        Model type: skipgram or cbow (default: skipgram).
  --dim DIM             Dimensionality of word vectors (default: 100).
  --epoch EPOCH         Number of epochs (default: 5).
  --lr LR               Learning rate (default: 0.05).
  --ws WS               Context window size (default: 5).
```

reference tag ဖိုင်ကို ပြင်ဆင် ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ perl ./mk-wordtag.pl ./data/syl/bone/train-valid.tagged.bone "\/" t >  ./data/syl/bone/train-valid.tagged.bone.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./data/syl/bone/train-valid.tagged.bone.tag
  50081 1334843 2669686 ./data/syl/bone/train-valid.tagged.bone.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./data/syl/bone/train-
valid.tagged.bone.tag
B N N E
B O N N N E
B O O O O O O N N N E
B O O N N N E
B O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O O O O O O N N N E
B N N E
B O O O O N N N E
B O O O O O O O O O O O O O N N N E B O O O O O O O O O O O N N N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Building tag fasttext feature file ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./build-fasttext-model.py --input ./data/syl/bone/train-valid.tagged.bone.tag --output ./tag.fasttext.model.bin
2024-12-15 17:11:03,866 - Starting FastText model training with model_type=skipgram, dim=100, epoch=5, lr=0.05, ws=5...
Read 1M words
Number of words:  5
Number of labels: 0
Progress: 100.0% words/sec/thread: 1097064 lr:  0.000000 avg.loss:  2.428067 ETA:   0h 0m 0s
2024-12-15 17:11:04,976 - Saving FastText model to './tag.fasttext.model.bin'...
2024-12-15 17:11:05,562 - FastText model training completed successfully.

real    0m1.935s
user    0m7.686s
sys     0m2.896s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Tag တွေနဲ့ ဆောက်ထားတဲ့ fasttext model က အောက်ပါအတိုင်း...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ll -h ./tag.fasttext.model.bin
-rw-rw-r-- 1 ye ye 763M Dec 15 17:11 ./tag.fasttext.model.bin
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

## Training Tag-Tag or Correction Model

bash script ကို update လုပ်ခဲ့ပေမဲ့ တကယ်တမ်း သုံးဖြစ်တာက ပထမ bash script ပဲ။ ဆိုလိုတာက --ft-model ကိုပဲ assign လုပ်ပြီး run တဲ့ bash script ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./build-2nd-models.sh ./models/fasttext/dummy/ train.tag.pair ./tag.fasttext.model.bin /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models | tee build-2nd-models.log

```

training log ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./build-2nd-models.sh ./models/fasttext/dummy/ train.tag.pair ./tag.fasttext.model.bin /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models | tee build-2nd-models.log
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//AdaBoost.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/AdaBoost.tag.model --method AdaBoost
2024-12-15 17:17:51,982 - Loading training data for AdaBoost...
2024-12-15 17:17:52,416 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 17:17:53,144 - Preparing features for AdaBoost...
2024-12-15 17:18:00,517 - Training AdaBoost model...
/home/ye/.local/lib/python3.10/site-packages/sklearn/ensemble/_weight_boosting.py:519: FutureWarning: The SAMME.R algorithm (the default) is deprecated and will be removed in 1.6. Use the SAMME algorithm to circumvent this warning.
  warnings.warn(
2024-12-15 17:20:05,647 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/AdaBoost.tag.model...
2024-12-15 17:20:05,740 - Training for AdaBoost completed.

real    2m15.062s
user    2m14.674s
sys     0m7.299s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//CRF.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.tag.model --method CRF
2024-12-15 17:20:07,042 - Loading training data for CRF...
2024-12-15 17:20:07,477 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 17:20:08,254 - Preparing features for CRF...
2024-12-15 17:21:13,779 - Training CRF model...
2024-12-15 17:26:21,312 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.tag.model...
2024-12-15 17:26:21,332 - Training for CRF completed.

real    6m24.317s
user    6m9.599s
sys     0m21.591s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//Decision-Tree.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Decision-Tree.tag.model --method Decision-Tree
2024-12-15 17:26:31,365 - Loading training data for Decision-Tree...
2024-12-15 17:26:31,800 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 17:26:32,530 - Preparing features for Decision-Tree...
2024-12-15 17:26:39,746 - Training Decision-Tree model...
2024-12-15 17:26:45,977 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Decision-Tree.tag.model...
2024-12-15 17:26:45,978 - Training for Decision-Tree completed.

real    0m15.865s
user    0m17.902s
sys     0m4.893s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//GradientBoosting.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/GradientBoosting.tag.model --method GradientBoosting
2024-12-15 17:26:47,233 - Loading training data for GradientBoosting...
2024-12-15 17:26:47,670 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 17:26:48,401 - Preparing features for GradientBoosting...
2024-12-15 17:26:55,945 - Training GradientBoosting model...


2024-12-15 18:02:04,476 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/GradientBoosting.tag.model...
2024-12-15 18:02:04,562 - Training for GradientBoosting completed.

real    35m18.633s
user    35m8.837s
sys     0m16.287s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//Logistic-Regression.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Logistic-Regression.tag.model --method Logistic-Regression
2024-12-15 18:02:05,866 - Loading training data for Logistic-Regression...
2024-12-15 18:02:06,308 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 18:02:07,038 - Preparing features for Logistic-Regression...
2024-12-15 18:02:14,504 - Training Logistic-Regression model...
2024-12-15 18:02:35,406 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Logistic-Regression.tag.model...
2024-12-15 18:02:35,409 - Training for Logistic-Regression completed.

real    0m30.953s
user    6m21.682s
sys     2m32.794s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//MLP.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/MLP.tag.model --method MLP
2024-12-15 18:02:36,822 - Loading training data for MLP...
2024-12-15 18:02:37,258 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 18:02:37,989 - Preparing features for MLP...
2024-12-15 18:02:45,548 - Training MLP model...
2024-12-15 18:12:54,276 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/MLP.tag.model...
2024-12-15 18:12:54,392 - Training for MLP completed.

real    10m18.884s
user    195m27.380s
sys     126m38.587s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//Random-Forest.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Random-Forest.tag.model --method Random-Forest
2024-12-15 18:12:55,752 - Loading training data for Random-Forest...
2024-12-15 18:12:56,189 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 18:12:56,903 - Preparing features for Random-Forest...
2024-12-15 18:13:04,584 - Training Random-Forest model...
2024-12-15 18:15:20,608 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Random-Forest.tag.model...
2024-12-15 18:15:20,751 - Training for Random-Forest completed.

real    2m26.339s
user    2m25.204s
sys     0m7.860s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/dummy//Voting.train.tag.pair --ft-model ./tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Voting.tag.model --method Voting
2024-12-15 18:15:22,046 - Loading training data for Voting...
2024-12-15 18:15:22,481 - Loading existing FastText model from ./tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 18:15:23,195 - Preparing features for Voting...
2024-12-15 18:15:30,805 - Training Voting model...
2024-12-15 18:18:13,449 - Saving trained model to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Voting.tag.model...
2024-12-15 18:18:13,556 - Training for Voting completed.

real    2m52.667s
user    8m8.613s
sys     2m29.966s

real    60m22.747s
user    256m13.917s
sys     132m39.286s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
(

```

Check trained model file:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ ll -h *.model
-rw-rw-r-- 1 ye ye  36K Dec 15 17:20 AdaBoost.tag.model
-rw-rw-r-- 1 ye ye  47K Dec 15 17:26 CRF.tag.model
-rw-rw-r-- 1 ye ye 2.0K Dec 15 17:26 Decision-Tree.tag.model
-rw-rw-r-- 1 ye ye 422K Dec 15 18:02 GradientBoosting.tag.model
-rw-rw-r-- 1 ye ye 4.0K Dec 15 18:02 Logistic-Regression.tag.model
-rw-rw-r-- 1 ye ye 252K Dec 15 18:12 MLP.tag.model
-rw-rw-r-- 1 ye ye 107K Dec 15 18:15 Random-Forest.tag.model
-rw-rw-r-- 1 ye ye 112K Dec 15 18:18 Voting.tag.model
```

## During Training, Only Testing for CRF-CRF  

test data path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext  

fasttext model path:  
/home/ye/data/hello-sayarwon/coding/model-based/

CRF model path:
./models/fasttext/dummy/models


ပြန်ဖတ်ကြည့်တော့ တကယ်က prepare-traindata-tags.sh က folder path နဲ့ extension ပေးယုံနဲ့ tag ဖိုင်တွေကို ထုတ်ဖို့ အသုံးဝင်တာမို့လို့ ဖိုင်နာမည်ကို extract-tag.sh လိုပြောင်းခဲ့...  
 
```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ mv prepare-traindata-tags.sh extract-tag.sh
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

1st model က ထွက်ထားတဲ့ hyp ဖိုင်တွေမှာက word/tag ပုံစံမို့လို့ အဲဒီကနေ tag တွေပဲ ဆွဲထုတ်ယူခဲ့...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./extract-tag.sh ./models/fas
ttext/ hyp
Processing: ./models/fasttext//AdaBoost.hyp -> ./models/fasttext//AdaBoost.hyp.tag
Processing: ./models/fasttext//CRF.hyp -> ./models/fasttext//CRF.hyp.tag
Processing: ./models/fasttext//Decision-Tree.hyp -> ./models/fasttext//Decision-Tree.hyp.tag
Processing: ./models/fasttext//GradientBoosting.hyp -> ./models/fasttext//GradientBoosting.hyp.tag
Processing: ./models/fasttext//Logistic-Regression.hyp -> ./models/fasttext//Logistic-Regression.hyp.tag
Processing: ./models/fasttext//MLP.hyp -> ./models/fasttext//MLP.hyp.tag
Processing: ./models/fasttext//Random-Forest.hyp -> ./models/fasttext//Random-Forest.hyp.tag
Processing: ./models/fasttext//Voting.hyp -> ./models/fasttext//Voting.hyp.tag

real    0m2.731s
user    0m2.695s
sys     0m0.036s
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

ဆွဲထုတ်ထားတဲ့ tag ဖိုင်တွေ ကို စစ်ဆေး...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ wc *.hyp.tag
   5512  143773  287546 AdaBoost.hyp.tag
   5512  143773  287546 CRF.hyp.tag
   5512  143773  287546 Decision-Tree.hyp.tag
   5512  143773  287546 GradientBoosting.hyp.tag
   5512  143773  287546 Logistic-Regression.hyp.tag
   5512  143773  287546 MLP.hyp.tag
   5512  143773  287546 Random-Forest.hyp.tag
   5512  143773  287546 Voting.hyp.tag
  44096 1150184 2300368 total
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ head CRF.hyp.tag
B O O O O O O N E
B N N N N E
B O O O O O O O N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N E
B O O O O O O O O O N N E
B O O O O O O O O O O O O O O O O O O O O N E
B O O O O O O N E
B O O O O O O O O O N E
B O O O O O O O O O O O O O O O O O N N N N N N E
B O O O O N N N N E
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$
```

Reference test-data tag ဖိုင်ကို ပြင်ဆင်...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ perl ./mk-wordtag.pl ./data/syl/bone/test.tagged.bone "\/" t > ./data/syl/bone/test.tagged.bone.tag
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

check ...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./data/syl/bone/test.tagged.bone.tag
B O O O O N N N E
B O N N N E
B O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O N N N E
B O O O O N N N E
B O O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O N N N E
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

make pair လုပ်ခဲ့...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./make-pair.sh ./models/fasttext/ hyp.tag tag.pair ./data/syl/bone/test.tagged.bone.tag
Processing: ./models/fasttext//AdaBoost.hyp.tag -> ./models/fasttext//AdaBoost.tag.pair
Processing: ./models/fasttext//CRF.hyp.tag -> ./models/fasttext//CRF.tag.pair
Processing: ./models/fasttext//Decision-Tree.hyp.tag -> ./models/fasttext//Decision-Tree.tag.pair
Processing: ./models/fasttext//GradientBoosting.hyp.tag -> ./models/fasttext//GradientBoosting.tag.pair
Processing: ./models/fasttext//Logistic-Regression.hyp.tag -> ./models/fasttext//Logistic-Regression.tag.pair
Processing: ./models/fasttext//MLP.hyp.tag -> ./models/fasttext//MLP.tag.pair
Processing: ./models/fasttext//Random-Forest.hyp.tag -> ./models/fasttext//Random-Forest.tag.pair
Processing: ./models/fasttext//Voting.hyp.tag -> ./models/fasttext//Voting.tag.pair

real    0m0.836s
user    0m0.796s
sys     0m0.040s
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

check ...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ head CRF.tag.pair
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O N/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O N/O N/N N/N N/N E/E
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$
```

အရင်ဆုံး မော်ဒယ်အားလုံး အတွက် correction model ဆောက်တာ မပြီးခင်မှာ လက်ရှိပြီးနေတဲ့ CRF model ကို သုံးပြီးတော့ model နှစ်ခု ဆင့်လုပ်တာရဲ့ အခြေအနေကို သိချင်လို့ testing လုပ်ကြည့်ခဲ့... 

excited ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.version2.py --test ./models/fasttext/CRF.tag.pair --ft-model ./tag.fasttext.model.bin --model ./models/fasttext/dummy/models/CRF.tag.model --method CRF --output ./CRF-CRF.testing.result
2024-12-15 18:00:33,199 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-15 18:00:34,021 - Preparing features for CRF testing...
2024-12-15 18:00:47,090 - Saving predictions to ./CRF-CRF.testing.result...
2024-12-15 18:00:47,121 - Predictions saved successfully.
2024-12-15 18:00:48,113 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.46      0.61     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773


real    0m16.527s
user    0m17.468s
sys     0m5.784s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Overall accuracy က 0.91 ပဲရတယ်။  

ပထမ word/tag တုန်းက ရခဲ့တဲ့ CRF result (error-overflow မှာတင်ထားတဲ့ log ဖိုင်ထဲက) တွေနဲ့ နှိုင်းယှဉ်ကြည့်ခဲ့ ...  

```
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
```

tagwise မှာ မတူဘူး။  
MLP တိုးပြီး run all နဲ့ run ပြီးရထားတဲ့ CRF baseline ရဲ့ ရလဒ်နဲ့ ပြန်နှိုင်းယှဉ်ကြည့်ခဲ့... အောက်ပါအတိုင်း  

```
2024-12-12 22:22:56,096 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-12 22:22:56,913 - Preparing features for CRF testing...
2024-12-12 22:23:10,000 - Saving predictions to ./models/CRF.hyp...
2024-12-12 22:23:10,052 - Predictions saved successfully.
2024-12-12 22:23:11,034 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.45      0.61     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773
```

output ဖိုင်ကို ကြည့်ကြည့်တော့ အောက်ပါအတိုင်း ရတာကို တွေ့ရတယ်။  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head CRF-CRF.testing.result
B/B O/O O/O O/O O/O O/O O/O N/N E/E
B/B N/N N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N N/N N/N N/N N/N E/E
B/B O/O O/O O/O O/O N/N N/N N/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ tail CRF-CRF.testing.result
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E B/B N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

check random ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ shuf ./CRF-CRF.testing.result | head
B/B O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B N/N N/N N/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

တခုခု လွဲနေသလား?!  

```python
import argparse

def extract_unequal_tag_sentences(input_file, output_file):
    unequal_sentences = []

    # Read and process the input file
    with open(input_file, 'r', encoding='utf-8') as file:
        for line in file:
            line = line.strip()
            if not line:
                continue

            # Check if tags are unequal
            tokens = line.split()
            unequal = any(token.split('/')[0] != token.split('/')[1] for token in tokens)

            if unequal:
                unequal_sentences.append(line)

    # Write output to file or stdout
    if output_file:
        with open(output_file, 'w', encoding='utf-8') as out_file:
            for sentence in unequal_sentences:
                out_file.write(sentence + '\n')
    else:
        for sentence in unequal_sentences:
            print(sentence)

if __name__ == "__main__":
    # Setup argument parser
    parser = argparse.ArgumentParser(description="Extract sentences with unequal tags from a UTF-8 text file.")
    parser.add_argument("input_file", help="Path to the input file.")
    parser.add_argument("--output_file", help="Path to the output file. Defaults to stdout.", default=None)

    args = parser.parse_args()

    # Run the extraction
    extract_unequal_tag_sentences(args.input_file, args.output_file)


```

1st tag နဲ့ 2nd tag မတူတာတွေကိုပဲ ဆွဲထုတ်ကြည့်ခဲ့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./chk-unequal-tags.py ./CRF-CRF.testing.result > ./CRF-CRF.testing.result.chk
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./CRF-CRF.testing.result.chk
  43  375 1500 ./CRF-CRF.testing.result.chk
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

၄၃ ကြောင်းမှားတာတွေ့ရ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./CRF-CRF.testing.result.chk
B/B O/N N/N E/E B/B O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/N N/N E/E B/B O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/N N/N E/E
O/B
B/B O/N N/N E/E
B/B O/N N/N E/E
B/B O/N O/E
B/B O/N N/N N/N N/N E/E
B/B O/N N/N N/N E/E
B/B O/N N/N E/E
```

အရင်က baseline or CRF model တစ်ခုတည်းနဲ့ test လုပ်ပြီး ရလာတဲ့ ရလဒ်ကိုလည်း စစ်ကြည့်ခဲ့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ perl ./mk-pair.pl ./models/fasttext/CRF.hyp.tag ./data/syl/bone/test.tagged.bone.tag > CRF-baseline.result
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./CRF-baseline.result
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O N/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O N/O N/N N/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Baseline ရလဒ်ဖိုင်ကနေ 1st tag နဲ့ 2nd tag မတူတာကို ဆွဲထုတ်ကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./chk-unequal-tags.py ./CRF-baseline.result > CRF-baseline.result.chk
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./CRF-baseline.result.chk
  4886 133897 535588 ./CRF-baseline.result.chk
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

./CRF-baseline.result.chk ဖိုင်ကို စစ်ကြည့်ခဲ့...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ head ./CRF-baseline.result.chk
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O N/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O N/O N/N N/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ tail ./CRF-baseline.result.
chk
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N N/N E/E B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O E/N B/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

F1-score က တူနေပေမဲ့ ရလဒ်က မတူတာတော့ သေချာသွားပြီ။  


```python
import argparse
from collections import defaultdict
import numpy as np

def parse_file(file_path):
    """Parses the input file into hypothesis and reference tags."""
    hyp_tags = []
    ref_tags = []

    with open(file_path, 'r', encoding='utf-8') as f:
        for line in f:
            line = line.strip()
            if not line:
                continue

            pairs = line.split()
            for pair in pairs:
                hyp, ref = pair.split('/')
                hyp_tags.append(hyp)
                ref_tags.append(ref)

    return hyp_tags, ref_tags

def calculate_metrics(hyp_tags, ref_tags):
    """Calculates precision, recall, F1-score, and accuracy for each tag."""
    tag_metrics = defaultdict(lambda: {'TP': 0, 'FP': 0, 'FN': 0})
    correct = 0

    for hyp, ref in zip(hyp_tags, ref_tags):
        if hyp == ref:
            correct += 1
            tag_metrics[ref]['TP'] += 1
        else:
            tag_metrics[hyp]['FP'] += 1
            tag_metrics[ref]['FN'] += 1

    total = len(hyp_tags)
    accuracy = correct / total if total > 0 else 0

    scores = {}
    for tag, counts in tag_metrics.items():
        TP = counts['TP']
        FP = counts['FP']
        FN = counts['FN']

        precision = TP / (TP + FP) if (TP + FP) > 0 else 0
        recall = TP / (TP + FN) if (TP + FN) > 0 else 0
        f1 = 2 * (precision * recall) / (precision + recall) if (precision + recall) > 0 else 0

        scores[tag] = {
            'precision': precision,
            'recall': recall,
            'f1': f1
        }

    overall_f1 = np.mean([scores[tag]['f1'] for tag in scores])

    return scores, accuracy, overall_f1

def compute_confusion_matrix(hyp_tags, ref_tags, unique_tags):
    """Computes the confusion matrix for all tags."""
    tag_to_idx = {tag: idx for idx, tag in enumerate(unique_tags)}
    matrix = np.zeros((len(unique_tags), len(unique_tags)), dtype=int)

    for hyp, ref in zip(hyp_tags, ref_tags):
        hyp_idx = tag_to_idx[hyp]
        ref_idx = tag_to_idx[ref]
        matrix[ref_idx][hyp_idx] += 1

    return matrix, unique_tags

def display_confusion_matrix(matrix, tags):
    """Displays the confusion matrix in a readable format."""
    print("\nConfusion Matrix:")
    header = "\t" + "\t".join(tags)
    print(header)
    for i, row in enumerate(matrix):
        row_str = "\t".join(map(str, row))
        print(f"{tags[i]}\t{row_str}")

def main():
    parser = argparse.ArgumentParser(description="Evaluate tag-based predictions.")
    parser.add_argument('input_file', help="Path to the input file containing hyp/ref tags.")
    parser.add_argument('--confusion', '-c', action='store_true', help="Include confusion matrix in the output.")
    args = parser.parse_args()

    # Parse input file
    hyp_tags, ref_tags = parse_file(args.input_file)

    # Calculate metrics
    scores, accuracy, overall_f1 = calculate_metrics(hyp_tags, ref_tags)

    # Display metrics
    print("Tag-wise Metrics:")
    for tag, metrics in scores.items():
        print(f"{tag}: Precision: {metrics['precision']:.4f}, Recall: {metrics['recall']:.4f}, F1-Score: {metrics['f1']:.4f}")

    print(f"\nOverall Accuracy: {accuracy:.4f}")
    print(f"Overall F1-Score: {overall_f1:.4f}")

    # Confusion matrix
    if args.confusion:
        unique_tags = sorted(set(hyp_tags + ref_tags))
        matrix, tags = compute_confusion_matrix(hyp_tags, ref_tags, unique_tags)
        display_confusion_matrix(matrix, tags)

if __name__ == "__main__":
    main()


```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./evaluate.py ./CRF-CRF.testing.result --confusion
Tag-wise Metrics:
B: Precision: 1.0000, Recall: 0.9990, F1-Score: 0.9995
O: Precision: 0.9996, Recall: 1.0000, F1-Score: 0.9998
N: Precision: 1.0000, Recall: 0.9960, F1-Score: 0.9980
E: Precision: 0.9992, Recall: 0.9980, F1-Score: 0.9986

Overall Accuracy: 0.9996
Overall F1-Score: 0.9990

Confusion Matrix:
        B       E       N       O
B       5932    5       0       1
E       0       5919    0       12
N       0       0       9555    38
O       0       0       0       122311
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

baseline model ရဲ့ ရလဒ်ကို တွက်ကြည့်တော့ အောက်ပါအတိုင်း ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python ./evaluate.py ./CRF-baseline.result --confusion
Tag-wise Metrics:
B: Precision: 0.9899, Recall: 0.8559, F1-Score: 0.9180
O: Precision: 0.8969, Recall: 0.9945, F1-Score: 0.9432
N: Precision: 0.9380, Recall: 0.4543, F1-Score: 0.6122
E: Precision: 0.9887, Recall: 0.8577, F1-Score: 0.9185

Overall Accuracy: 0.9072
Overall F1-Score: 0.8480

Confusion Matrix:
        B       E       N       O
B       5872    7       27      955
E       4       5857    18      950
N       26      27      8963    10712
O       30      33      547     109745
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

အလုပ်လုပ်တယ်။ 
Researcher smile :)   

## Updating train/test python code (version 3)
မှားနေတယ်။ ဒီ code က ပြန်စစ်ရန် ...  

```python
import argparse
import os
import fasttext
import numpy as np
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier, AdaBoostClassifier, GradientBoostingClassifier, VotingClassifier
from sklearn.linear_model import LogisticRegression
from sklearn.neural_network import MLPClassifier
from sklearn_crfsuite import CRF
from sklearn_crfsuite.metrics import flat_classification_report
from sklearn.metrics import classification_report
from sklearn.metrics import confusion_matrix

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

def calculate_metrics(flattened_true, flattened_predictions):
    """Calculate tag-wise metrics and overall accuracy."""
    unique_tags = sorted(set(flattened_true) | set(flattened_predictions))
    tag_metrics = {}
    tag_to_idx = {tag: idx for idx, tag in enumerate(unique_tags)}
    confusion = np.zeros((len(unique_tags), len(unique_tags)), dtype=int)

    # Populate confusion matrix
    for true_tag, pred_tag in zip(flattened_true, flattened_predictions):
        true_idx = tag_to_idx[true_tag]
        pred_idx = tag_to_idx[pred_tag]
        confusion[true_idx, pred_idx] += 1

    # Calculate metrics for each tag
    for tag, idx in tag_to_idx.items():
        tp = confusion[idx, idx]
        fp = confusion[:, idx].sum() - tp
        fn = confusion[idx, :].sum() - tp
        precision = tp / (tp + fp) if (tp + fp) > 0 else 0.0
        recall = tp / (tp + fn) if (tp + fn) > 0 else 0.0
        f1 = 2 * precision * recall / (precision + recall) if (precision + recall) > 0 else 0.0

        tag_metrics[tag] = {
            "precision": precision,
            "recall": recall,
            "f1": f1,
        }

    # Overall accuracy
    accuracy = np.trace(confusion) / np.sum(confusion) if np.sum(confusion) > 0 else 0.0

    return tag_metrics, accuracy, confusion, unique_tags

def display_confusion_matrix(confusion, tags):
    """Displays the confusion matrix in a readable format."""
    print("\nConfusion Matrix:")
    header = "\t" + "\t".join(tags)
    print(header)
    for i, row in enumerate(confusion):
        row_str = "\t".join(map(str, row))
        print(f"{tags[i]}\t{row_str}")

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
    elif method == "MLP":
        model = MLPClassifier(hidden_layer_sizes=(100,), max_iter=500, random_state=42)
    else:
        raise ValueError(f"Unsupported method: {method}")

    model.fit(X, y)
    logger.info(f"Saving trained model to {output_model_file}...")
    joblib.dump(model, output_model_file)
    logger.info(f"Training for {method} completed.")

def test_model(test_file, ft_model_file, trained_model_file, raw_test, method, output_file, logger):
    """Test the model and evaluate metrics."""
    logger.info(f"Testing {method} model...")

    if raw_test:
        sentences = load_raw_data(test_file)
        labels = None
    else:
        sentences, labels = load_tagged_data(test_file)

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
        start_idx = 0
        realigned_predictions = []

        for length in sentence_lengths:
            realigned_predictions.append(predictions[start_idx:start_idx + length])
            start_idx += length

        predictions = realigned_predictions

    logger.info(f"Saving predictions to {output_file}...")
    with open(output_file, 'w', encoding='utf-8') as f:
        for sentence, sentence_predictions in zip(sentences, predictions):
            formatted_sentence = " ".join(f"{word}/{tag}" for word, tag in zip(sentence, sentence_predictions))
            f.write(f"{formatted_sentence}\n")

    logger.info(f"Predictions saved successfully.")

    if not raw_test:
        flattened_true = flatten_labels(labels)
        flattened_predictions = flatten_labels(predictions)

        if len(flattened_true) != len(flattened_predictions):
            logger.error(f"Length mismatch: true labels ({len(flattened_true)}) vs predictions ({len(flattened_predictions)})")
            for i, (t, p) in enumerate(zip(flattened_true, flattened_predictions)):
                print(f"Index {i}: True={t}, Predicted={p}")
            raise ValueError("Length mismatch detected!")

        logger.info("Calculating custom evaluation metrics...")
        tag_metrics, accuracy, confusion, unique_tags = calculate_metrics(flattened_true, flattened_predictions)

        logger.info("Displaying evaluation results...")
        print("\nTag-wise Metrics:")
        for tag, metrics in tag_metrics.items():
            print(f"{tag}: Precision: {metrics['precision']:.4f}, Recall: {metrics['recall']:.4f}, F1-Score: {metrics['f1']:.4f}")

        print(f"\nOverall Accuracy: {accuracy:.4f}")
        print(f"\nOverall F1-Score: {np.mean([metrics['f1'] for metrics in tag_metrics.values()]):.4f}")
        
        logger.info("Displaying confusion matrix...")
        display_confusion_matrix(confusion, unique_tags)

def main():
    parser = argparse.ArgumentParser(description="FastText + ML Models for Sentence Segmentation.")
    parser.add_argument("--train", help="Train the model. Provide the training corpus file path.")
    parser.add_argument("--test", help="Test the model. Provide the test corpus file path.")
    parser.add_argument("--ft-model", default="fasttext_model.bin", help="FastText model file (default: fasttext_model.bin).")
    parser.add_argument("--model", default="model.pkl", help="Trained model file (default: model.pkl).")
    parser.add_argument("--method", "-m", default="CRF",
                        choices=["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting", "MLP", "all"],
                        help="Choose the classification method (default: CRF).")
    parser.add_argument("--raw", action="store_true", help="Test the model with raw input (no tags).")
    parser.add_argument("--output", help="Specify the output file for predictions.")

    args = parser.parse_args()

    logging.basicConfig(filename="all-training-testing.log" if args.method == "all" else None,
                        level=logging.INFO,
                        format="%(asctime)s - %(message)s")
    logger = logging.getLogger()

    if args.method == "all":
        methods = ["Decision-Tree", "Random-Forest", "Logistic-Regression", "CRF", "AdaBoost", "GradientBoosting", "Voting", "MLP"]
    else:
        methods = [args.method]

    if args.train:
        for method in methods:
            #model_file = f"models/{method}.model"
            model_file = args.model
            train_model(args.train, args.ft_model, model_file, method, logger)
    elif args.test or args.raw:
        raw_mode = args.raw  # True if raw, False otherwise
        for method in methods:
            #model_file = f"models/{method}.model"
            model_file = args.model
            default_output_file = f"predictions_{method}.txt"
            output_file = args.output or default_output_file
            test_model(
                test_file=args.test,
                ft_model_file=args.ft_model,
                trained_model_file=model_file,
                raw_test=raw_mode,
                method=method,
                output_file=output_file,
                logger=logger
            )
    else:
        parser.print_help()


if __name__ == "__main__":
    main()



```

--help ပဲခေါ်ကြည့်ထား။ train/test မလုပ်ရသေး။  

## Testing with ALL Error Correction Model  

ပထမမော်ဒယ် သို့မဟုတ် baseline မော်ဒယ်နဲ့ train ထားတဲ့ output hyp ဖိုင်တွေက ဒီတခါတော့ test data ဖြစ်လိမ့်မယ်။  

model file:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ ll -h *.model
-rw-rw-r-- 1 ye ye  36K Dec 15 17:20 AdaBoost.tag.model
-rw-rw-r-- 1 ye ye  47K Dec 15 17:26 CRF.tag.model
-rw-rw-r-- 1 ye ye 2.0K Dec 15 17:26 Decision-Tree.tag.model
-rw-rw-r-- 1 ye ye 422K Dec 15 18:02 GradientBoosting.tag.model
-rw-rw-r-- 1 ye ye 4.0K Dec 15 18:02 Logistic-Regression.tag.model
-rw-rw-r-- 1 ye ye 252K Dec 15 18:12 MLP.tag.model
-rw-rw-r-- 1 ye ye 107K Dec 15 18:15 Random-Forest.tag.model
-rw-rw-r-- 1 ye ye 112K Dec 15 18:18 Voting.tag.model
```

Test data path:  

```
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/  
```

Prepare Test Files:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./extract-tag.sh ./models/fasttext/dummy/models/ hyp
Processing: ./models/fasttext/dummy/models//AdaBoost.hyp -> ./models/fasttext/dummy/models//AdaBoost.hyp.tag
Processing: ./models/fasttext/dummy/models//CRF.hyp -> ./models/fasttext/dummy/models//CRF.hyp.tag
Processing: ./models/fasttext/dummy/models//Decision-Tree.hyp -> ./models/fasttext/dummy/models//Decision-Tree.hyp.tag
Processing: ./models/fasttext/dummy/models//GradientBoosting.hyp -> ./models/fasttext/dummy/models//GradientBoosting.hyp.tag
Processing: ./models/fasttext/dummy/models//Logistic-Regression.hyp -> ./models/fasttext/dummy/models//Logistic-Regression.hyp.tag
Processing: ./models/fasttext/dummy/models//MLP.hyp -> ./models/fasttext/dummy/models//MLP.hyp.tag
Processing: ./models/fasttext/dummy/models//Random-Forest.hyp -> ./models/fasttext/dummy/models//Random-Forest.hyp.tag
Processing: ./models/fasttext/dummy/models//Voting.hyp -> ./models/fasttext/dummy/models//Voting.hyp.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ wc ./models/fasttext/dummy/models/*.tag
   5512  143773  287546 ./models/fasttext/dummy/models/AdaBoost.hyp.tag
   5512  143773  287546 ./models/fasttext/dummy/models/CRF.hyp.tag
   5512  143773  287546 ./models/fasttext/dummy/models/Decision-Tree.hyp.tag
   5512  143773  287546 ./models/fasttext/dummy/models/GradientBoosting.hyp.tag
   5512  143773  287546 ./models/fasttext/dummy/models/Logistic-Regression.hyp.tag
   5512  143773  287546 ./models/fasttext/dummy/models/MLP.hyp.tag
   5512  143773  287546 ./models/fasttext/dummy/models/Random-Forest.hyp.tag
   5512  143773  287546 ./models/fasttext/dummy/models/Voting.hyp.tag
  44096 1150184 2300368 total
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

အောက်ပါ command ကို run မိခဲ့တယ်။   
မှားတယ်။ test data ကို train-valid နဲ့ သွားတွဲမိလို့။ ပြီးတော့ reference path လည်း မဟုတ်ခဲ့။  
```
 ./make-pair.sh ./models/fasttext/dummy/models/ hyp.tag tag.pair ./models/fasttext/dummy/train-valid.tagged.bone.tag
```

အဲဒါကြောင့် တွဲပြီးထွက်လာတဲ့ ရလဒ်က အောက်ပါအတိုင်း စာကြောင်း length မညီတဲ့ ပြဿနာတွေရှိလာတယ်။  
Pair လုပ်တာမှာ ERROR ရှိတယ်။   
  
```
$ head -n 3 ../../../../data/syl/bone/test.tagged.bone.tag
B O O O O N N N E
B O N N N E
B O O O O O O N N N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head -n 3 ./CRF.hyp.tag
B O O O O O O N E
B N N N N E
B O O O O O O O N N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head -n 3 ./CRF.hyp
B/B O/O O/O O/O O/O O/O O/O N/N E/E
B/B N/N N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head -n 3 ./CRF.tag.pair
B/B O/N O/N O/E O/ O/ O/ N/ E/
B/B N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$
```

အမှန်က အောက်ပါအတိုင်း run ရမယ်။  

```
./make-pair.sh ./models/fasttext/dummy/models/ hyp.tag tag.pair ./data/syl/bone/test.tagged.bone.tag
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./make-pair.sh ./models/fasttext/dummy/models/ hyp.tag tag.pair ./data/syl/bone/test.tagged.bone.tag
Processing: ./models/fasttext/dummy/models//AdaBoost.hyp.tag -> ./models/fasttext/dummy/models//AdaBoost.tag.pair
Processing: ./models/fasttext/dummy/models//CRF.hyp.tag -> ./models/fasttext/dummy/models//CRF.tag.pair
Processing: ./models/fasttext/dummy/models//Decision-Tree.hyp.tag -> ./models/fasttext/dummy/models//Decision-Tree.tag.pair
Processing: ./models/fasttext/dummy/models//GradientBoosting.hyp.tag -> ./models/fasttext/dummy/models//GradientBoosting.tag.pair
Processing: ./models/fasttext/dummy/models//Logistic-Regression.hyp.tag -> ./models/fasttext/dummy/models//Logistic-Regression.tag.pair
Processing: ./models/fasttext/dummy/models//MLP.hyp.tag -> ./models/fasttext/dummy/models//MLP.tag.pair
Processing: ./models/fasttext/dummy/models//Random-Forest.hyp.tag -> ./models/fasttext/dummy/models//Random-Forest.tag.pair
Processing: ./models/fasttext/dummy/models//Voting.hyp.tag -> ./models/fasttext/dummy/models//Voting.tag.pair
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

pair တွဲထားတဲ့ ဖိုင်တွေကို ဝင်စစ်...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ wc *.tag.pair
   5512  143773  575092 AdaBoost.tag.pair
   5512  143773  575092 CRF.tag.pair
   5512  143773  575092 Decision-Tree.tag.pair
   5512  143773  575092 GradientBoosting.tag.pair
   5512  143773  575092 Logistic-Regression.tag.pair
   5512  143773  575092 MLP.tag.pair
   5512  143773  575092 Random-Forest.tag.pair
   5512  143773  575092 Voting.tag.pair
  44096 1150184 4600736 total
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ ll -h *.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 AdaBoost.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 CRF.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 Decision-Tree.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 GradientBoosting.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 Logistic-Regression.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 MLP.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 Random-Forest.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 05:47 Voting.tag.pair
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head CRF.tag.pair
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O N/O N/O N/N N/N N/N E/E
B/B O/O O/O O/O O/O N/O N/N N/N N/N E/E
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ tail Decision-Tree.tag.pair
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E
B/B O/O O/O O/O O/N O/N O/N E/E
O/B O/O O/O O/N O/N O/N N/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E
O/B N/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N N/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N N/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/O E/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N O/N E/E
O/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/N O/N N/N E/E
```

check make-pair.sh   

training data အတွက်က  
```
## ./make-pair.sh ./models/fasttext/dummy/ hyp.tag tag.pair \
## ./models/fasttext/dummy/train-valid.tagged.bone.tag
```
train-valid.tagged.bone.tag ဖိုင်ကို models/fasttext/dummy/ ဖိုလ်ဒါအောက်ကို ကောပီကူးပြီးမှ လုပ်ခဲ့တဲ့ပုံရတယ်။  

test data အတွက် pair ပြင်တဲ့ command က  
```
## ./make-pair.sh ./models/fasttext/ hyp.tag tag.pair ./data/syl/bone/test.tagged.bone.tag
```

ပြန်စဉ်းစားရင် model/fasttext/ အောက်က ရလဒ်တွေက baseline model ရဲ့ ရလဒ်တွေ။ စာလုံး input လုပ်ပြီး ထွက်လာတဲ့ tag တွေ။  

fasttext/dummy/အောက်က ရလဒ်တွေက training data ပြင်ဆင်တုန်းက တွဲခဲ့တဲ့ pair တွေ။  

fasttext model for tags:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ls *.bin
tag.fasttext.model.bin
```

Example Running commands:  
တကယ်လို့ shell script မသုံးပဲနဲ့ experiment တစ်ခုချင်းစီကို run မယ်ဆိုရင် အောက်ပါအတိုင်းသွားရမယ်။  

```
time python ./fasttext-ml.version3.py --test ./models/fasttext/dummy/models/CRF.tag.pair --ft-model ./tag.fasttext.model.bin --model ./models/fasttext/dummy/models/CRF.tag.model --method CRF --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.hyp

time python ./fasttext-ml.version3.py --test ./models/fasttext/dummy/models/Decision-Tree.tag.pair --ft-model ./tag.fasttext.model.bin --model ./models/fasttext/dummy/models/Decision-Tree.tag.model --method Decision-Tree --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Decision-Tree.hyp
```

Preparing a bash shell script ...  

```bash
#!/bin/bash

# Usage: ./run_tests.sh --test-dir <test_files_dir> --model-dir <models_dir> --output-dir <output_dir> --ft-model <fasttext_model>

# Function to display usage
function usage() {
    echo "Usage: $0 --test-dir <test_files_dir> --model-dir <models_dir> --output-dir <output_dir> --ft-model <fasttext_model>"
    exit 1
}

# Parse command-line arguments
while [[ $# -gt 0 ]]; do
    case $1 in
        --test-dir)
            TEST_DIR="$2"
            shift 2
            ;;
        --model-dir)
            MODEL_DIR="$2"
            shift 2
            ;;
        --output-dir)
            OUTPUT_DIR="$2"
            shift 2
            ;;
        --ft-model)
            FT_MODEL="$2"
            shift 2
            ;;
        *)
            usage
            ;;
    esac
done

# Check if all required arguments are provided
if [[ -z "$TEST_DIR" || -z "$MODEL_DIR" || -z "$OUTPUT_DIR" || -z "$FT_MODEL" ]]; then
    usage
fi

# Ensure output directory exists
mkdir -p "$OUTPUT_DIR"

# Loop through test files in the specified test directory
for TEST_FILE in "$TEST_DIR"/*.tag.pair; do
    # Extract base name (e.g., CRF from CRF.tag.pair)
    BASE_NAME=$(basename "$TEST_FILE" .tag.pair)

    # Determine the corresponding model file and method
    MODEL_FILE="$MODEL_DIR/$BASE_NAME.tag.model"
    METHOD="$BASE_NAME"

    # Construct the output file path
    OUTPUT_FILE="$OUTPUT_DIR/$BASE_NAME.hyp"

    # Check if model file exists
    if [[ ! -f "$MODEL_FILE" ]]; then
        echo "Model file not found for $TEST_FILE (expected: $MODEL_FILE). Skipping."
        continue
    fi

    # Run the Python command
    time python ./fasttext-ml.version3.py \
        --test "$TEST_FILE" \
        --ft-model "$FT_MODEL" \
        --model "$MODEL_FILE" \
        --method "$METHOD" \
        --output "$OUTPUT_FILE"

done

```

Testing with all error-correction models ...  
*** Output model folder ကို ဖိုလ်ဒါသပ်သပ်ဆောက်ပြီး ပေးရမယ်။ မဟုတ်ရင် hyp ဖိုင်တွေ ရောကုန်လိမ့်မယ်။  

```
time ./run-test-with-err-models.sh --test-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext --model-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models --output-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/err-model-result/ --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin
```

ဒီနေရာမှာ လည်နေခဲ့တယ်။  
အိပ်ယာနိုး ပြန်စစ်၊ ပြန်စဉ်းစားကြည့်တော့မှ ဂရုပြုမိတာက ...

2nd time testing or testing with error-correction model လုပ်တဲ့အခါမှာ test data path ကို သတိထားရမယ်။ ပြီးတော့ testing လုပ်ပြီးထွက်လာတဲ့ hyp ဖိုင်တွေကနေ evaluation အတွက် ပြင်တဲ့အခါမှာ output ကို ဖိုလ်ဒါသပ်သပ်မှာ ခွဲသိမ်းသင့်တယ်။  

နောက်ထပ် လုပ်ခဲ့တဲ့ အမှားက version 3 code ရဲ့ evaluation အပိုင်းလို့ ထင်တယ်။ tag/tag ကနေ evaluation လုပ်ထားတာကို training-testing python code ထဲမှာ ဝင်ရောရေးတာမှာ မှားတာ ရှိနိုင်တယ်။ version 3 က လက်ရှိ manual testing ပြီးမှပဲ ပြန် update လုပ်ရမယ်။

Testing with error-correction model အတွက်ဆိုရင် အောက်က experiment ကိုပဲ ကြည့်ရင် OK တယ်။ အထက်က testing with error-correction model လုပ်တဲ့ အဆင့်တွေကို မကြည့်နဲ့။  

#########################################################
#########################################################

## Testing with Error-Correction Model (AGAIN!)  
 

testing မလုပ်ခင်မှာ model folder မှာ model file (i.e. error-correction models) တွေပဲ ကျန်အောင် cleaning လုပ်ခဲ့တယ်။  
rm *.hyp, rm *.tag, rm *.tag.pair လုပ်ခဲ့တယ်။  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ ls
AdaBoost.tag.model       err-model-result               mk-pair.pl               tmp
CRF.tag.model            GradientBoosting.tag.model     MLP.tag.model            Voting.tag.model
Decision-Tree.tag.model  Logistic-Regression.tag.model  Random-Forest.tag.model
```

Model တစ်ခုချင်းစီအတွက် experiment တစ်ခုချင်းစီအတွက် Manual Run မယ်ဆိုရင် အောက်ပါလိုမျိုး run ရမယ်။  
 
```
time python ./fasttext-ml.version2.py --test ./models/fasttext/CRF.tag.pair --ft-model ./tag.fasttext.model.bin --model ./models/fasttext/dummy/models/CRF.tag.model --method CRF --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.hyp

time python ./fasttext-ml.version2.py --test ./models/fasttext/Decision-Tree.tag.pair --ft-model ./tag.fasttext.model.bin --model ./models/fasttext/dummy/models/Decision-Tree.tag.model --method Decision-Tree --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Decision-Tree.hyp
```

bash script ကိုလည်း ပြန် update လုပ်ခဲ့တယ်။  

```bash
#!/bin/bash

# Usage: ./run_tests.sh --test-dir <test_files_dir> --model-dir <models_dir> --output-dir <output_dir> --ft-model <fasttext_model>

# Function to display usage
function usage() {
    echo "Usage: $0 --test-dir <test_files_dir> --model-dir <models_dir> --output-dir <output_dir> --ft-model <fasttext_model>"
    exit 1
}

# Parse command-line arguments
while [[ $# -gt 0 ]]; do
    case $1 in
        --test-dir)
            TEST_DIR="$2"
            shift 2
            ;;
        --model-dir)
            MODEL_DIR="$2"
            shift 2
            ;;
        --output-dir)
            OUTPUT_DIR="$2"
            shift 2
            ;;
        --ft-model)
            FT_MODEL="$2"
            shift 2
            ;;
        *)
            usage
            ;;
    esac
done

# Check if all required arguments are provided
if [[ -z "$TEST_DIR" || -z "$MODEL_DIR" || -z "$OUTPUT_DIR" || -z "$FT_MODEL" ]]; then
    usage
fi

# Ensure output directory exists
mkdir -p "$OUTPUT_DIR"

# Loop through test files in the specified test directory
for TEST_FILE in "$TEST_DIR"/*.tag.pair; do
    # Extract base name (e.g., CRF from CRF.tag.pair)
    BASE_NAME=$(basename "$TEST_FILE" .tag.pair)

    # Determine the corresponding model file and method
    MODEL_FILE="$MODEL_DIR/$BASE_NAME.tag.model"
    METHOD="$BASE_NAME"

    # Construct the output file path
    OUTPUT_FILE="$OUTPUT_DIR/$BASE_NAME.hyp"

    # Check if model file exists
    if [[ ! -f "$MODEL_FILE" ]]; then
        echo "Model file not found for $TEST_FILE (expected: $MODEL_FILE). Skipping."
        continue
    fi

    # Run the Python command
    time python ./fasttext-ml.version2.py \
        --test "$TEST_FILE" \
        --ft-model "$FT_MODEL" \
        --model "$MODEL_FILE" \
        --method "$METHOD" \
        --output "$OUTPUT_FILE"

done

```

Testing with all error-correction models ...  
*** Output model folder ကို ဖိုလ်ဒါသပ်သပ်ဆောက်ပြီး ပေးရမယ်။ မဟုတ်ရင် hyp ဖိုင်တွေ ရောကုန်လိမ့်မယ်။  

```
time ./run-test-with-err-models.sh --test-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext --model-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models --output-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/ --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin
```


Run testing with version-2 ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./run-test-with-err-models.sh --test-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext --model-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models --output-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/ --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/AdaBoost.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/AdaBoost.tag.model --method AdaBoost --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//AdaBoost.hyp
2024-12-16 07:16:46,506 - Testing AdaBoost model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:16:47,303 - Preparing features for AdaBoost testing...
2024-12-16 07:16:49,220 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//AdaBoost.hyp...
2024-12-16 07:16:49,309 - Predictions saved successfully.
/home/ye/.local/lib/python3.10/site-packages/sklearn/metrics/_classification.py:1509: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, f"{metric.capitalize()} is", len(result))
/home/ye/.local/lib/python3.10/site-packages/sklearn/metrics/_classification.py:1509: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, f"{metric.capitalize()} is", len(result))
/home/ye/.local/lib/python3.10/site-packages/sklearn/metrics/_classification.py:1509: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, f"{metric.capitalize()} is", len(result))
2024-12-16 07:16:50,347 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.00      0.00      0.00      6861
           E       0.71      0.63      0.67      6829
           N       0.62      0.07      0.13     19728
           O       0.80      0.98      0.88    110355

    accuracy                           0.79    143773
   macro avg       0.53      0.42      0.42    143773
weighted avg       0.73      0.79      0.73    143773


real    0m4.793s
user    0m7.387s
sys     0m4.302s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/CRF.tag.pair .tag.pair
+ BASE_NAME=CRF
+ MODEL_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.tag.model
+ METHOD=CRF
+ OUTPUT_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//CRF.hyp
+ [[ ! -f /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.tag.model ]]
+ set -x
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/CRF.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/CRF.tag.model --method CRF --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//CRF.hyp
2024-12-16 07:16:51,297 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:16:52,083 - Preparing features for CRF testing...
2024-12-16 07:17:05,048 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//CRF.hyp...
2024-12-16 07:17:05,079 - Predictions saved successfully.
2024-12-16 07:17:06,068 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.99      0.86      0.92      6861
           E       0.99      0.86      0.92      6829
           N       0.94      0.46      0.61     19728
           O       0.90      0.99      0.94    110355

    accuracy                           0.91    143773
   macro avg       0.95      0.79      0.85    143773
weighted avg       0.91      0.91      0.90    143773


real    0m16.391s
user    0m17.652s
sys     0m5.668s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Decision-Tree.tag.pair .tag.pair
+ BASE_NAME=Decision-Tree
+ MODEL_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Decision-Tree.tag.model
+ METHOD=Decision-Tree
+ OUTPUT_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Decision-Tree.hyp
+ [[ ! -f /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Decision-Tree.tag.model ]]
+ set -x
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Decision-Tree.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Decision-Tree.tag.model --method Decision-Tree --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Decision-Tree.hyp
2024-12-16 07:17:07,691 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:17:08,478 - Preparing features for Decision-Tree testing...
2024-12-16 07:17:09,368 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Decision-Tree.hyp...
2024-12-16 07:17:09,455 - Predictions saved successfully.
2024-12-16 07:17:10,505 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.67      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m3.734s
user    0m6.397s
sys     0m4.266s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/GradientBoosting.tag.pair .tag.pair
+ BASE_NAME=GradientBoosting
+ MODEL_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/GradientBoosting.tag.model
+ METHOD=GradientBoosting
+ OUTPUT_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//GradientBoosting.hyp
+ [[ ! -f /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/GradientBoosting.tag.model ]]
+ set -x
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/GradientBoosting.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/GradientBoosting.tag.model --method GradientBoosting --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//GradientBoosting.hyp
2024-12-16 07:17:11,423 - Testing GradientBoosting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:17:12,224 - Preparing features for GradientBoosting testing...
2024-12-16 07:17:14,508 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//GradientBoosting.hyp...
2024-12-16 07:17:14,595 - Predictions saved successfully.
2024-12-16 07:17:15,625 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.56      0.17      0.26      6861
           E       0.71      0.77      0.74      6829
           N       0.62      0.16      0.26     19728
           O       0.82      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.52      0.54    143773
weighted avg       0.78      0.81      0.76    143773


real    0m5.142s
user    0m7.827s
sys     0m4.247s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Logistic-Regression.tag.pair .tag.pair
+ BASE_NAME=Logistic-Regression
+ MODEL_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Logistic-Regression.tag.model
+ METHOD=Logistic-Regression
+ OUTPUT_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Logistic-Regression.hyp
+ [[ ! -f /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Logistic-Regression.tag.model ]]
+ set -x
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Logistic-Regression.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Logistic-Regression.tag.model --method Logistic-Regression --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Logistic-Regression.hyp
2024-12-16 07:17:16,564 - Testing Logistic-Regression model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:17:17,344 - Preparing features for Logistic-Regression testing...
2024-12-16 07:17:18,274 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Logistic-Regression.hyp...
2024-12-16 07:17:18,422 - Predictions saved successfully.
2024-12-16 07:17:19,456 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.55      0.09      0.16      6861
           E       0.72      0.73      0.72      6829
           N       0.56      0.13      0.21     19728
           O       0.81      0.97      0.88    110355

    accuracy                           0.80    143773
   macro avg       0.66      0.48      0.49    143773
weighted avg       0.76      0.80      0.75    143773


real    0m3.807s
user    0m8.480s
sys     0m6.227s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/MLP.tag.pair .tag.pair
+ BASE_NAME=MLP
+ MODEL_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/MLP.tag.model
+ METHOD=MLP
+ OUTPUT_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//MLP.hyp
+ [[ ! -f /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/MLP.tag.model ]]
+ set -x
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/MLP.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/MLP.tag.model --method MLP --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//MLP.hyp
2024-12-16 07:17:20,379 - Testing MLP model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:17:21,164 - Preparing features for MLP testing...
2024-12-16 07:17:24,560 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//MLP.hyp...
2024-12-16 07:17:24,697 - Predictions saved successfully.
2024-12-16 07:17:25,742 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.16      0.25      6861
           E       0.71      0.77      0.74      6829
           N       0.61      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.52      0.54    143773
weighted avg       0.78      0.81      0.77    143773


real    0m6.324s
user    1m7.647s
sys     0m18.198s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Random-Forest.tag.pair .tag.pair
+ BASE_NAME=Random-Forest
+ MODEL_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Random-Forest.tag.model
+ METHOD=Random-Forest
+ OUTPUT_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Random-Forest.hyp
+ [[ ! -f /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Random-Forest.tag.model ]]
+ set -x
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Random-Forest.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Random-Forest.tag.model --method Random-Forest --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Random-Forest.hyp
2024-12-16 07:17:26,699 - Testing Random-Forest model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:17:27,512 - Preparing features for Random-Forest testing...
2024-12-16 07:17:28,929 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Random-Forest.hyp...
2024-12-16 07:17:29,021 - Predictions saved successfully.
2024-12-16 07:17:30,068 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m4.279s
user    0m6.812s
sys     0m4.398s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Voting.tag.pair .tag.pair
+ BASE_NAME=Voting
+ MODEL_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Voting.tag.model
+ METHOD=Voting
+ OUTPUT_FILE=/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Voting.hyp
+ [[ ! -f /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Voting.tag.model ]]
+ set -x
+ python ./fasttext-ml.version2.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/Voting.tag.pair --ft-model /home/ye/data/hello-sayarwon/coding/model-based/tag.fasttext.model.bin --model /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models/Voting.tag.model --method Voting --output /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Voting.hyp
2024-12-16 07:17:30,981 - Testing Voting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-16 07:17:31,799 - Preparing features for Voting testing...
2024-12-16 07:17:34,310 - Saving predictions to /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models//Voting.hyp...
2024-12-16 07:17:34,396 - Predictions saved successfully.
2024-12-16 07:17:35,428 - Evaluation Results:
              precision    recall  f1-score   support

           B       0.57      0.19      0.28      6861
           E       0.71      0.77      0.74      6829
           N       0.60      0.18      0.28     19728
           O       0.83      0.96      0.89    110355

    accuracy                           0.81    143773
   macro avg       0.68      0.53      0.55    143773
weighted avg       0.78      0.81      0.77    143773


real    0m5.400s
user    0m9.675s
sys     0m6.565s
+ set +x

real    0m49.885s
user    2m11.892s
sys     0m53.873s

```

## Preparing for Evaluation  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ wc *.hyp
   5512  143773  575092 AdaBoost.hyp
   5512  143773  575092 CRF.hyp
   5512  143773  575092 Decision-Tree.hyp
   5512  143773  575092 GradientBoosting.hyp
   5512  143773  575092 Logistic-Regression.hyp
   5512  143773  575092 MLP.hyp
   5512  143773  575092 Random-Forest.hyp
   5512  143773  575092 Voting.hyp
  44096 1150184 4600736 total
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head AdaBoost.hyp
O/O O/O O/O O/O O/O O/O O/O O/O N/N
O/O O/O O/O O/O O/O E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E O/O O/O N/N E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O
O/O O/O O/O O/O O/O O/O O/O O/O E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E O/O O/O O/O E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head CRF.hyp
B/B O/O O/O O/O O/O O/O O/O N/N E/E
B/B N/N N/N N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N N/N N/N N/N N/N N/N E/E
B/B O/O O/O O/O O/O N/N N/N N/N N/N E/E
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head MLP.hyp
O/O O/O O/O O/O O/O O/O O/O O/O N/N
O/O O/O O/O O/O O/O E/E
O/O O/O O/O O/O O/O O/O O/O O/O N/N O/O O/O
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O N/N O/O O/O O/O O/O O/O O/O O/O E/E O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E O/O N/N N/N E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E
O/O O/O O/O O/O O/O B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O
B/B O/O N/N O/O O/O O/O O/O O/O E/E
O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E
B/B O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O O/O E/E O/O O/O N/N E/E
O/O O/O B/B O/O O/O O/O O/O O/O O/O E/E
```

အရင်ဆုံး hyp ဖိုင်တွေဆီကနေ tag တွေကိုပဲ ဆွဲထုတ်ရမယ်။  
model ဖိုလ်ဒါအောက်မှာက လက်ရှိ အနေအထား...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ls ./models/fasttext/dummy/models/
AdaBoost.hyp        Decision-Tree.tag.model     Logistic-Regression.tag.model  Random-Forest.tag.model
AdaBoost.tag.model  err-model-result            mk-pair.pl                     tmp
CRF.hyp             GradientBoosting.hyp        MLP.hyp                        Voting.hyp
CRF.tag.model       GradientBoosting.tag.model  MLP.tag.model                  Voting.tag.model
Decision-Tree.hyp   Logistic-Regression.hyp     Random-Forest.hyp
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

run extract-tag as follows ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./extract-tag.sh ./models/fasttext/dummy/models/ hyp
Processing: ./models/fasttext/dummy/models//AdaBoost.hyp -> ./models/fasttext/dummy/models//AdaBoost.hyp.tag
Processing: ./models/fasttext/dummy/models//CRF.hyp -> ./models/fasttext/dummy/models//CRF.hyp.tag
Processing: ./models/fasttext/dummy/models//Decision-Tree.hyp -> ./models/fasttext/dummy/models//Decision-Tree.hyp.tag
Processing: ./models/fasttext/dummy/models//GradientBoosting.hyp -> ./models/fasttext/dummy/models//GradientBoosting.hyp.tag
Processing: ./models/fasttext/dummy/models//Logistic-Regression.hyp -> ./models/fasttext/dummy/models//Logistic-Regression.hyp.tag
Processing: ./models/fasttext/dummy/models//MLP.hyp -> ./models/fasttext/dummy/models//MLP.hyp.tag
Processing: ./models/fasttext/dummy/models//Random-Forest.hyp -> ./models/fasttext/dummy/models//Random-Forest.hyp.tag
Processing: ./models/fasttext/dummy/models//Voting.hyp -> ./models/fasttext/dummy/models//Voting.hyp.tag
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ wc *.hyp.tag
   5512  143773  287546 AdaBoost.hyp.tag
   5512  143773  287546 CRF.hyp.tag
   5512  143773  287546 Decision-Tree.hyp.tag
   5512  143773  287546 GradientBoosting.hyp.tag
   5512  143773  287546 Logistic-Regression.hyp.tag
   5512  143773  287546 MLP.hyp.tag
   5512  143773  287546 Random-Forest.hyp.tag
   5512  143773  287546 Voting.hyp.tag
  44096 1150184 2300368 total
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head -n 1 *.hyp.tag
==> AdaBoost.hyp.tag <==
O O O O O O O O N

==> CRF.hyp.tag <==
B O O O O O O N E

==> Decision-Tree.hyp.tag <==
O O O O O O O O N

==> GradientBoosting.hyp.tag <==
O O O O O O O O N

==> Logistic-Regression.hyp.tag <==
O O O O O O O O N

==> MLP.hyp.tag <==
O O O O O O O O N

==> Random-Forest.hyp.tag <==
O O O O O O O O N

==> Voting.hyp.tag <==
O O O O O O O O N
```

make pair လုပ်ခဲ့...  

```
## preparation for evaluation with err-correction model result (i.e. final result)
./make-pair.sh ./models/fasttext/dummy/models/ hyp.tag tag.pair ./data/syl/bone/test.tagged.bone.tag
```

Running make-pair.pl ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./make-pair.sh ./models/fasttext/dummy/models/ hyp.tag tag.pair ./data/syl/bone/test.tagged.bone.tag
Processing: ./models/fasttext/dummy/models//AdaBoost.hyp.tag -> ./models/fasttext/dummy/models//AdaBoost.tag.pair
Processing: ./models/fasttext/dummy/models//CRF.hyp.tag -> ./models/fasttext/dummy/models//CRF.tag.pair
Processing: ./models/fasttext/dummy/models//Decision-Tree.hyp.tag -> ./models/fasttext/dummy/models//Decision-Tree.tag.pair
Processing: ./models/fasttext/dummy/models//GradientBoosting.hyp.tag -> ./models/fasttext/dummy/models//GradientBoosting.tag.pair
Processing: ./models/fasttext/dummy/models//Logistic-Regression.hyp.tag -> ./models/fasttext/dummy/models//Logistic-Regression.tag.pair
Processing: ./models/fasttext/dummy/models//MLP.hyp.tag -> ./models/fasttext/dummy/models//MLP.tag.pair
Processing: ./models/fasttext/dummy/models//Random-Forest.hyp.tag -> ./models/fasttext/dummy/models//Random-Forest.tag.pair
Processing: ./models/fasttext/dummy/models//Voting.hyp.tag -> ./models/fasttext/dummy/models//Voting.tag.pair
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

Check paired files ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ ll -h *.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 AdaBoost.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 CRF.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 Decision-Tree.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 GradientBoosting.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 Logistic-Regression.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 MLP.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 Random-Forest.tag.pair
-rw-rw-r-- 1 ye ye 562K Dec 16 07:47 Voting.tag.pair
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ wc *.tag.pair
   5512  143773  575092 AdaBoost.tag.pair
   5512  143773  575092 CRF.tag.pair
   5512  143773  575092 Decision-Tree.tag.pair
   5512  143773  575092 GradientBoosting.tag.pair
   5512  143773  575092 Logistic-Regression.tag.pair
   5512  143773  575092 MLP.tag.pair
   5512  143773  575092 Random-Forest.tag.pair
   5512  143773  575092 Voting.tag.pair
  44096 1150184 4600736 total
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/dummy/models$ head -n 1 *.tag.pair
==> AdaBoost.tag.pair <==
O/B O/O O/O O/O O/O O/N O/N O/N N/E

==> CRF.tag.pair <==
B/B O/O O/O O/O O/O O/N O/N N/N E/E

==> Decision-Tree.tag.pair <==
O/B O/O O/O O/O O/O O/N O/N O/N N/E

==> GradientBoosting.tag.pair <==
O/B O/O O/O O/O O/O O/N O/N O/N N/E

==> Logistic-Regression.tag.pair <==
O/B O/O O/O O/O O/O O/N O/N O/N N/E

==> MLP.tag.pair <==
O/B O/O O/O O/O O/O O/N O/N O/N N/E

==> Random-Forest.tag.pair <==
O/B O/O O/O O/O O/O O/N O/N O/N N/E

==> Voting.tag.pair <==
O/B O/O O/O O/O O/O O/N O/N O/N N/E
```

## Evaluation with Error-Correction Model (i.e. Final Result)    

Prepare a bash shell script for evaluation with 2nd model or error-correction models ...  

```bash
#!/bin/bash

# Usage: ./evaluate4all.sh --folder <folder_path> --extension <file_extension>

# Function to display usage
function usage() {
    echo "Usage: $0 --folder <folder_path> --extension <file_extension>"
    exit 1
}

# Parse command-line arguments
while [[ $# -gt 0 ]]; do
    case $1 in
        --folder)
            FOLDER_PATH="$2"
            shift 2
            ;;
        --extension)
            FILE_EXTENSION="$2"
            shift 2
            ;;
        *)
            usage
            ;;
    esac
done

# Check if all required arguments are provided
if [[ -z "$FOLDER_PATH" || -z "$FILE_EXTENSION" ]]; then
    usage
fi

# Ensure the folder exists
if [[ ! -d "$FOLDER_PATH" ]]; then
    echo "Error: Folder '$FOLDER_PATH' does not exist."
    exit 1
fi

# Loop through files with the specified extension in the folder
for FILE in "$FOLDER_PATH"/*."$FILE_EXTENSION"; do
    # Check if any file matches the pattern
    if [[ ! -f "$FILE" ]]; then
        echo "No files with extension '$FILE_EXTENSION' found in folder '$FOLDER_PATH'."
        exit 1
    fi

    # Run the Python evaluation command
    echo "Processing file: $FILE"
    python evaluate.py "$FILE" --confusion

done

```

run evaluation ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./evaluate4all.sh --folder ./models/fasttext/dummy/models/ --extension tag.pair
Processing file: ./models/fasttext/dummy/models//AdaBoost.tag.pair
Tag-wise Metrics:
O: Precision: 0.8009, Recall: 0.9832, F1-Score: 0.8827
B: Precision: 0.0000, Recall: 0.0000, F1-Score: 0.0000
N: Precision: 0.6222, Recall: 0.0728, F1-Score: 0.1303
E: Precision: 0.7131, Recall: 0.6264, F1-Score: 0.6670

Overall Accuracy: 0.7944
Overall F1-Score: 0.4200

Confusion Matrix:
        B       E       N       O
B       0       29      8       6824
E       0       4278    494     2057
N       0       203     1436    18089
O       0       1489    370     108496
Processing file: ./models/fasttext/dummy/models//CRF.tag.pair
Tag-wise Metrics:
B: Precision: 0.9899, Recall: 0.8567, F1-Score: 0.9185
O: Precision: 0.8972, Recall: 0.9944, F1-Score: 0.9433
N: Precision: 0.9378, Recall: 0.4560, F1-Score: 0.6136
E: Precision: 0.9895, Recall: 0.8594, F1-Score: 0.9199

Overall Accuracy: 0.9076
Overall F1-Score: 0.8488

Confusion Matrix:
        B       E       N       O
B       5878    2       27      954
E       4       5869    18      938
N       26      27      8996    10679
O       30      33      552     109740
Processing file: ./models/fasttext/dummy/models//Decision-Tree.tag.pair
Tag-wise Metrics:
O: Precision: 0.8263, Recall: 0.9584, F1-Score: 0.8874
B: Precision: 0.5583, Recall: 0.1883, F1-Score: 0.2816
N: Precision: 0.6029, Recall: 0.1841, F1-Score: 0.2820
E: Precision: 0.7087, Recall: 0.7720, F1-Score: 0.7390

Overall Accuracy: 0.8065
Overall F1-Score: 0.5475

Confusion Matrix:
        B       E       N       O
B       1292    22      27      5520
E       3       5272    513     1041
N       72      348     3631    15677
O       947     1797    1852    105759
Processing file: ./models/fasttext/dummy/models//GradientBoosting.tag.pair
Tag-wise Metrics:
O: Precision: 0.8231, Recall: 0.9633, F1-Score: 0.8877
B: Precision: 0.5646, Recall: 0.1676, F1-Score: 0.2585
N: Precision: 0.6211, Recall: 0.1636, F1-Score: 0.2589
E: Precision: 0.7089, Recall: 0.7669, F1-Score: 0.7368

Overall Accuracy: 0.8063
Overall F1-Score: 0.5355

Confusion Matrix:
        B       E       N       O
B       1150    19      21      5671
E       1       5237    507     1084
N       60      347     3227    16094
O       826     1784    1441    106304
Processing file: ./models/fasttext/dummy/models//Logistic-Regression.tag.pair
Tag-wise Metrics:
O: Precision: 0.8139, Recall: 0.9675, F1-Score: 0.8841
B: Precision: 0.5511, Recall: 0.0912, F1-Score: 0.1566
N: Precision: 0.5552, Recall: 0.1270, F1-Score: 0.2067
E: Precision: 0.7152, Recall: 0.7275, F1-Score: 0.7213

Overall Accuracy: 0.7989
Overall F1-Score: 0.4922

Confusion Matrix:
        B       E       N       O
B       626     19      32      6184
E       0       4968    508     1353
N       49      298     2506    16875
O       461     1661    1468    106765
Processing file: ./models/fasttext/dummy/models//MLP.tag.pair
Tag-wise Metrics:
O: Precision: 0.8251, Recall: 0.9603, F1-Score: 0.8875
B: Precision: 0.5684, Recall: 0.1599, F1-Score: 0.2496
N: Precision: 0.6055, Recall: 0.1845, F1-Score: 0.2828
E: Precision: 0.7088, Recall: 0.7672, F1-Score: 0.7368

Overall Accuracy: 0.8065
Overall F1-Score: 0.5392

Confusion Matrix:
        B       E       N       O
B       1097    20      25      5719
E       2       5239    513     1075
N       65      347     3640    15676
O       766     1785    1834    105970
Processing file: ./models/fasttext/dummy/models//Random-Forest.tag.pair
Tag-wise Metrics:
O: Precision: 0.8262, Recall: 0.9590, F1-Score: 0.8876
B: Precision: 0.5684, Recall: 0.1866, F1-Score: 0.2809
N: Precision: 0.6046, Recall: 0.1839, F1-Score: 0.2820
E: Precision: 0.7092, Recall: 0.7720, F1-Score: 0.7393

Overall Accuracy: 0.8069
Overall F1-Score: 0.5475

Confusion Matrix:
        B       E       N       O
B       1280    22      24      5535
E       3       5272    513     1041
N       68      348     3628    15684
O       901     1792    1836    105826
Processing file: ./models/fasttext/dummy/models//Voting.tag.pair
Tag-wise Metrics:
O: Precision: 0.8262, Recall: 0.9590, F1-Score: 0.8876
B: Precision: 0.5686, Recall: 0.1867, F1-Score: 0.2811
N: Precision: 0.6047, Recall: 0.1839, F1-Score: 0.2820
E: Precision: 0.7092, Recall: 0.7720, F1-Score: 0.7393

Overall Accuracy: 0.8069
Overall F1-Score: 0.5475

Confusion Matrix:
        B       E       N       O
B       1281    22      24      5534
E       3       5272    513     1041
N       67      348     3628    15685
O       902     1792    1835    105826
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$

```

CRF နဲ့ CRF-CRF ရလဒ်ကိုပဲ နှိုင်းယှဉ်ကြည့်ခဲ့...  

CRF result:  
```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python evaluate.py ./models/fasttext/CRF.tag.pair --confusion
Tag-wise Metrics:
B: Precision: 0.9899, Recall: 0.8559, F1-Score: 0.9180
O: Precision: 0.8969, Recall: 0.9945, F1-Score: 0.9432
N: Precision: 0.9380, Recall: 0.4543, F1-Score: 0.6122
E: Precision: 0.9887, Recall: 0.8577, F1-Score: 0.9185

Overall Accuracy: 0.9072
Overall F1-Score: 0.8480

Confusion Matrix:
        B       E       N       O
B       5872    7       27      955
E       4       5857    18      950
N       26      27      8963    10712
O       30      33      547     109745
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

CRF-CRF result:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ python evaluate.py ./models/fasttext/dummy/models/CRF.tag.pair --confusion
Tag-wise Metrics:
B: Precision: 0.9899, Recall: 0.8567, F1-Score: 0.9185
O: Precision: 0.8972, Recall: 0.9944, F1-Score: 0.9433
N: Precision: 0.9378, Recall: 0.4560, F1-Score: 0.6136
E: Precision: 0.9895, Recall: 0.8594, F1-Score: 0.9199

Overall Accuracy: 0.9076
Overall F1-Score: 0.8488

Confusion Matrix:
        B       E       N       O
B       5878    2       27      954
E       4       5869    18      938
N       26      27      8996    10679
O       30      33      552     109740
```

ရလဒ် အနေနဲ့က မတက်တဲ့အပြင် နည်းနည်းထပ်ကျသွားတယ်။  
tag only information နဲ့ error-correction လုပ်တာက sentence breaking အတွက် အဆင်မပြေဘူး ဆိုတဲ့ ရလဒ်ပဲ။  

## Thinking

CRF-Rule Combination လုပ်ရင်ကော။  
CRF က ထွက်လာတဲ့ output တော်တော်များများက မှန်တယ်။  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ head -n 5 CRF.hyp
ရင်/B ဘတ်/O အောင့်/O လာ/O ရင်/O သ/O တိ/O ထား/N ပါ/E
ဘယ်/B လောက်/N နောက်/N ကျ/N သ/N လဲ/E
ကြြို/B ပပိပို့/O ဘတ်စ်/O ကား/O က/O အ/O ဆင်/O အ/O ပြေ/N ဆဆုံး/N ပဲ/E
အဲ/B ဒီ/O အ/O ဖွွဲ့/O ရရဲ့/O ဥက္ကဋ္ဌ/O ဖြစ်/O တတဲ့/O ယယို/O ကကို/O ယာ/O မာ့/O အာ/O ကိ/O ဟီ/O တတို/O YokoyamaAkihito/O က/O တ/O ခြား/O နနိုင်/O ငံ/O တွေ/O မှာ/O ဖြစ်/O ပွား/O တတဲ့/O လူ/O နာ/O တွေ/O ရရဲ့/O အ/O ဆုတ်/O လုပ်/O ဆောင်/O ပပုံ/O တွေ/O က/O ဗဗိုင်း/O ရပ်စ်/O ကူး/O စက်/O ခံ/O ရ/O ပြီး/O ကု/O သ/O လလိုက်/O လလိလို့/O ရော/O ဂါ/O ပပိုး/O မ/O ရှိ/O တော့/O ဘူး/O လလိလို့/O စစ်/O ဆေး/O ပြီး/O နောက်/O မှာ/O တောင်/O မှ/O အ/O ဆုတ်/O က/O အ/O ပြည့်/O အ/O ဝ/O ပပုံ/O မှန်/O ပြန်/O ဖြစ်/O မ/O လာ/O တတဲ့/O လ                          လူ                                                                                                       လူ/O နာ/O တွေ/O အ/O များ/O အ/O ပြား/O တွေ့/O ရ/O တယ်/O လလိလို့/O ပြော/N ပါ/N တယ်/E
အ/B ဆင့်/O အေ/O ဝင်/O ငွေ/O ခွန်/O ကကို/O လ/O စာ/O မှ/O ဖြတ်/N တောက်/N သည်/E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ head -n 5 CRF.hyp.tag
B O O O O O O N E
B N N N N E
B O O O O O O O N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N E
B O O O O O O O O O N N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ shuf CRF.hyp.tag | head
B O O O O O O O O O O O O O O O O O O N E
B N N N N N E
B O O O O O O O O O O O O O O O O O N E
B O O O O O O O N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N E
B O O O O O O N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N E B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N N N E
B O O O O O O O O O O O O O O O O O O N E B O O O O O O O O O N E
B O O O O O N N N E
B O O O N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ shuf CRF.hyp.tag | head
B N N E B O O O O O O O O O N E
B N N N N N E
B N E B O O O O O O N E
B O O O O O O O O O O O O O O O O O O O O N N E
B O O O O O O O O O O O O O O O O O O O O O O O O O O O O O N E
B O O N N E
B O O O O O O O O O O O O O O O O O O O O O O N E
B O O O N N E
B O O O O O O O O O O O O O O O O O O O O O O O N E
B O O O O O O N N N E
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext$ shuf CRF.hyp | head
ဂီ/B မစ်ရ်/O လဲ/O ဘယ်/O လောက်/O စွမ်း/O စွမ်း/O မီး/O လျှံ/O ဘဘုံ/O က/O မီး/O မိစ္ဆာ/O ကြီး/O ဆာ/O တာ/Oရဲ့/O မီး/O ဓါး/O နနဲ့/O တောင်/O ယှ/O ဉ်/O နနိုင်/O တတဲ့/O ဖ/O ရေး/O ရရဲ့/O ဓါး/O ကကို/O ဘယ်/O နနိုင်/O မ/O လဲ/O အဲ/O လလို/O ပြော/O လလိုက်/O တော့/O ဂါ့ဒ်/O တွေ/O ဝေ/O သွား/N တယ်/E
မမိုး/B ရွာ/O ပြီး/O တတဲ့/O နောက်/O မြေ/O ကြီး/O က/O မာ/O ကျော/O လာ/N တယ်/E
အေး/B ကောင်း/N တယ်/E ကောင်း/B တယ်/O ငွေ/O လဲ/O နှုန်း/O က/O ကော/O ဘယ်/O လလို/O အ/O ခြေ/O အ/O နေ/N လဲ/E
ဒေါ်/B မြ/O က/O မ/O နှစ်/O က/O သ/O မီး/O လေး/O ကကို/O အိမ်/O ထောင်/O ချ/O ပေး/O လလိုက်/O ပြီး/O တော့/O တစ်/O ယောက်/O တည်း/O နေ/N နေ/N တယ်/E
အ/B ခု/O အ/O အေး/O မိ/O လလိလို့/O လည်/O ချောင်း/O လည်း/O နာ/O ပြီး/O ခေါင်း/O လည်း/O ကကိုက်/N တယ်/E
ရန်/B ကုန်/O မြြိြို့/O မှာ/O မမိုး/O လလုံ/O လေ/O လလုံ/O အား/O က/O စား/O ရရုံ/O ရှိ/O သ/N လား/E
လဲ/B နေ/O စ/O ရာ/O ထထိုင်/O ခခုံ/O ရှိ/N လား/E
ကြီး/B မား/O တတဲ့/O မြွေ/O ကြီး/O တစ်/N ကောင်/E
မင်း/B ရော/O ကျွန်/O တော်/O လည်း/O မ/O ရှိ/N ပါ/E
ခင်/B ဗျား/O ဒါ/O လေး/O တောင်/O မ/O တတ်/N ဘူး/E
```

