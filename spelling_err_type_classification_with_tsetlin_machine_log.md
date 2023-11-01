# Spelling Error Type Classification with Tsetlin Machine

## pyTsetlinMachine Installation

Current Python version:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ python --version
Python 3.9.12
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Python enviornment အသစ် ဘာညာ မဆောက်တော့ပဲနဲ့ လက်ရှိ python version 3.9.12 အောက်မှာပဲ run ဖို့ ဆုံးဖြတ်ခဲ့တယ်။  
Python library ပဲ installation လုပ်လိုက်တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ pip install pyTsetlinMachine
Collecting pyTsetlinMachine
  Using cached pyTsetlinMachine-0.6.4.tar.gz (24 kB)
Building wheels for collected packages: pyTsetlinMachine
  Building wheel for pyTsetlinMachine (setup.py) ... done
  Created wheel for pyTsetlinMachine: filename=pyTsetlinMachine-0.6.4-cp39-cp39-linux_x86_64.whl size=23099 sha256=347c7203fdf0c83d8e6db61d21d5c70befe967bda3c34b8f845d0bb23489d95b
  Stored in directory: /home/ye/.cache/pip/wheels/9e/cd/16/acb627a7ec3f28d7385b6c5e5c496029c8ec98b74588888887
Successfully built pyTsetlinMachine
Installing collected packages: pyTsetlinMachine
Successfully installed pyTsetlinMachine-0.6.4
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$
```

Library call testing ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/fasttext$ python
Python 3.9.12 (main, Apr  5 2022, 06:56:58)
[GCC 7.5.0] :: Anaconda, Inc. on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from pyTsetlinMachine.tm import MultiClassTsetlinMachine
>>>
>>>
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ library ကိုတော့ သိသွားပြီ။  

## Testing Example Code

Example code နဲ့ Tsetlin Machine က ကိုယ့်စက်ထဲမှာ အလုပ်လုပ်မလုပ် အရင်ဆုံး စမ်းဖို့အတွက် XOR training data နဲ့ test data ကို download လုပ်ဖို့ လိုအပ်တယ်။  


```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$ wget https://raw.githubusercontent.com/cair/pyTsetlinMachine/master/examples/NoisyXORTrainingData.txt
--2023-11-01 12:31:55--  https://raw.githubusercontent.com/cair/pyTsetlinMachine/master/examples/NoisyXORTrainingData.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.109.133, 185.199.110.133, 185.199.111.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.109.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 130000 (127K) [text/plain]
Saving to: ‘NoisyXORTrainingData.txt’

NoisyXORTrainingData.t 100%[==========================>] 126.95K  --.-KB/s    in 0.007s

2023-11-01 12:31:56 (18.9 MB/s) - ‘NoisyXORTrainingData.txt’ saved [130000/130000]

(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$
```

testing data ကိုလည်း အောက်ပါအတိုင်း download လုပ်ခဲ့တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$ wget https://raw.githubusercontent.com/cair/pyTsetlinMachine/master/examples/NoisyXORTestData.txt
--2023-11-01 12:31:27--  https://raw.githubusercontent.com/cair/pyTsetlinMachine/master/examples/NoisyXORTestData.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.110.133, 185.199.109.133, 185.199.108.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.110.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 130000 (127K) [text/plain]
Saving to: ‘NoisyXORTestData.txt’

NoisyXORTestData.txt   100%[==========================>] 126.95K  --.-KB/s    in 0.007s

2023-11-01 12:31:28 (18.4 MB/s) - ‘NoisyXORTestData.txt’ saved [130000/130000]

(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$
```

Training data format က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$ head -n 5 ./NoisyXORTrainingData.txt
0 1 1 0 0 0 0 1 1 1 1 0 0
0 1 0 1 1 1 0 1 1 1 1 0 1
0 0 1 1 0 0 0 1 1 1 1 1 1
0 1 0 0 1 1 0 1 0 0 0 0 1
0 0 0 0 0 1 1 1 0 1 1 0 1
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$
```

Test data format က အောက်ပါအတိုင်း ...  
 

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$ head ./NoisyXORTestData.txt
0 1 1 0 0 1 1 0 1 1 1 1 1
0 0 1 0 0 1 1 0 1 0 1 0 0
0 0 0 1 0 0 0 1 0 0 1 0 0
1 0 1 0 0 1 0 1 0 0 1 0 1
0 0 1 0 0 1 1 0 0 0 0 1 0
0 0 0 0 1 0 1 1 1 0 1 0 0
1 0 1 1 0 0 0 0 0 1 0 0 1
1 1 0 1 0 1 1 0 0 0 1 1 0
0 0 0 1 0 1 0 0 0 0 0 1 0
1 1 0 0 0 1 1 1 0 1 1 0 0
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$
```

filesize information က အောက်ပါအတိုင်းပါ။  


```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$ wc NoisyXORTrainingData.txt
  5000  65000 130000 NoisyXORTrainingData.txt
```

for test data:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$ wc NoisyXORTestData.txt
  5000  65000 130000 NoisyXORTestData.txt
```

Tsetlin Machine Python GitHub မှာ ရေးပြထားတဲ့ source code က အောက်ပါအတိုင်းပါ။  

```python
from pyTsetlinMachine.tm import MultiClassTsetlinMachine
import numpy as np

train_data = np.loadtxt("NoisyXORTrainingData.txt")
X_train = train_data[:,0:-1]
Y_train = train_data[:,-1]

test_data = np.loadtxt("NoisyXORTestData.txt")
X_test = test_data[:,0:-1]
Y_test = test_data[:,-1]

tm = MultiClassTsetlinMachine(10, 15, 3.9, boost_true_positive_feedback=0)

tm.fit(X_train, Y_train, epochs=200)

print("Accuracy:", 100*(tm.predict(X_test) == Y_test).mean())

print("Prediction: x1 = 1, x2 = 0, ... -> y = %d" % (tm.predict(np.array([[1,0,1,0,1,0,1,1,1,1,0,0]]))))
print("Prediction: x1 = 0, x2 = 1, ... -> y = %d" % (tm.predict(np.array([[0,1,1,0,1,0,1,1,1,1,0,0]]))))
print("Prediction: x1 = 0, x2 = 0, ... -> y = %d" % (tm.predict(np.array([[0,0,1,0,1,0,1,1,1,1,0,0]]))))
print("Prediction: x1 = 1, x2 = 1, ... -> y = %d" % (tm.predict(np.array([[1,1,1,0,1,0,1,1,1,1,0,0]]))))
```

Tsetlin Machine Test run with XOR data:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$ time python ./NoisyXORDemo.py | tee runNo
isyXORDemo.log
Accuracy: 100.0
Prediction: x1 = 1, x2 = 0, ... -> y = 1
Prediction: x1 = 0, x2 = 1, ... -> y = 1
Prediction: x1 = 0, x2 = 0, ... -> y = 0
Prediction: x1 = 1, x2 = 1, ... -> y = 0

real    0m1.090s
user    0m1.782s
sys     0m1.863s
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin/eg$
```

XOR Demo code ကတော့ ကောင်းကောင်း အလုပ်လုပ်တယ်။  

## Coding for Our Error Type Classification

ငါတို့ရဲ့ ဒေတာ format က အောက်ပါအတိုင်း ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ head error_type.train
__label__typo ကျော် နိင် ပါ
__label__seq ေ န ကို
__label__typo ငယ် ချ ငိး ရေ
__label__pho ထား တ ခု
__label__pho __label__typo သန်း မှု့ တွေ
__label__typo တာ ပဲ့ မြင်
__label__pho ကို ပစ် ဒဏ်
__label__pho တာ တ ခါ
__label__pho အ မ
__label__stack တယ် သ ဘော် သီး
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

Tsetlin machine က အခြေခံအားဖြင့်က binary classification ပြီးတော့ သူက text data input ကို လက်ခံတာ မဟုတ်ဘူး။ အဲဒါကြောင့် preprocessing ကိစ္စကိုပါ ထည့်သွင်းစဉ်းစားရတယ်။  

အခါခါ coding လုပ်၊ test run လုပ်ပြီး အလုပ်လုပ်ပေးနိုင်တဲ့ python code တော့ ရလာပြီ။  

```python
import numpy as np
import argparse
from pyTsetlinMachine.tm import MultiClassTsetlinMachine
from sklearn.preprocessing import MultiLabelBinarizer
from sklearn.feature_extraction.text import CountVectorizer
import joblib

def save_model(filename, tm):
    joblib.dump(tm, filename)

def load_model(filename):
    return joblib.load(filename)

def load_data(file_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        lines = f.readlines()
    data, labels = [], []
    for line in lines:
        label, text = line.strip().split(' ', 1)
        data.append(text)
        labels.append(label.split())
    return data, labels

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--mode', help='train or test', default='train')
    parser.add_argument('--train_data', help='path to training data file', default='data/train.txt')
    parser.add_argument('--test_data', help='path to test data file', default='data/test.txt')
    parser.add_argument('--model_name', help='path to save/load model', default='model')
    parser.add_argument('--clauses', help='number of clauses', type=int, default=20)
    parser.add_argument('--T', help='threshold', type=int, default=15)
    parser.add_argument('--s', help='s', type=float, default=3.9)
    args = parser.parse_args()

    vectorizer = CountVectorizer(analyzer='char', ngram_range=(1, 3))
    mlb = MultiLabelBinarizer()

    if args.mode == 'train':
        train_data, train_labels = load_data(args.train_data)
        train_data = vectorizer.fit_transform(train_data).toarray()  # Convert to dense matrix
        train_labels = mlb.fit_transform(train_labels)

        num_classes = len(mlb.classes_)
        tm = MultiClassTsetlinMachine(args.clauses, args.T, args.s)
        tm.fit(train_data, np.argmax(train_labels, axis=1), epochs=100)  # Train for 100 epochs as an example

        save_model(args.model_name + '.joblib', tm)  # Updated line
        joblib.dump(vectorizer, args.model_name + '_vectorizer.pkl')  # Save the vectorizer
        joblib.dump(mlb, args.model_name + '_mlb.pkl')  # Save the multi-label binarizer

        print(f'Model trained and saved as {args.model_name}.joblib')

    elif args.mode == 'test':
        if args.test_data is None:
            print('Please provide the testing data path using --test_data argument')
            return

        test_data, test_labels = load_data(args.test_data)
        vectorizer = joblib.load(args.model_name + '_vectorizer.pkl')  # Load the vectorizer
        mlb = joblib.load(args.model_name + '_mlb.pkl')  # Load the multi-label binarizer
        test_data = vectorizer.transform(test_data).toarray()  # Convert to dense matrix
        test_labels = mlb.transform(test_labels)

        tm = load_model(args.model_name + '.joblib')  # Updated line

        accuracy = 100*(tm.predict(test_data) == np.argmax(test_labels, axis=1)).mean()  # Updated line
        print(f'Accuracy: {accuracy:.2f}%')

if __name__ == '__main__':
    main()
```

command line argument တွေက အောက်ပါအတိုင်း ...

```
$ python ./tsetlin_classifier.py --help
usage: tsetlin_classifier.py [-h] [--mode MODE] [--train_data TRAIN_DATA]
                             [--test_data TEST_DATA] [--model_name MODEL_NAME]
                             [--clauses CLAUSES] [--T T] [--s S]

optional arguments:
  -h, --help            show this help message and exit
  --mode MODE           train or test
  --train_data TRAIN_DATA
                        path to training data file
  --test_data TEST_DATA
                        path to test data file
  --model_name MODEL_NAME
                        path to save/load model
  --clauses CLAUSES     number of clauses
  --T T                 threshold
  --s S                 s
```

Prepare small training/testing data as follows:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ head -n 5000 error_type.train > error_type.5k.train
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ head -n 100 error_type.valid > error_type.100.valid
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

Training with 5K data:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ time python ./tsetlin_classifier.py --mode train --train_data ./error_type.5k.train --model_name error_type.5k.model
Model trained and saved as error_type.5k.model.joblib

real    1m0.615s
user    1m0.918s
sys     0m2.067s
```

Testing with 100 error sentences data:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ time python ./tsetlin_classifier.py --mode test --model_name error_type.5k.model --test_data ./error_type.100.valid
Accuracy: 56.00%

real    0m0.379s
user    0m1.020s
sys     0m1.897s
```

ဒီတစ်ခါတော့ small corpus/test_data နဲ့တော့ အလုပ်လုပ်သွားပြီ။ သို့သော် hyp ဖိုင်ကို save လုပ်တာ မလုပ်ရသေးဘူး။ ပြီးတော့ --epoch argument parameter မထည့်ရသေးဘူး။ Accuracy အပြင် တကယ်တမ်းက F1, P, R တွေလည်း ထည့်ဖို့ လိုအပ်တယ်။ အဲဒါနဲ့ coding ကို update ထပ်လုပ်ခဲ့။  


```python
import numpy as np
import argparse
from pyTsetlinMachine.tm import MultiClassTsetlinMachine
from sklearn.preprocessing import MultiLabelBinarizer
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.metrics import accuracy_score, f1_score, precision_score, recall_score
import joblib

def save_model(filename, tm):
    joblib.dump(tm, filename)

def load_model(filename):
    return joblib.load(filename)

def load_data(file_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        lines = f.readlines()
    data, labels = [], []
    for line in lines:
        label, text = line.strip().split(' ', 1)
        data.append(text)
        labels.append(label.split())
    return data, labels

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--mode', help='train or test', default='train')
    parser.add_argument('--train_data', help='path to training data file', default='data/train.txt')
    parser.add_argument('--test_data', help='path to test data file', default='data/test.txt')
    parser.add_argument('--model_name', help='path to save/load model', default='model')
    parser.add_argument('--hypothesis_filename', help='path to save hypothesis file', default='hypothesis.txt')
    parser.add_argument('--clauses', help='number of clauses', type=int, default=20)
    parser.add_argument('--T', help='threshold', type=int, default=15)
    parser.add_argument('--s', help='s', type=float, default=3.9)
    parser.add_argument('--epoch', help='number of epochs', type=int, default=100)
    args = parser.parse_args()

    vectorizer = CountVectorizer(analyzer='char', ngram_range=(1, 3))
    mlb = MultiLabelBinarizer()

    if args.mode == 'train':
        train_data, train_labels = load_data(args.train_data)
        train_data = vectorizer.fit_transform(train_data).toarray()  # Convert to dense matrix
        train_labels = mlb.fit_transform(train_labels)

        num_classes = len(mlb.classes_)
        tm = MultiClassTsetlinMachine(args.clauses, args.T, args.s)
        for epoch in range(args.epoch):
            tm.fit(train_data, np.argmax(train_labels, axis=1), epochs=1)  # Train for 1 epoch at a time
            # Calculate and display metrics after each epoch
            predictions = tm.predict(train_data)
            accuracy = accuracy_score(np.argmax(train_labels, axis=1), predictions)
            f1 = f1_score(np.argmax(train_labels, axis=1), predictions, average='weighted')
            precision = precision_score(np.argmax(train_labels, axis=1), predictions, average='weighted')
            recall = recall_score(np.argmax(train_labels, axis=1), predictions, average='weighted')
            print(f'Epoch {epoch + 1}/{args.epoch}, Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        save_model(args.model_name + '.joblib', tm)  # Updated line
        joblib.dump(vectorizer, args.model_name + '_vectorizer.pkl')  # Save the vectorizer
        joblib.dump(mlb, args.model_name + '_mlb.pkl')  # Save the multi-label binarizer

        print(f'Model trained and saved as {args.model_name}.joblib')

    elif args.mode == 'test':
        if args.test_data is None:
            print('Please provide the testing data path using --test_data argument')
            return

        test_data, test_labels = load_data(args.test_data)
        vectorizer = joblib.load(args.model_name + '_vectorizer.pkl')  # Load the vectorizer
        mlb = joblib.load(args.model_name + '_mlb.pkl')  # Load the multi-label binarizer
        test_data = vectorizer.transform(test_data).toarray()  # Convert to dense matrix
        test_labels = mlb.transform(test_labels)

        tm = load_model(args.model_name + '.joblib')  # Updated line

        predictions = tm.predict(test_data)
        # Calculate and display metrics
        accuracy = accuracy_score(np.argmax(test_labels, axis=1), predictions)
        f1 = f1_score(np.argmax(test_labels, axis=1), predictions, average='weighted')
        precision = precision_score(np.argmax(test_labels, axis=1), predictions, average='weighted')
        recall = recall_score(np.argmax(test_labels, axis=1), predictions, average='weighted')
        print(f'Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        # Save the hypothesis file
        with open(args.hypothesis_filename, 'w') as f:
            for prediction in predictions:
                f.write(f'{prediction}\n')

        print(f'Test results saved as {args.hypothesis_filename}')

if __name__ == '__main__':
    main()

```

--help ခေါ်ကြည့်ရင် အောက်ပါအတိုင်း command line argument အသစ်တွေကို တွေ့ရလိမ့်မယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ python ./tsetlin_classifier.py --help
usage: tsetlin_classifier.py [-h] [--mode MODE] [--train_data TRAIN_DATA]
                             [--test_data TEST_DATA] [--model_name MODEL_NAME]
                             [--hypothesis_filename HYPOTHESIS_FILENAME]
                             [--clauses CLAUSES] [--T T] [--s S] [--epoch EPOCH]

optional arguments:
  -h, --help            show this help message and exit
  --mode MODE           train or test
  --train_data TRAIN_DATA
                        path to training data file
  --test_data TEST_DATA
                        path to test data file
  --model_name MODEL_NAME
                        path to save/load model
  --hypothesis_filename HYPOTHESIS_FILENAME
                        path to save hypothesis file
  --clauses CLAUSES     number of clauses
  --T T                 threshold
  --s S                 s
  --epoch EPOCH         number of epochs
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

shell script တစ်ပုဒ် ပြင်လိုက်တယ်။  

```bash
#!/bin/bash

echo "Training with 5K data ..."
time python ./tsetlin_classifier.py --mode train --train_data ./error_type.5k.train --model_name error_type.5k.model --epoch 100

echo "==============="
echo "Testing with 100 errors ..."
time python ./tsetlin_classifier.py --mode test --model_name error_type.5k.model --test_data ./error_type.100.valid --hypothesis_filename ./error_type.100.hyp
```

run ရတာ အဆင်ပြေအောင် executable mode ပြောင်းထားလိုက်တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ chmod +x ./train_test.sh
```
 
Training/Testing again with updated python program ...  
5K ဒေတာနဲ့ပဲ အရင်စမ်းခဲ့တယ်။  

Running log က အောက်ပါအတိုင်းပဲ ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ ./train_test.sh
...
...
...
Epoch 83/100, Accuracy: 0.44, F1 Score: 0.41, Precision: 0.40, Recall: 0.44
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 84/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.40, Recall: 0.47
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 85/100, Accuracy: 0.48, F1 Score: 0.43, Precision: 0.41, Recall: 0.48
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 86/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.43, Recall: 0.47
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 87/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.43, Recall: 0.46
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 88/100, Accuracy: 0.46, F1 Score: 0.41, Precision: 0.40, Recall: 0.46
Epoch 89/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.42, Recall: 0.47
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 90/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.42, Recall: 0.48
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 91/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.43, Recall: 0.48
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 92/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.44, Recall: 0.48
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 93/100, Accuracy: 0.42, F1 Score: 0.40, Precision: 0.39, Recall: 0.42
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 94/100, Accuracy: 0.45, F1 Score: 0.42, Precision: 0.41, Recall: 0.45
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 95/100, Accuracy: 0.46, F1 Score: 0.42, Precision: 0.40, Recall: 0.46
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 96/100, Accuracy: 0.46, F1 Score: 0.41, Precision: 0.40, Recall: 0.46
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 97/100, Accuracy: 0.49, F1 Score: 0.45, Precision: 0.44, Recall: 0.49
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 98/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.42, Recall: 0.48
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Epoch 99/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.46, Recall: 0.47
Epoch 100/100, Accuracy: 0.46, F1 Score: 0.44, Precision: 0.44, Recall: 0.46
Model trained and saved as error_type.5k.model.joblib

real    2m57.032s
user    2m52.036s
sys     0m6.917s
===============
Testing with 100 errors ...
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Precision is ill-defined and being set to 0.0 in labels with no predicted samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/metrics/_classification.py:1469: UndefinedMetricWarning: Recall is ill-defined and being set to 0.0 in labels with no true samples. Use `zero_division` parameter to control this behavior.
  _warn_prf(average, modifier, msg_start, len(result))
Accuracy: 0.49, F1 Score: 0.48, Precision: 0.47, Recall: 0.49
Test results saved as ./error_type.100.hyp

real    0m0.372s
user    0m0.981s
sys     0m1.942s
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

Check the hyp file ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ head error_type.100.hyp
3
3
3
3
3
3
9
3
3
3
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

filesize:  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ wc ./error_type.100.hyp
100 100 200 ./error_type.100.hyp
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

အရင်ဆုံး လက်ရှိ code ကို backup ကူးထားလိုက်တယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ cp ./tsetlin_classifier.py ./bk/tsetlin_classifier.py.ver1
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

## Updating the Tsetlin Classifier Code

လက်ရှိ code က 5K ဒေတာနဲ့ စမ်းထားသလောက် အလုပ်က လုပ်နေပြီ သို့သော် training လုပ်နေတဲ့အချိန်မှာ warning message တွေကပါ ရောပါနေလို့ progress report ကို ဖတ်ရတာ အဆင်မပြေဘူး။ ပြီးတော့ hyp ဖိုင်ရဲ့ output က code နဲ့ပဲ ထွက်သေးတာမို့လို့ အဲဒါကို human readable ဖြစ်အောင် ပြင်လိုက်တာက ပိုကောင်းတယ်။ အဲဒါမှာ ကိုယ့်ဖာသာကိုယ်လည်း မျက်လုံးနဲ့ confirm လုပ်လို့ ရလိမ့်မယ်။  

```python
import numpy as np
import argparse
from pyTsetlinMachine.tm import MultiClassTsetlinMachine
from sklearn.preprocessing import MultiLabelBinarizer
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.metrics import accuracy_score, f1_score, precision_score, recall_score
import joblib

def save_model(filename, tm):
    joblib.dump(tm, filename)

def load_model(filename):
    return joblib.load(filename)

def load_data(file_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        lines = f.readlines()
    data, labels = [], []
    for line in lines:
        label, text = line.strip().split(' ', 1)
        data.append(text)
        labels.append(label.split())
    return data, labels

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--mode', help='train or test', default='train')
    parser.add_argument('--train_data', help='path to training data file', default='data/train.txt')
    parser.add_argument('--test_data', help='path to test data file', default='data/test.txt')
    parser.add_argument('--model_name', help='path to save/load model', default='model')
    parser.add_argument('--hypothesis_filename', help='path to save hypothesis file', default='hypothesis.txt')
    parser.add_argument('--clauses', help='number of clauses', type=int, default=20)
    parser.add_argument('--T', help='threshold', type=int, default=15)
    parser.add_argument('--s', help='s', type=float, default=3.9)
    parser.add_argument('--epoch', help='number of epochs', type=int, default=100)
    args = parser.parse_args()

    vectorizer = CountVectorizer(analyzer='char', ngram_range=(1, 3))
    mlb = MultiLabelBinarizer()

    if args.mode == 'train':
        train_data, train_labels = load_data(args.train_data)
        train_data = vectorizer.fit_transform(train_data).toarray()  # Convert to dense matrix
        train_labels = mlb.fit_transform(train_labels)

        num_classes = len(mlb.classes_)
        tm = MultiClassTsetlinMachine(args.clauses, args.T, args.s)
        for epoch in range(args.epoch):
            tm.fit(train_data, np.argmax(train_labels, axis=1), epochs=1)  # Train for 1 epoch at a time
            # Calculate and display metrics after each epoch
            predictions = tm.predict(train_data)
            accuracy = accuracy_score(np.argmax(train_labels, axis=1), predictions)
            f1 = f1_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            precision = precision_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            recall = recall_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            print(f'Epoch {epoch + 1}/{args.epoch}, Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        save_model(args.model_name + '.joblib', tm)  # Updated line
        joblib.dump(vectorizer, args.model_name + '_vectorizer.pkl')  # Save the vectorizer
        joblib.dump(mlb, args.model_name + '_mlb.pkl')  # Save the multi-label binarizer

        print(f'Model trained and saved as {args.model_name}.joblib')

    elif args.mode == 'test':
        if args.test_data is None:
            print('Please provide the testing data path using --test_data argument')
            return

        test_data, test_labels = load_data(args.test_data)
        vectorizer = joblib.load(args.model_name + '_vectorizer.pkl')  # Load the vectorizer
        mlb = joblib.load(args.model_name + '_mlb.pkl')  # Load the multi-label binarizer
        test_data = vectorizer.transform(test_data).toarray()  # Convert to dense matrix
        test_labels = mlb.transform(test_labels)

        tm = load_model(args.model_name + '.joblib')  # Updated line

        predictions = tm.predict(test_data)
        # Convert numerical labels back to original labels
        original_labels = mlb.inverse_transform(predictions.reshape(-1, 1))
        # Calculate and display metrics
        accuracy = accuracy_score(np.argmax(test_labels, axis=1), predictions)
        f1 = f1_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        precision = precision_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        recall = recall_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        print(f'Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        # Save the hypothesis file
        with open(args.hypothesis_filename, 'w') as f:
            for label_set in original_labels:
                f.write(' '.join(label_set) + '\n')

        print(f'Test results saved as {args.hypothesis_filename}')

if __name__ == '__main__':
    main()

```

update လုပ်ထားတဲ့ python code နဲ့ ထပ် training/testing လုပ်ကြည့်ခဲ့ ...  
ဒီတစ်ခါလည်း 5K ဒေတာနဲ့ပဲ training ပါ။  
Testing အပိုင်းမှာ အောက်ပါအတိုင်း error တက်နေသေးတယ် ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ ./train_test.sh | tee 5K_train_test.log
...
...
...
Epoch 94/100, Accuracy: 0.45, F1 Score: 0.42, Precision: 0.41, Recall: 0.45
Epoch 95/100, Accuracy: 0.46, F1 Score: 0.42, Precision: 0.40, Recall: 0.46
Epoch 96/100, Accuracy: 0.46, F1 Score: 0.41, Precision: 0.40, Recall: 0.46
Epoch 97/100, Accuracy: 0.49, F1 Score: 0.45, Precision: 0.44, Recall: 0.49
Epoch 98/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.42, Recall: 0.48
Epoch 99/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.46, Recall: 0.47
Epoch 100/100, Accuracy: 0.46, F1 Score: 0.44, Precision: 0.44, Recall: 0.46
Model trained and saved as error_type.5k.model.joblib

real    2m57.595s
user    2m52.732s
sys     0m7.200s
===============
Testing with 100 errors ...
Traceback (most recent call last):
  File "/home/ye/exp/mySpell/tsetlin/./tsetlin_classifier.py", line 95, in <module>
    main()
  File "/home/ye/exp/mySpell/tsetlin/./tsetlin_classifier.py", line 79, in main
    original_labels = mlb.inverse_transform(predictions.reshape(-1, 1))
  File "/home/ye/anaconda3/lib/python3.9/site-packages/sklearn/preprocessing/_label.py", line 926, in inverse_transform
    raise ValueError(
ValueError: Expected indicator for 10 classes, but got 1

real    0m0.390s
user    0m0.936s
sys     0m1.987s
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

updated python code is as follows:  

```python
## Tsetlin Machine for Burmese spelling error type classification
## Written by Ye Kyaw Thu, LU Lab., Myanmar
## Last updated: 1 Nov 2023
## Preparation for the 5th NLP/AI Workshop, Bangkok, Thailand

import numpy as np
import argparse
from pyTsetlinMachine.tm import MultiClassTsetlinMachine
from sklearn.preprocessing import MultiLabelBinarizer
from sklearn.feature_extraction.text import CountVectorizer
from sklearn.metrics import accuracy_score, f1_score, precision_score, recall_score
import joblib

def save_model(filename, tm):
    joblib.dump(tm, filename)

def load_model(filename):
    return joblib.load(filename)

def load_data(file_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        lines = f.readlines()
    data, labels = [], []
    for line in lines:
        label, text = line.strip().split(' ', 1)
        data.append(text)
        labels.append(label.split())
    return data, labels

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--mode', help='train or test', default='train')
    parser.add_argument('--train_data', help='path to training data file', default='data/train.txt')
    parser.add_argument('--test_data', help='path to test data file', default='data/test.txt')
    parser.add_argument('--model_name', help='path to save/load model', default='model')
    parser.add_argument('--hypothesis_filename', help='path to save hypothesis file', default='hypothesis.txt')
    parser.add_argument('--clauses', help='number of clauses', type=int, default=20)
    parser.add_argument('--T', help='threshold', type=int, default=15)
    parser.add_argument('--s', help='s', type=float, default=3.9)
    parser.add_argument('--epoch', help='number of epochs', type=int, default=100)
    args = parser.parse_args()

    vectorizer = CountVectorizer(analyzer='char', ngram_range=(1, 3))
    mlb = MultiLabelBinarizer()

    if args.mode == 'train':
        train_data, train_labels = load_data(args.train_data)
        train_data = vectorizer.fit_transform(train_data).toarray()  # Convert to dense matrix
        train_labels = mlb.fit_transform(train_labels)

        num_classes = len(mlb.classes_)
        tm = MultiClassTsetlinMachine(args.clauses, args.T, args.s)
        for epoch in range(args.epoch):
            tm.fit(train_data, np.argmax(train_labels, axis=1), epochs=1)  # Train for 1 epoch at a time
            # Calculate and display metrics after each epoch
            predictions = tm.predict(train_data)
            accuracy = accuracy_score(np.argmax(train_labels, axis=1), predictions)
            f1 = f1_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            precision = precision_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            recall = recall_score(np.argmax(train_labels, axis=1), predictions, average='weighted', zero_division=0)
            print(f'Epoch {epoch + 1}/{args.epoch}, Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        save_model(args.model_name + '.joblib', tm)  # Updated line
        joblib.dump(vectorizer, args.model_name + '_vectorizer.pkl')  # Save the vectorizer
        joblib.dump(mlb, args.model_name + '_mlb.pkl')  # Save the multi-label binarizer

        print(f'Model trained and saved as {args.model_name}.joblib')

    elif args.mode == 'test':
        if args.test_data is None:
            print('Please provide the testing data path using --test_data argument')
            return

        test_data, test_labels = load_data(args.test_data)
        vectorizer = joblib.load(args.model_name + '_vectorizer.pkl')  # Load the vectorizer
        mlb = joblib.load(args.model_name + '_mlb.pkl')  # Load the multi-label binarizer
        test_data = vectorizer.transform(test_data).toarray()  # Convert to dense matrix
        test_labels = mlb.transform(test_labels)

        tm = load_model(args.model_name + '.joblib')  # Updated line

        predictions = tm.predict(test_data)
        # Convert numerical labels to binary matrix representation
        binarized_predictions = np.zeros((len(predictions), len(mlb.classes_)))
        for i, pred in enumerate(predictions):
            binarized_predictions[i, pred] = 1
        # Convert binary matrix representation to original labels
        original_labels = mlb.inverse_transform(binarized_predictions)
        # Calculate and display metrics
        accuracy = accuracy_score(np.argmax(test_labels, axis=1), predictions)
        f1 = f1_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        precision = precision_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        recall = recall_score(np.argmax(test_labels, axis=1), predictions, average='weighted', zero_division=0)
        print(f'Accuracy: {accuracy:.2f}, F1 Score: {f1:.2f}, Precision: {precision:.2f}, Recall: {recall:.2f}')

        # Save the hypothesis file
        with open(args.hypothesis_filename, 'w') as f:
            for label_set in original_labels:
                f.write(' '.join(label_set) + '\n')

        print(f'Test results saved as {args.hypothesis_filename}')

if __name__ == '__main__':
    main()
```

ဒီတစ်ခါ 5K နဲ့ training လုပ်ကြည့်တော့ အောက်ပါအတိုင်း ရလဒ်ရတယ်။  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ ./train_test.sh | tee 5K_train_test.log
Training with 5K data ...
Epoch 1/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.45, Recall: 0.48
Epoch 2/100, Accuracy: 0.45, F1 Score: 0.44, Precision: 0.42, Recall: 0.45
Epoch 3/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.48, Recall: 0.46
Epoch 4/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.43, Recall: 0.48
Epoch 5/100, Accuracy: 0.50, F1 Score: 0.45, Precision: 0.42, Recall: 0.50
Epoch 6/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.42, Recall: 0.47
Epoch 7/100, Accuracy: 0.45, F1 Score: 0.43, Precision: 0.41, Recall: 0.45
Epoch 8/100, Accuracy: 0.46, F1 Score: 0.41, Precision: 0.39, Recall: 0.46
Epoch 9/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.41, Recall: 0.47
Epoch 10/100, Accuracy: 0.47, F1 Score: 0.42, Precision: 0.42, Recall: 0.47
Epoch 11/100, Accuracy: 0.46, F1 Score: 0.44, Precision: 0.42, Recall: 0.46
Epoch 12/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.42, Recall: 0.46
Epoch 13/100, Accuracy: 0.45, F1 Score: 0.41, Precision: 0.46, Recall: 0.45
Epoch 14/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.40, Recall: 0.46
Epoch 15/100, Accuracy: 0.49, F1 Score: 0.46, Precision: 0.45, Recall: 0.49
Epoch 16/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.40, Recall: 0.47
Epoch 17/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.42, Recall: 0.46
Epoch 18/100, Accuracy: 0.44, F1 Score: 0.43, Precision: 0.45, Recall: 0.44
Epoch 19/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.45, Recall: 0.47
Epoch 20/100, Accuracy: 0.44, F1 Score: 0.42, Precision: 0.46, Recall: 0.44
Epoch 21/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.46, Recall: 0.48
Epoch 22/100, Accuracy: 0.44, F1 Score: 0.43, Precision: 0.43, Recall: 0.44
Epoch 23/100, Accuracy: 0.47, F1 Score: 0.42, Precision: 0.42, Recall: 0.47
Epoch 24/100, Accuracy: 0.47, F1 Score: 0.45, Precision: 0.42, Recall: 0.47
Epoch 25/100, Accuracy: 0.51, F1 Score: 0.47, Precision: 0.44, Recall: 0.51
Epoch 26/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.42, Recall: 0.48
Epoch 27/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.41, Recall: 0.48
Epoch 28/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.41, Recall: 0.47
Epoch 29/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.44, Recall: 0.46
Epoch 30/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.42, Recall: 0.47
Epoch 31/100, Accuracy: 0.44, F1 Score: 0.41, Precision: 0.38, Recall: 0.44
Epoch 32/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.42, Recall: 0.46
Epoch 33/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.42, Recall: 0.48
Epoch 34/100, Accuracy: 0.46, F1 Score: 0.41, Precision: 0.40, Recall: 0.46
Epoch 35/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.48, Recall: 0.47
Epoch 36/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.42, Recall: 0.48
Epoch 37/100, Accuracy: 0.47, F1 Score: 0.42, Precision: 0.40, Recall: 0.47
Epoch 38/100, Accuracy: 0.45, F1 Score: 0.43, Precision: 0.41, Recall: 0.45
Epoch 39/100, Accuracy: 0.49, F1 Score: 0.46, Precision: 0.43, Recall: 0.49
Epoch 40/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.44, Recall: 0.48
Epoch 41/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.41, Recall: 0.46
Epoch 42/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.44, Recall: 0.46
Epoch 43/100, Accuracy: 0.44, F1 Score: 0.42, Precision: 0.40, Recall: 0.44
Epoch 44/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.41, Recall: 0.46
Epoch 45/100, Accuracy: 0.45, F1 Score: 0.43, Precision: 0.41, Recall: 0.45
Epoch 46/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.41, Recall: 0.47
Epoch 47/100, Accuracy: 0.46, F1 Score: 0.39, Precision: 0.40, Recall: 0.46
Epoch 48/100, Accuracy: 0.44, F1 Score: 0.42, Precision: 0.40, Recall: 0.44
Epoch 49/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.42, Recall: 0.47
Epoch 50/100, Accuracy: 0.48, F1 Score: 0.42, Precision: 0.40, Recall: 0.48
Epoch 51/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.41, Recall: 0.46
Epoch 52/100, Accuracy: 0.43, F1 Score: 0.42, Precision: 0.43, Recall: 0.43
Epoch 53/100, Accuracy: 0.47, F1 Score: 0.45, Precision: 0.44, Recall: 0.47
Epoch 54/100, Accuracy: 0.49, F1 Score: 0.45, Precision: 0.42, Recall: 0.49
Epoch 55/100, Accuracy: 0.45, F1 Score: 0.42, Precision: 0.39, Recall: 0.45
Epoch 56/100, Accuracy: 0.46, F1 Score: 0.42, Precision: 0.42, Recall: 0.46
Epoch 57/100, Accuracy: 0.46, F1 Score: 0.44, Precision: 0.44, Recall: 0.46
Epoch 58/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.44, Recall: 0.47
Epoch 59/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.44, Recall: 0.47
Epoch 60/100, Accuracy: 0.46, F1 Score: 0.42, Precision: 0.43, Recall: 0.46
Epoch 61/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.42, Recall: 0.48
Epoch 62/100, Accuracy: 0.49, F1 Score: 0.45, Precision: 0.44, Recall: 0.49
Epoch 63/100, Accuracy: 0.45, F1 Score: 0.42, Precision: 0.40, Recall: 0.45
Epoch 64/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.46, Recall: 0.48
Epoch 65/100, Accuracy: 0.49, F1 Score: 0.47, Precision: 0.46, Recall: 0.49
Epoch 66/100, Accuracy: 0.48, F1 Score: 0.43, Precision: 0.41, Recall: 0.48
Epoch 67/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.45, Recall: 0.48
Epoch 68/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.41, Recall: 0.47
Epoch 69/100, Accuracy: 0.49, F1 Score: 0.45, Precision: 0.44, Recall: 0.49
Epoch 70/100, Accuracy: 0.43, F1 Score: 0.41, Precision: 0.41, Recall: 0.43
Epoch 71/100, Accuracy: 0.44, F1 Score: 0.42, Precision: 0.42, Recall: 0.44
Epoch 72/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.43, Recall: 0.48
Epoch 73/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.41, Recall: 0.46
Epoch 74/100, Accuracy: 0.44, F1 Score: 0.43, Precision: 0.42, Recall: 0.44
Epoch 75/100, Accuracy: 0.44, F1 Score: 0.42, Precision: 0.40, Recall: 0.44
Epoch 76/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.41, Recall: 0.48
Epoch 77/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.41, Recall: 0.48
Epoch 78/100, Accuracy: 0.46, F1 Score: 0.42, Precision: 0.41, Recall: 0.46
Epoch 79/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.43, Recall: 0.48
Epoch 80/100, Accuracy: 0.46, F1 Score: 0.42, Precision: 0.44, Recall: 0.46
Epoch 81/100, Accuracy: 0.49, F1 Score: 0.45, Precision: 0.44, Recall: 0.49
Epoch 82/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.42, Recall: 0.47
Epoch 83/100, Accuracy: 0.44, F1 Score: 0.41, Precision: 0.40, Recall: 0.44
Epoch 84/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.40, Recall: 0.47
Epoch 85/100, Accuracy: 0.48, F1 Score: 0.43, Precision: 0.41, Recall: 0.48
Epoch 86/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.43, Recall: 0.47
Epoch 87/100, Accuracy: 0.46, F1 Score: 0.43, Precision: 0.43, Recall: 0.46
Epoch 88/100, Accuracy: 0.46, F1 Score: 0.41, Precision: 0.40, Recall: 0.46
Epoch 89/100, Accuracy: 0.47, F1 Score: 0.43, Precision: 0.42, Recall: 0.47
Epoch 90/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.42, Recall: 0.48
Epoch 91/100, Accuracy: 0.48, F1 Score: 0.44, Precision: 0.43, Recall: 0.48
Epoch 92/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.44, Recall: 0.48
Epoch 93/100, Accuracy: 0.42, F1 Score: 0.40, Precision: 0.39, Recall: 0.42
Epoch 94/100, Accuracy: 0.45, F1 Score: 0.42, Precision: 0.41, Recall: 0.45
Epoch 95/100, Accuracy: 0.46, F1 Score: 0.42, Precision: 0.40, Recall: 0.46
Epoch 96/100, Accuracy: 0.46, F1 Score: 0.41, Precision: 0.40, Recall: 0.46
Epoch 97/100, Accuracy: 0.49, F1 Score: 0.45, Precision: 0.44, Recall: 0.49
Epoch 98/100, Accuracy: 0.48, F1 Score: 0.45, Precision: 0.42, Recall: 0.48
Epoch 99/100, Accuracy: 0.47, F1 Score: 0.44, Precision: 0.46, Recall: 0.47
Epoch 100/100, Accuracy: 0.46, F1 Score: 0.44, Precision: 0.44, Recall: 0.46
Model trained and saved as error_type.5k.model.joblib

real    2m52.551s
user    2m48.306s
sys     0m6.776s
===============
Testing with 100 errors ...
Accuracy: 0.49, F1 Score: 0.48, Precision: 0.47, Recall: 0.49
Test results saved as ./error_type.100.hyp

real    0m0.382s
user    0m0.995s
sys     0m1.927s
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

hyp ဖိုင် output ကလည်း original label format အနေနဲ့ ပြန်ထုတ်ပေးတာကို confirm လုပ်ခဲ့ ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ head error_type.100.hyp
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
__label__pho
__label__typo
__label__pho
__label__pho
__label__pho
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

## Increasing the No. of Epoch

backup 5K, 100 epoch models ...  

```
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ mv error_type.5k.model* ./bk/5K_100epoch/
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$ ls ./bk/5K_100epoch/
error_type.5k.model.joblib   error_type.5k.model_vectorizer.pkl
error_type.5k.model_mlb.pkl
(base) ye@lst-gpu-3090:~/exp/mySpell/tsetlin$
```

Updating the shell script for training with 300 epoch ...  

```bash
#!/bin/bash

echo "Training with 5K data ..."
time python ./tsetlin_classifier.py --mode train --train_data ./error_type.5k.train --model_name error_type.5k.model --epoch 300

echo "==============="
echo "Testing with 100 errors ..."
time python ./tsetlin_classifier.py --mode test --model_name error_type.5k.model --test_data ./error_type.100.valid --hypothesis_filename ./error_type.100.hyp
```

Running log for 300 epoch is as follows ...  

```

```

## Training/Testing with All Data
### Experiment No. 1 with Tsetlin Machine

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
