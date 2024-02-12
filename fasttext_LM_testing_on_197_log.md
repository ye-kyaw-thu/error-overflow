# FastText LM Training/Testing on 197 Server


## FastText Installation on 197 Server

```
ye@lst-gpu-server-197:~/ye/tool$ git clone https://github.com/facebookresearch/fastText.git
Cloning into 'fastText'...
remote: Enumerating objects: 3986, done.
remote: Counting objects: 100% (1014/1014), done.
remote: Compressing objects: 100% (180/180), done.
remote: Total 3986 (delta 888), reused 854 (delta 830), pack-reused 2972
Receiving objects: 100% (3986/3986), 8.29 MiB | 15.04 MiB/s, done.
Resolving deltas: 100% (2526/2526), done.
ye@lst-gpu-server-197:~/ye/tool$ cd fastText/
ye@lst-gpu-server-197:~/ye/tool/fastText$ ls
alignment                  get-wikimedia.sh         scripts
classification-example.sh  LICENSE                  setup.cfg
classification-results.sh  Makefile                 setup.py
CMakeLists.txt             MANIFEST.in              src
CODE_OF_CONDUCT.md         PACKAGE                  tests
CONTRIBUTING.md            pyproject.toml           webassembly
crawl                      python                   website
docs                       quantization-example.sh  wikifil.pl
download_model.py          README.md                word-vector-example.sh
eval.py                    reduce_model.py
fasttext.pc.in             runtests.py
ye@lst-gpu-server-197:~/ye/tool/fastText$ make
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/args.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/autotune.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/matrix.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/dictionary.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/loss.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/productquantizer.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/densematrix.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/quantmatrix.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/vector.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/model.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/utils.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/meter.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG -c src/fasttext.cc
c++ -pthread -std=c++17 -march=native -O3 -funroll-loops -DNDEBUG args.o autotune.o matrix.o dictionary.o loss.o productquantizer.o densematrix.o quantmatrix.o vector.o model.o utils.o meter.o fasttext.o src/main.cc -o fasttext
ye@lst-gpu-server-197:~/ye/tool/fastText$ fasttext --help
Command 'fasttext' not found, but can be installed with:
apt install fasttext
Please ask your administrator.
ye@lst-gpu-server-197:~/ye/tool/fastText$
```

path ကို .bashrc မှာ export လုပ်ပြီးတော့ fasttext command ခေါ်လို့ရ။  

```
ye@lst-gpu-server-197:~/ye/tool/fastText$ ./fasttext --help
usage: fasttext <command> <args>

The commands supported by fasttext are:

  supervised              train a supervised classifier
  quantize                quantize a model to reduce the memory usage
  test                    evaluate a supervised classifier
  test-label              print labels with precision and recall scores
  predict                 predict most likely labels
  predict-prob            predict most likely labels with probabilities
  skipgram                train a skipgram model
  cbow                    train a cbow model
  print-word-vectors      print word vectors given a trained model
  print-sentence-vectors  print sentence vectors given a trained model
  print-ngrams            print ngrams given a trained model and word
  nn                      query for nearest neighbors
  analogies               query for analogies
  dump                    dump arguments,dictionary,input/output vectors

ye@lst-gpu-server-197:~/ye/tool/fastText$
```

## FastText Python Installation on 197 Server

```
ye@lst-gpu-server-197:~/ye/exp/lm$ pip install fasttext
Defaulting to user installation because normal site-packages is not writeable
Collecting fasttext
  Downloading fasttext-0.9.2.tar.gz (68 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 68.8/68.8 KB 1.4 MB/s eta 0:00:00
  Preparing metadata (setup.py) ... done
Collecting numpy
  Downloading numpy-1.26.4-cp310-cp310-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (18.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 18.2/18.2 MB 52.6 MB/s eta 0:00:00
Collecting pybind11>=2.2
  Using cached pybind11-2.11.1-py3-none-any.whl (227 kB)
Requirement already satisfied: setuptools>=0.7.0 in /usr/lib/python3/dist-packages (from fasttext) (59.6.0)
Building wheels for collected packages: fasttext
  Building wheel for fasttext (setup.py) ... done
  Created wheel for fasttext: filename=fasttext-0.9.2-cp310-cp310-linux_x86_64.whl size=4199781 sha256=5a11700390f24f89dc6f811d041c69f6103e207d282cde7465d66296a7da6691
  Stored in directory: /home/ye/.cache/pip/wheels/a5/13/75/f811c84a8ab36eedbaef977a6a58a98990e8e0f1967f98f394
Successfully built fasttext
Installing collected packages: pybind11, numpy, fasttext
  WARNING: The script pybind11-config is installed in '/home/ye/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
  WARNING: The script f2py is installed in '/home/ye/.local/bin' which is not on PATH.
  Consider adding this directory to PATH or, if you prefer to suppress this warning, use --no-warn-script-location.
Successfully installed fasttext-0.9.2 numpy-1.26.4 pybind11-2.11.1
ye@lst-gpu-server-197:~/ye/exp/lm$
```

## Import Testing

```
ye@lst-gpu-server-197:~/ye/exp/lm$ python --version
Command 'python' not found, did you mean:
  command 'python3' from deb python3
  command 'python' from deb python-is-python3
```

ဪ !!!  

```  
ye@lst-gpu-server-197:~/ye/exp/lm$ python3 --version
Python 3.10.12
ye@lst-gpu-server-197:~/ye/exp/lm$
```

```
ye@lst-gpu-server-197:~/ye/exp/lm$ python3
Python 3.10.12 (main, Nov 20 2023, 15:14:05) [GCC 11.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import fasttext
>>> print(dir(fasttext))
['BOW', 'EOS', 'EOW', 'FastText', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__path__', '__spec__', 'absolute_import', 'cbow', 'division', 'load_model', 'print_function', 'skipgram', 'supervised', 'tokenize', 'train_supervised', 'train_unsupervised', 'unicode_literals']
>>> exit()
ye@lst-gpu-server-197:~/ye/exp/lm$
```

## Copied the Python Code to 197 Server

```python
"""

LM building and testing with FastText.
Written by Ye Kyaw Thu, LU Lab., Myanmar.
Last updated: 11 Feb 2024

Usage:
 python3 ./fasttext_lm.py --help
 python3 ./fasttext_lm.py train --help
 python3 ./fasttext_lm.py test --help


"""

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

## Run with --help

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ python3 ./fasttext_lm.py --help
usage: fasttext_lm.py [-h] {train,test} ...

FastText Model Trainer and Tester

positional arguments:
  {train,test}  Mode of operation
    train       Train a model
    test        Test a model

options:
  -h, --help    show this help message and exit
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$
```

Help for training ...  

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ python3 ./fasttext_lm.py train --help
usage: fasttext_lm.py train [-h] --input INPUT --output OUTPUT
                            [--model_type {cbow,skipgram}] [--epochs EPOCHS]
                            [--min_count MIN_COUNT] [--max_ngram MAX_NGRAM] [--dim DIM]

options:
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
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$
```

Help for testing ...  

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ python3 ./fasttext_lm.py test --help
usage: fasttext_lm.py test [-h] --model MODEL
                           [--operation {word_vector,nearest_neighbors,word_analogies}]
                           [--word WORD] [--analogy ANALOGY] [--k K] [--interactive]

options:
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
  --interactive         Enable interactive mode
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$
```

## Training/Testing Shell Script

ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ cat ./run_ftlm.sh  

```bash
#!/bin/bash

set -x
mkdir model;

# Training Mode:
time python3 ./fasttext_lm.py train \
--input ./corpus/myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned \
--output ./model/fasttext.5gram.30ep.model --model_type skipgram \
--min_count 3 --max_ngram 5 --epochs 30

# Testing Mode Example (Word Vector):
time python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation word_vector --word "အိပ်မက်" --k 10

# Testing Mode Example (Nearest Neighbors):
time python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation nearest_neighbors --word "အိပ်မက်" --k 10

# Testing Mode Example (Word Analogy):
python3 fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model \
--operation word_analogies --analogy "အချစ် အမုန်း စိတ်ဆိုး" --k 10

set +x
```

## Training/Testing on 197 Server

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ ./run_ftlm.sh | tee ftlm_train_test.log
+ mkdir model
mkdir: cannot create directory ‘model’: File exists
+ python3 ./fasttext_lm.py train --input ./corpus/myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned --output ./model/fasttext.5gram.30ep.model --model_type skipgram --min_count 3 --max_ngram 5 --epochs 30
Read 7M words
Number of words:  36649
Number of labels: 0
Progress:   0.1% words/sec/thread:   42150 lr:  0.049969 avg.loss:  3.324318 ETA:   0h 2m4Progress:   0.1% words/sec/thread:   42685 lr:  0.049938 avg.loss:  2.730555 ETA:   0h 2m4Progress:   0.2% words/sec/thread:   43183 lr:  0.049907 avg.loss:  2.535747 ETA:   0h 2m4Progress:   0.3% words/sec/thread:   43735 lr:  0.049875 avg.loss:  2.436563 ETA:   0h 2m4Progress:   0.3% words/sec/thread:   43226 lr:  0.049845 avg.loss:  2.388498 ETA:   0h 2m4Progress:   0.4% words/sec/thread:   42781 lr:  0.049817 avg.loss:  2.339857 ETA:   0h 2m4Progress:   0.4% words/sec/thread:   42478 lr:  0.049788 avg.loss:  2.317615 ETA:   0h 2m4Progress:   0.5% words/sec/thread:   42332 lr:  0.049758 avg.loss:  2.300719 ETA:   0h 2m4Progress:   0.5% words/sec/thread:   42212 lr:  0.049729 avg.loss:  2.280957 ETA:   0h 2m4Progress:   0.6% words/sec/thread:   42090 lr:  0.049700 avg.loss:  2.258365 ETA:   0h 2m4Progress:   0.7% words/sec/thread:   41904 lr:  0.049672 avg.loss:  2.246244 ETA:   0h 2m4Progress:   0.7% words/sec/thread:   41763 lr:  0.049643 avg.loss:  2.230191 ETA:   0h 2m4Progress:   0.8% words/sec/thread:   41663 lr:  0.049614 avg.loss:  2.216394 ETA:   0h 2m4Progress:   0.8% words/sec/thread:   41629 lr:  0.049585 avg.loss:  2.209474 ETA:   0h 2m4Progress:   0.9% words/sec/thread:   41610 lr:  0.049555 avg.loss:  2.199957 ETA:   0h 2m4Progress:   0.9% words/sec/thread:   41597 lr:  0.049526 avg.loss:  2.196213 ETA:   0h 2m4Progress:   1.0% words/sec/thread:   41540 lr:  0.049497 avg.loss:  2.191755 ETA:   0h 2m4Progress:   1.1% words/sec/thread:   41504 lr:  0.049468 avg.loss:  2.186958 ETA:   0h 2m4Progress:   1.1% words/sec/thread:   41460 lr:  0.049439 avg.loss:  2.180880 ETA:   0h 2m4Progress:   1.2% words/sec/thread:   41416 lr:  0.049410 avg.loss:  2.171787 ETA:   0h 2m4Progress:   1.2% words/sec/thread:   41496 lr:  0.049380 avg.loss:  2.168504 ETA:   0h 2m4Progress:   1.3% words/sec/thread:   41671 lr:  0.049347 avg.loss:  2.164691 ETA:   0h 2m4Progress:   1.4% words/sec/thread:   41812 lr:  0.049315 avg.loss:  2.162251 ETA:   0h 2m4Progress:   1.4% words/sec/thread:   41994 lr:  0.049283 avg.loss:  2.160625 ETA:   0h 2m4Progress:   1.5% words/sec/thread:   42175 lr:  0.049249 avg.loss:  2.155608 ETA:   0h 2m4Progress:   1.6% words/sec/thread:   42395 lr:  0.049215 avg.loss:  2.153674 ETA:   0h 2m4Progress:   1.6% words/sec/thread:   42550 lr:  0.049182 avg.loss:  2.150924 ETA:   0h 2m4Progress:   1.7% words/sec/thread:   42722 lr:  0.049149 avg.loss:  2.144417 ETA:   0h 2m4Progress:   1.8% words/sec/thread:   42877 lr:  0.049115 avg.loss:  2.143516 ETA:   0h 2m4Progress:   1.8% words/sec/thread:   43013 lr:  0.049082 avg.loss:  2.140328 ETA:   0h 2m4Progress:   1.9% words/sec/thread:   43129 lr:  0.049049 avg.loss:  2.137802 ETA:   0h 2m4Progress:   2.0% words/sec/thread:   43225 lr:  0.049016 avg.loss:  2.133069 ETA:   0h 2m3Progress:   2.0% words/sec/thread:   43319 lr:  0.048983 avg.loss:  2.129501 ETA:   0h 2m3Progress:   2.1% words/sec/thread:   43416 lr:  0.048950 avg.loss:  2.126586 ETA:   0h 2m3Progress:   2.2% words/sec/thread:   43505 lr:  0.048917 avg.loss:  2.124781 ETA:   0h 2m3Progress:   2.2% words/sec/thread:   43555 lr:  0.048885 avg.loss:  2.120742 ETA:   0h 2m3Progress:   2.3% words/sec/thread:   43646 lr:  0.048851 avg.loss:  2.119258 ETA:   0h 2m3Progress:   2.4% words/sec/thread:   43759 lr:  0.048817 avg.loss:  2.116261 ETA:   0h 2m3Progress:   2.4% words/sec/thread:   43878 lr:  0.048783 avg.loss:  2.114637 ETA:   0h 2m3Progress:   2.5% words/sec/thread:   43984 lr:  0.048749 avg.loss:  2.110531 ETA:   0h 2m3Progress:   2.6% words/sec/thread:   44048 lr:  0.048716 avg.loss:  2.110392 ETA:   0h 2m3Progress:   2.6% words/sec/thread:   44159 lr:  0.048681 avg.loss:  2.107957 ETA:   0h 2m3Progress:   2.7% words/sec/thread:   44245 lr:  0.048647 avg.loss:  2.107947 ETA:   0h 2m3Progress:   2.8% words/sec/thread:   44329 lr:  0.048613 avg.loss:  2.106988 ETA:   0h 2m3Progress:   2.8% words/sec/thread:   44396 lr:  0.048579 avg.loss:  2.105729 ETA:   0h 2m3Progress:   2.9% words/sec/thread:   44439 lr:  0.048546 avg.loss:  2.105488 ETA:   0h 2m3Progress:   3.0% words/sec/thread:   44515 lr:  0.048512 avg.loss:  2.102260 ETA:   0h 2m3Progress:   3.0% words/sec/thread:   44592 lr:  0.048478 avg.loss:  2.101344 ETA:   0h 2m3Progress:   3.1% words/sec/thread:   44676 lr:  0.048444 avg.loss:  2.098789 ETA:   0h 2m3Progress:   3.2% words/sec/thread:   44737 lr:  0.048410 avg.loss:  2.097567 ETA:   0h 2m3Progress:   3.2% words/sec/thread:   44815 lr:  0.048375 avg.loss:  2.096766 ETA:   0h 2m3Progress:   3.3% words/sec/thread:   44877 lr:  0.048341 avg.loss:  2.094431 ETA:   0h 2m3Progress:   3.4% words/sec/thread:   44912 lr:  0.048308 avg.loss:  2.093085 ETA:   0h 2m3Progress:   3.5% words/sec/thread:   44973 lr:  0.048274 avg.loss:  2.091367 ETA:   0h 2m3Progress:   3.5% words/sec/thread:   45026 lr:  0.048239 avg.loss:  2.090464 ETA:   0h 2m3Progress:   3.6% words/sec/thread:   45077 lr:  0.048205 avg.loss:  2.088603 ETA:   0h 2m3Progress:   3.7% words/sec/thread:   45108 lr:  0.048172 avg.loss:  2.087742 ETA:   0h 2m3Progress:   3.7% words/sec/thread:   45146 lr:  0.048139 avg.loss:  2.086972 ETA:   0h 2m3Progress:   3.8% words/sec/thread:   45188 lr:  0.048105 avg.loss:  2.084531 ETA:   0h 2m3Progress:   3.9% words/sec/thread:   45256 lr:  0.048070 avg.loss:  2.083408 ETA:   0h 2m2Progress:   3.9% words/sec/thread:   45267 lr:  0.048037 avg.loss:  2.083244 ETA:   0h 2m2Progress:   4.0% words/sec/thread:   45322 lr:  0.048003 avg.loss:  2.083017 ETA:   0h 2m2Progress:   4.1% words/sec/thread:   45369 lr:  0.047968 avg.loss:  2.081589 ETA:   0h 2m2Progress:   4.1% words/sec/thread:   45391 lr:  0.047935 avg.loss:  2.080350 ETA:   0h 2m2Progress:   4.2% words/sec/thread:   45432 lr:  0.047901 avg.loss:  2.079160 ETA:   0h 2m2Progress:   4.3% words/sec/thread:   45448 lr:  0.047868 avg.loss:  2.077521 ETA:   0h 2m2Progress:   4.3% words/sec/thread:   45483 lr:  0.047834 avg.loss:  2.076216 ETA:   0h 2m2Progress:   4.4% words/sec/thread:   45421 lr:  0.047805 avg.loss:  2.074929 ETA:   0h 2m2Progress:   4.5% words/sec/thread:   45433 lr:  0.047772 avg.loss:  2.074120 ETA:   0h 2m2Progress:   4.5% words/sec/thread:   45462 lr:  0.047738 avg.loss:  2.072994 ETA:   0h 2m2Progress:   4.6% words/sec/thread:   45506 lr:  0.047704 avg.loss:  2.071838 ETA:   0h 2m2Progress:   4.7% words/sec/thread:   45555 lr:  0.047669 avg.loss:  2.070719 ETA:   0h 2m2Progress:   4.7% words/sec/thread:   45585 lr:  0.047635 avg.loss:  2.069675 ETA:   0h 2m2Progress:   4.8% words/sec/thread:   45621 lr:  0.047601 avg.loss:  2.069607 ETA:   0h 2m2Progress:   4.9% words/sec/thread:   45661 lr:  0.047566 avg.loss:  2.069165 ETA:   0h 2m2Progress:   4.9% words/sec/thread:   45692 lr:  0.047532 avg.loss:  2.068580 ETA:   0h 2m2Progress:   5.0% words/sec/thread:   45714 lr:  0.047498 avg.loss:  2.067867 ETA:   0h 2m2Progress:   5.1% words/sec/thread:   45745 lr:  0.047464 avg.loss:  2.066881 ETA:   0h 2m2Progress:   5.1% words/sec/thread:   45776 lr:  0.047430 avg.loss:  2.066958 ETA:   0h 2m2Progress:   5.2% words/sec/thread:   45819 lr:  0.047395 avg.loss:  2.065817 ETA:   0h 2m2Progress:   5.3% words/sec/thread:   45852 lr:  0.047361 avg.loss:  2.064363 ETA:   0h 2m2Progress:   5.3% words/sec/thread:   45879 lr:  0.047326 avg.loss:  2.062880 ETA:   0h 2m2Progress:   5.4% words/sec/thread:   45902 lr:  0.047293 avg.loss:  2.061264 ETA:   0h 2m2Progress:   5.5% words/sec/thread:   45936 lr:  0.047258 avg.loss:  2.060138 ETA:   0h 2m2Progress:   5.6% words/sec/thread:   45964 lr:  0.047224 avg.loss:  2.060187 ETA:   0h 2m2Progress:   5.6% words/sec/thread:   45990 lr:  0.047189 avg.loss:  2.059338 ETA:   0h 2m2Progress:   5.7% words/sec/thread:   46022 lr:  0.047155 avg.loss:  2.059275 ETA:   0h 2m2Progress:   5.8% words/sec/thread:   46034 lr:  0.047121 avg.loss:  2.058750 ETA:   0h 2m2Progress:   5.8% words/sec/thread:   46051 lr:  0.047087 avg.loss:  2.058106 ETA:   0h 2m2Progress:   5.9% words/sec/thread:   46078 lr:  0.047053 avg.loss:  2.057301 ETA:   0h 2m2Progress:   6.0% words/sec/thread:   46109 lr:  0.047018 avg.loss:  2.056440 ETA:   0h 2m2Progress:   6.0% words/sec/thread:   46137 lr:  0.046984 avg.loss:  2.053700 ETA:   0h 2m2Progress:   6.1% words/sec/thread:   46156 lr:  0.046950 avg.loss:  2.052286 ETA:   0h 2m2Progress:   6.2% words/sec/thread:   46190 lr:  0.046915 avg.loss:  2.052050 ETA:   0h 2m2Progress:   6.2% words/sec/thread:   46214 lr:  0.046880 avg.loss:  2.051459 ETA:   0h 2m2Progress:   6.3% words/sec/thread:   46237 lr:  0.046846 avg.loss:  2.051141 ETA:   0h 2m2Progress:   6.4% words/sec/thread:   46262 lr:  0.046811 avg.loss:  2.049548 ETA:   0h 2m2Progress:   6.4% words/sec/thread:   46283 lr:  0.046777 avg.loss:  2.048412 ETA:   0h 2m2Progress:   6.5% words/sec/thread:   46306 lr:  0.046743 avg.loss:  2.047874 ETA:   0h 2m2Progress:   6.6% words/sec/thread:   46318 lr:  0.046709 avg.loss:  2.047450 ETA:   0h 2m2Progress:   6.7% words/sec/thread:   46336 lr:  0.046675 avg.loss:  2.045647 ETA:   0h 2m2Progress:   6.7% words/sec/thread:   46354 lr:  0.046641 avg.loss:  2.044493 ETA:   0h 2m2Progress:   6.8% words/sec/thread:   46375 lr:  0.046606 avg.loss:  2.043769 ETA:   0h 2m2Progress:   6.9% words/sec/thread:   46399 lr:  0.046571 avg.loss:  2.043237 ETA:   0h 2m2Progress:   6.9% words/sec/thread:   46425 lr:  0.046537 avg.loss:  2.041786 ETA:   0h 2m2Progress:   7.0% words/sec/thread:   46449 lr:  0.046502 avg.loss:  2.041145 ETA:   0h 2m2Progress:   7.1% words/sec/thread:   46465 lr:  0.046468 avg.loss:  2.039834 ETA:   0h 2m2Progress:   7.1% words/sec/thread:   46493 lr:  0.046432 avg.loss:  2.039042 ETA:   0h 2m2Progress:   7.2% words/sec/thread:   46512 lr:  0.046398 avg.loss:  2.038565 ETA:   0h 2m2Progress:   7.3% words/sec/thread:   46515 lr:  0.046365 avg.loss:  2.037622 ETA:   0h 2m2Progress:   7.3% words/sec/thread:   46524 lr:  0.046331 avg.loss:  2.036375 ETA:   0h 2m2Progress:   7.4% words/sec/thread:   46544 lr:  0.046296 avg.loss:  2.035738 ETA:   0h 2m2Progress:   7.5% words/sec/thread:   46566 lr:  0.046262 avg.loss:  2.034877 ETA:   0h 2m2Progress:   7.5% words/sec/thread:   46587 lr:  0.046227 avg.loss:  2.034760 ETA:   0h 2m1Progress:   7.6% words/sec/thread:   46601 lr:  0.046193 avg.loss:  2.034304 ETA:   0h 2m1Progress:   7.7% words/sec/thread:   46617 lr:  0.046158 avg.loss:  2.033205 ETA:   0h 2m1Progress:   7.8% words/sec/thread:   46633 lr:  0.046124 avg.loss:  2.032773 ETA:   0h 2m1Progress:   7.8% words/sec/thread:   46644 lr:  0.046090 avg.loss:  2.031619 ETA:   0h 2m1Progress:   7.9% words/sec/thread:   46659 lr:  0.046055 avg.loss:  2.030835 ETA:   0h 2m1Progress:   8.0% words/sec/thread:   46670 lr:  0.046021 avg.loss:  2.030286 ETA:   0h 2m1Progress:   8.0% words/sec/thread:   46660 lr:  0.045989 avg.loss:  2.029392 ETA:   0h 2m1Progress:   8.1% words/sec/thread:   46666 lr:  0.045955 avg.loss:  2.029366 ETA:   0h 2m1Progress:   8.2% words/sec/thread:   46684 lr:  0.045921 avg.loss:  2.028631 ETA:   0h 2m1Progress:   8.2% words/sec/thread:   46701 lr:  0.045886 avg.loss:  2.027957 ETA:   0h 2m1Progress:   8.3% words/sec/thread:   46714 lr:  0.045852 avg.loss:  2.027962 ETA:   0h 2m1Progress:   8.4% words/sec/thread:   46722 lr:  0.045818 avg.loss:  2.024191 ETA:   0h 2m1Progress:   8.4% words/sec/thread:   46735 lr:  0.045783 avg.loss:  2.023439 ETA:   0h 2m1Progress:   8.5% words/sec/thread:   46749 lr:  0.045749 avg.loss:  2.023171 ETA:   0h 2m1Progress:   8.6% words/sec/thread:   46761 lr:  0.045715 avg.loss:  2.022887 ETA:   0h 2m1Progress:   8.6% words/sec/thread:   46779 lr:  0.045680 avg.loss:  2.022838 ETA:   0h 2m1Progress:   8.7% words/sec/thread:   46788 lr:  0.045646 avg.loss:  2.022240 ETA:   0h 2m1Progress:   8.8% words/sec/thread:   46776 lr:  0.045613 avg.loss:  2.021568 ETA:   0h 2m1Progress:   8.8% words/sec/thread:   46783 lr:  0.045580 avg.loss:  2.021195 ETA:   0h 2m1Progress:   8.9% words/sec/thread:   46793 lr:  0.045545 avg.loss:  2.020167 ETA:   0h 2m1Progress:   9.0% words/sec/thread:   46803 lr:  0.045511 avg.loss:  2.019116 ETA:   0h 2m1Progress:   9.0% words/sec/thread:   46815 lr:  0.045477 avg.loss:  2.018341 ETA:   0h 2m1Progress:   9.1% words/sec/thread:   46829 lr:  0.045442 avg.loss:  2.017799 ETA:   0h 2m1Progress:   9.2% words/sec/thread:   46821 lr:  0.045409 avg.loss:  2.017379 ETA:   0h 2m1Progress:   9.2% words/sec/thread:   46831 lr:  0.045375 avg.loss:  2.016120 ETA:   0h 2m1Progress:   9.3% words/sec/thread:   46835 lr:  0.045341 avg.loss:  2.015836 ETA:   0h 2m1Progress:   9.4% words/sec/thread:   46836 lr:  0.045308 avg.loss:  2.014613 ETA:   0h 2m1Progress:   9.5% words/sec/thread:   46838 lr:  0.045274 avg.loss:  2.014267 ETA:   0h 2m1Progress:   9.5% words/sec/thread:   46844 lr:  0.045241 avg.loss:  2.013443 ETA:   0h 2m1Progress:   9.6% words/sec/thread:   46852 lr:  0.045206 avg.loss:  2.011828 ETA:   0h 2m1Progress:   9.7% words/sec/thread:   46865 lr:  0.045172 avg.loss:  2.011787 ETA:   0h 2m1Progress:   9.7% words/sec/thread:   46874 lr:  0.045138 avg.loss:  2.011601 ETA:   0h 2m1Progress:   9.8% words/sec/thread:   46886 lr:  0.045103 avg.loss:  2.011262 ETA:   0h 2m1Progress:   9.9% words/sec/thread:   46897 lr:  0.045069 avg.loss:  2.010023 ETA:   0h 2m1Progress:   9.9% words/sec/thread:   46907 lr:  0.045034 avg.loss:  2.009911 ETA:   0h 2m1Progress:  10.0% words/sec/thread:   46910 lr:  0.045001 avg.loss:  2.009283 ETA:   0h 2m1Progress:  10.1% words/sec/thread:   46923 lr:  0.044966 avg.loss:  2.009342 ETA:   0h 2m1Progress:  10.1% words/sec/thread:   46934 lr:  0.044931 avg.loss:  2.009150 ETA:   0h 2m1Progress:  10.2% words/sec/thread:   46943 lr:  0.044897 avg.loss:  2.009149 ETA:   0h 2m1Progress:  10.3% words/sec/thread:   46946 lr:  0.044863 avg.loss:  2.008858 ETA:   0h 2m1Progress:  10.3% words/sec/thread:   46956 lr:  0.044829 avg.loss:  2.008552 ETA:   0h 2m1Progress:  10.4% words/sec/thread:   46965 lr:  0.044795 avg.loss:  2.008216 ETA:   0h 2m1Progress:  10.5% words/sec/thread:   46977 lr:  0.044760 avg.loss:  2.008388 ETA:   0h 2m1Progress:  10.5% words/sec/thread:   46983 lr:  0.044726 avg.loss:  2.007800 ETA:   0h 2m1Progress:  10.6% words/sec/thread:   46987 lr:  0.044692 avg.loss:  2.006984 ETA:   0h 2m1Progress:  10.7% words/sec/thread:   46997 lr:  0.044658 avg.loss:  2.006415 ETA:   0h 2m1Progress:  10.8% words/sec/thread:   47003 lr:  0.044624 avg.loss:  2.006233 ETA:   0h 2m1Progress:  10.8% words/sec/thread:   47009 lr:  0.044589 avg.loss:  2.005856 ETA:   0h 2m1Progress:  10.9% words/sec/thread:   47019 lr:  0.044555 avg.loss:  2.005934 ETA:   0h 2m1Progress:  11.0% words/sec/thread:   47017 lr:  0.044522 avg.loss:  2.005443 ETA:   0h 2m1Progress:  11.0% words/sec/thread:   47023 lr:  0.044488 avg.loss:  2.005513 ETA:   0h 2m1Progress:  11.1% words/sec/thread:   47032 lr:  0.044453 avg.loss:  2.005614 ETA:   0h 2m1Progress:  11.2% words/sec/thread:   47038 lr:  0.044419 avg.loss:  2.005104 ETA:   0h 2m1Progress:  11.2% words/sec/thread:   47051 lr:  0.044384 avg.loss:  2.004890 ETA:   0h 2m1Progress:  11.3% words/sec/thread:   47058 lr:  0.044350 avg.loss:  2.004686 ETA:   0h 2m1Progress:  11.4% words/sec/thread:   47063 lr:  0.044316 avg.loss:  2.004328 ETA:   0h 2m1Progress:  11.4% words/sec/thread:   47075 lr:  0.044281 avg.loss:  2.003875 ETA:   0h 2m1Progress:  11.5% words/sec/thread:   47084 lr:  0.044246 avg.loss:  2.003585 ETA:   0h 2m1Progress:  11.6% words/sec/thread:   47090 lr:  0.044212 avg.loss:  2.003222 ETA:   0h 2m1Progress:  11.6% words/sec/thread:   47091 lr:  0.044179 avg.loss:  2.002844 ETA:   0h 2m1Progress:  11.7% words/sec/thread:   47090 lr:  0.044145 avg.loss:  2.002618 ETA:   0h 2m1Progress:  11.8% words/sec/thread:   47094 lr:  0.044111 avg.loss:  2.001757 ETA:   0h 2m1Progress:  11.8% words/sec/thread:   47080 lr:  0.044080 avg.loss:  2.001593 ETA:   0h 2m1Progress:  11.9% words/sec/thread:   47083 lr:  0.044046 avg.loss:  2.000973 ETA:   0h 2m1Progress:  12.0% words/sec/thread:   47085 lr:  0.044012 avg.loss:  2.000882 ETA:   0h 2m1Progress:  12.0% words/sec/thread:   47092 lr:  0.043978 avg.loss:  2.000377 ETA:   0h 2m1Progress:  12.1% words/sec/thread:   47097 lr:  0.043944 avg.loss:  2.000495 ETA:   0h 2m1Progress:  12.2% words/sec/thread:   47105 lr:  0.043909 avg.loss:  1.999742 ETA:   0h 2m1Progress:  12.2% words/sec/thread:   47106 lr:  0.043876 avg.loss:  1.999354 ETA:   0h 2m1Progress:  12.3% words/sec/thread:   47109 lr:  0.043842 avg.loss:  1.999247 ETA:   0h 2m1Progress:  12.4% words/sec/thread:   47114 lr:  0.043808 avg.loss:  1.999012 ETA:   0h 2m1Progress:  12.5% words/sec/thread:   47115 lr:  0.043774 avg.loss:  1.998751 ETA:   0h 2m1Progress:  12.5% words/sec/thread:   47121 lr:  0.043740 avg.loss:  1.998354 ETA:   0h 2m1Progress:  12.6% words/sec/thread:   47130 lr:  0.043705 avg.loss:  1.998106 ETA:   0h 2m1Progress:  12.7% words/sec/thread:   47134 lr:  0.043671 avg.loss:  1.997813 ETA:   0h 2m1Progress:  12.7% words/sec/thread:   47141 lr:  0.043637 avg.loss:  1.997025 ETA:   0h 2m1Progress:  12.8% words/sec/thread:   47142 lr:  0.043603 avg.loss:  1.996552 ETA:   0h 2m1Progress:  12.9% words/sec/thread:   47148 lr:  0.043569 avg.loss:  1.996498 ETA:   0h 2m1Progress:  12.9% words/sec/thread:   47154 lr:  0.043535 avg.loss:  1.996150 ETA:   0h 2m1Progress:  13.0% words/sec/thread:   47161 lr:  0.043500 avg.loss:  1.996118 ETA:   0h 2m1Progress:  13.1% words/sec/thread:   47168 lr:  0.043466 avg.loss:  1.995804 ETA:   0h 2m1Progress:  13.1% words/sec/thread:   47169 lr:  0.043432 avg.loss:  1.995000 ETA:   0h 2m Progress:  13.2% words/sec/thread:   47170 lr:  0.043398 avg.loss:  1.994849 ETA:   0h 2m Progress:  13.3% words/sec/thread:   47177 lr:  0.043364 avg.loss:  1.995038 ETA:   0h 2m Progress:  13.3% words/sec/thread:   47184 lr:  0.043329 avg.loss:  1.994753 ETA:   0h 2m Progress:  13.4% words/sec/thread:   47193 lr:  0.043295 avg.loss:  1.994093 ETA:   0h 2m Progress:  13.5% words/sec/thread:   47199 lr:  0.043260 avg.loss:  1.994019 ETA:   0h 2m Progress:  13.5% words/sec/thread:   47204 lr:  0.043226 avg.loss:  1.993877 ETA:   0h 2m Progress:  13.6% words/sec/thread:   47212 lr:  0.043191 avg.loss:  1.993634 ETA:   0h 2m Progress:  13.7% words/sec/thread:   47220 lr:  0.043157 avg.loss:  1.993200 ETA:   0h 2m Progress:  13.8% words/sec/thread:   47222 lr:  0.043123 avg.loss:  1.993004 ETA:   0h 2m Progress:  13.8% words/sec/thread:   47228 lr:  0.043088 avg.loss:  1.992787 ETA:   0h 2m Progress:  13.9% words/sec/thread:   47226 lr:  0.043055 avg.loss:  1.992395 ETA:   0h 2m Progress:  14.0% words/sec/thread:   47228 lr:  0.043021 avg.loss:  1.992184 ETA:   0h 2m Progress:  14.0% words/sec/thread:   47232 lr:  0.042987 avg.loss:  1.992028 ETA:   0h 2m Progress:  14.1% words/sec/thread:   47236 lr:  0.042953 avg.loss:  1.991802 ETA:   0h 2m Progress:  14.2% words/sec/thread:   47238 lr:  0.042919 avg.loss:  1.991314 ETA:   0h 2m Progress:  14.2% words/sec/thread:   47241 lr:  0.042885 avg.loss:  1.991176 ETA:   0h 2m Progress:  14.3% words/sec/thread:   47246 lr:  0.042851 avg.loss:  1.991288 ETA:   0h 2m Progress:  14.4% words/sec/thread:   47252 lr:  0.042816 avg.loss:  1.991122 ETA:   0h 2m Progress:  14.4% words/sec/thread:   47255 lr:  0.042782 avg.loss:  1.990821 ETA:   0h 2m Progress:  14.5% words/sec/thread:   47264 lr:  0.042747 avg.loss:  1.990304 ETA:   0h 2m Progress:  14.6% words/sec/thread:   47272 lr:  0.042713 avg.loss:  1.990313 ETA:   0h 2m Progress:  14.6% words/sec/thread:   47268 lr:  0.042680 avg.loss:  1.988021 ETA:   0h 2m Progress:  14.7% words/sec/thread:   47266 lr:  0.042647 avg.loss:  1.987799 ETA:   0h 2m Progress:  14.8% words/sec/thread:   47277 lr:  0.042611 avg.loss:  1.987239 ETA:   0h 2m Progress:  14.8% words/sec/thread:   47281 lr:  0.042577 avg.loss:  1.986758 ETA:   0h 2m Progress:  14.9% words/sec/thread:   47286 lr:  0.042543 avg.loss:  1.986496 ETA:   0h 2m Progress:  15.0% words/sec/thread:   47289 lr:  0.042509 avg.loss:  1.986372 ETA:   0h 2m Progress:  15.1% words/sec/thread:   47296 lr:  0.042474 avg.loss:  1.985976 ETA:   0h 2m Progress:  15.1% words/sec/thread:   47301 lr:  0.042439 avg.loss:  1.985547 ETA:   0h 2m Progress:  15.2% words/sec/thread:   47309 lr:  0.042405 avg.loss:  1.985065 ETA:   0h 2m Progress:  15.3% words/sec/thread:   47315 lr:  0.042370 avg.loss:  1.984890 ETA:   0h 2m Progress:  15.3% words/sec/thread:   47320 lr:  0.042336 avg.loss:  1.984461 ETA:   0h 2m Progress:  15.4% words/sec/thread:   47319 lr:  0.042302 avg.loss:  1.984053 ETA:   0h 2m Progress:  15.5% words/sec/thread:   47324 lr:  0.042268 avg.loss:  1.983710 ETA:   0h 2m Progress:  15.5% words/sec/thread:   47331 lr:  0.042233 avg.loss:  1.983649 ETA:   0h 2m Progress:  15.6% words/sec/thread:   47338 lr:  0.042198 avg.loss:  1.983331 ETA:   0h 2m Progress:  15.7% words/sec/thread:   47341 lr:  0.042164 avg.loss:  1.982884 ETA:   0h 2m Progress:  15.7% words/sec/thread:   47348 lr:  0.042129 avg.loss:  1.982520 ETA:   0h 2m Progress:  15.8% words/sec/thread:   47355 lr:  0.042095 avg.loss:  1.982322 ETA:   0h 2m Progress:  15.9% words/sec/thread:   47357 lr:  0.042061 avg.loss:  1.982050 ETA:   0h 2m Progress:  15.9% words/sec/thread:   47365 lr:  0.042026 avg.loss:  1.981822 ETA:   0h 2m Progress:  16.0% words/sec/thread:   47371 lr:  0.041991 avg.loss:  1.981804 ETA:   0h 2m Progress:  16.1% words/sec/thread:   47375 lr:  0.041957 avg.loss:  1.981419 ETA:   0h 2m Progress:  16.2% words/sec/thread:   47373 lr:  0.041923 avg.loss:  1.981391 ETA:   0h 2m Progress:  16.2% words/sec/thread:   47378 lr:  0.041889 avg.loss:  1.980989 ETA:   0h 2m Progress:  16.3% words/sec/thread:   47381 lr:  0.041855 avg.loss:  1.980789 ETA:   0h 2m Progress:  16.4% words/sec/thread:   47386 lr:  0.041820 avg.loss:  1.980549 ETA:   0h 2m Progress:  16.4% words/sec/thread:   47393 lr:  0.041785 avg.loss:  1.980464 ETA:   0h 2m Progress:  16.5% words/sec/thread:   47398 lr:  0.041751 avg.loss:  1.980335 ETA:   0h 2m Progress:  16.6% words/sec/thread:   47402 lr:  0.041716 avg.loss:  1.980248 ETA:   0h 2m Progress:  16.6% words/sec/thread:   47409 lr:  0.041682 avg.loss:  1.980062 ETA:   0h 2m Progress:  16.7% words/sec/thread:   47415 lr:  0.041647 avg.loss:  1.979842 ETA:   0h 2m Progress:  16.8% words/sec/thread:   47420 lr:  0.041612 avg.loss:  1.979638 ETA:   0h 2m Progress:  16.8% words/sec/thread:   47422 lr:  0.041578 avg.loss:  1.979521 ETA:   0h 2m Progress:  16.9% words/sec/thread:   47422 lr:  0.041545 avg.loss:  1.979354 ETA:   0h 2m Progress:  17.0% words/sec/thread:   47426 lr:  0.041510 avg.loss:  1.978924 ETA:   0h 2m Progress:  17.0% words/sec/thread:   47433 lr:  0.041475 avg.loss:  1.978746 ETA:   0h 2m Progress:  17.1% words/sec/thread:   47436 lr:  0.041441 avg.loss:  1.978587 ETA:   0h 2m Progress:  17.2% words/sec/thread:   47440 lr:  0.041407 avg.loss:  1.978159 ETA:   0h 2m Progress:  17.3% words/sec/thread:   47444 lr:  0.041372 avg.loss:  1.977659 ETA:   0h 2m Progress:  17.3% words/sec/thread:   47450 lr:  0.041337 avg.loss:  1.977554 ETA:   0h 2m Progress:  17.4% words/sec/thread:   47457 lr:  0.041302 avg.loss:  1.977258 ETA:   0h 2m Progress:  17.5% words/sec/thread:   47451 lr:  0.041269 avg.loss:  1.977106 ETA:   0h 2m Progress:  17.5% words/sec/thread:   47448 lr:  0.041236 avg.loss:  1.976583 ETA:   0h 2m Progress:  17.6% words/sec/thread:   47449 lr:  0.041202 avg.loss:  1.976533 ETA:   0h 2m Progress:  17.7% words/sec/thread:   47447 lr:  0.041169 avg.loss:  1.976297 ETA:   0h 2m Progress:  17.7% words/sec/thread:   47453 lr:  0.041134 avg.loss:  1.976289 ETA:   0h 2m Progress:  17.8% words/sec/thread:   47455 lr:  0.041100 avg.loss:  1.976166 ETA:   0h 2m Progress:  17.9% words/sec/thread:   47455 lr:  0.041066 avg.loss:  1.975987 ETA:   0h 2m Progress:  17.9% words/sec/thread:   47457 lr:  0.041032 avg.loss:  1.975215 ETA:   0h 2m Progress:  18.0% words/sec/thread:   47461 lr:  0.040998 avg.loss:  1.975045 ETA:   0h 2m Progress:  18.1% words/sec/thread:   47464 lr:  0.040963 avg.loss:  1.975065 ETA:   0h 2m Progress:  18.1% words/sec/thread:   47467 lr:  0.040929 avg.loss:  1.974975 ETA:   0h 2m Progress:  18.2% words/sec/thread:   47471 lr:  0.040894 avg.loss:  1.974740 ETA:   0h 2m Progress:  18.3% words/sec/thread:   47477 lr:  0.040859 avg.loss:  1.974515 ETA:   0h 2m Progress:  18.3% words/sec/thread:   47478 lr:  0.040826 avg.loss:  1.974542 ETA:   0h 2m Progress:  18.4% words/sec/thread:   47478 lr:  0.040792 avg.loss:  1.974363 ETA:   0h 2m Progress:  18.5% words/sec/thread:   47482 lr:  0.040757 avg.loss:  1.974212 ETA:   0h 2m Progress:  18.6% words/sec/thread:   47485 lr:  0.040723 avg.loss:  1.974078 ETA:   0h 2m Progress:  18.6% words/sec/thread:   47488 lr:  0.040689 avg.loss:  1.973863 ETA:   0h 2m Progress:  18.7% words/sec/thread:   47492 lr:  0.040654 avg.loss:  1.973563 ETA:   0h 2m Progress:  18.8% words/sec/thread:   47495 lr:  0.040620 avg.loss:  1.973274 ETA:   0h 2m Progress:  18.8% words/sec/thread:   47498 lr:  0.040585 avg.loss:  1.973146 ETA:   0h 2m Progress:  18.9% words/sec/thread:   47502 lr:  0.040551 avg.loss:  1.973033 ETA:   0h 2m Progress:  19.0% words/sec/thread:   47508 lr:  0.040516 avg.loss:  1.972431 ETA:   0h 2m Progress:  19.0% words/sec/thread:   47511 lr:  0.040481 avg.loss:  1.972060 ETA:   0h 2m Progress:  19.1% words/sec/thread:   47511 lr:  0.040448 avg.loss:  1.971961 ETA:   0h 2m Progress:  19.2% words/sec/thread:   47510 lr:  0.040414 avg.loss:  1.971686 ETA:   0h 2m Progress:  19.2% words/sec/thread:   47515 lr:  0.040379 avg.loss:  1.971388 ETA:   0h 1m5Progress:  19.3% words/sec/thread:   47514 lr:  0.040346 avg.loss:  1.971297 ETA:   0h 1m5Progress:  19.4% words/sec/thread:   47521 lr:  0.040310 avg.loss:  1.970873 ETA:   0h 1m5Progress:  19.4% words/sec/thread:   47527 lr:  0.040275 avg.loss:  1.970867 ETA:   0h 1m5Progress:  19.5% words/sec/thread:   47529 lr:  0.040241 avg.loss:  1.970405 ETA:   0h 1m5Progress:  19.6% words/sec/thread:   47535 lr:  0.040206 avg.loss:  1.970235 ETA:   0h 1m5Progress:  19.7% words/sec/thread:   47535 lr:  0.040172 avg.loss:  1.970253 ETA:   0h 1m5Progress:  19.7% words/sec/thread:   47541 lr:  0.040137 avg.loss:  1.969994 ETA:   0h 1m5Progress:  19.8% words/sec/thread:   47544 lr:  0.040103 avg.loss:  1.969799 ETA:   0h 1m5Progress:  19.9% words/sec/thread:   47543 lr:  0.040069 avg.loss:  1.969656 ETA:   0h 1m5Progress:  19.9% words/sec/thread:   47547 lr:  0.040035 avg.loss:  1.969425 ETA:   0h 1m5Progress:  20.0% words/sec/thread:   47551 lr:  0.040000 avg.loss:  1.969419 ETA:   0h 1m5Progress:  20.1% words/sec/thread:   47555 lr:  0.039966 avg.loss:  1.969298 ETA:   0h 1m5Progress:  20.1% words/sec/thread:   47561 lr:  0.039931 avg.loss:  1.969217 ETA:   0h 1m5Progress:  20.2% words/sec/thread:   47564 lr:  0.039896 avg.loss:  1.969105 ETA:   0h 1m5Progress:  20.3% words/sec/thread:   47567 lr:  0.039862 avg.loss:  1.968933 ETA:   0h 1m5Progress:  20.3% words/sec/thread:   47573 lr:  0.039827 avg.loss:  1.968603 ETA:   0h 1m5Progress:  20.4% words/sec/thread:   47576 lr:  0.039792 avg.loss:  1.968230 ETA:   0h 1m5Progress:  20.5% words/sec/thread:   47579 lr:  0.039758 avg.loss:  1.968106 ETA:   0h 1m5Progress:  20.6% words/sec/thread:   47580 lr:  0.039724 avg.loss:  1.967770 ETA:   0h 1m5Progress:  20.6% words/sec/thread:   47578 lr:  0.039691 avg.loss:  1.967647 ETA:   0h 1m5Progress:  20.7% words/sec/thread:   47581 lr:  0.039656 avg.loss:  1.967216 ETA:   0h 1m5Progress:  20.8% words/sec/thread:   47585 lr:  0.039621 avg.loss:  1.967039 ETA:   0h 1m5Progress:  20.8% words/sec/thread:   47588 lr:  0.039587 avg.loss:  1.967027 ETA:   0h 1m5Progress:  20.9% words/sec/thread:   47592 lr:  0.039552 avg.loss:  1.967063 ETA:   0h 1m5Progress:  21.0% words/sec/thread:   47596 lr:  0.039518 avg.loss:  1.966738 ETA:   0h 1m5Progress:  21.0% words/sec/thread:   47598 lr:  0.039483 avg.loss:  1.966653 ETA:   0h 1m5Progress:  21.1% words/sec/thread:   47601 lr:  0.039449 avg.loss:  1.965580 ETA:   0h 1m5Progress:  21.2% words/sec/thread:   47603 lr:  0.039415 avg.loss:  1.965441 ETA:   0h 1m5Progress:  21.2% words/sec/thread:   47607 lr:  0.039380 avg.loss:  1.965408 ETA:   0h 1m5Progress:  21.3% words/sec/thread:   47607 lr:  0.039346 avg.loss:  1.965039 ETA:   0h 1m5Progress:  21.4% words/sec/thread:   47605 lr:  0.039313 avg.loss:  1.964808 ETA:   0h 1m5Progress:  21.4% words/sec/thread:   47607 lr:  0.039278 avg.loss:  1.964786 ETA:   0h 1m5Progress:  21.5% words/sec/thread:   47610 lr:  0.039244 avg.loss:  1.964719 ETA:   0h 1m5Progress:  21.6% words/sec/thread:   47613 lr:  0.039209 avg.loss:  1.964724 ETA:   0h 1m5Progress:  21.6% words/sec/thread:   47615 lr:  0.039175 avg.loss:  1.964398 ETA:   0h 1m5Progress:  21.7% words/sec/thread:   47618 lr:  0.039141 avg.loss:  1.964075 ETA:   0h 1m5Progress:  21.8% words/sec/thread:   47624 lr:  0.039106 avg.loss:  1.963906 ETA:   0h 1m5Progress:  21.9% words/sec/thread:   47626 lr:  0.039071 avg.loss:  1.963367 ETA:   0h 1m5Progress:  21.9% words/sec/thread:   47630 lr:  0.039037 avg.loss:  1.963211 ETA:   0h 1m5Progress:  22.0% words/sec/thread:   47634 lr:  0.039002 avg.loss:  1.961842 ETA:   0h 1m5Progress:  22.1% words/sec/thread:   47633 lr:  0.038968 avg.loss:  1.961677 ETA:   0h 1m5Progress:  22.1% words/sec/thread:   47631 lr:  0.038935 avg.loss:  1.961482 ETA:   0h 1m5Progress:  22.2% words/sec/thread:   47635 lr:  0.038900 avg.loss:  1.961583 ETA:   0h 1m5Progress:  22.3% words/sec/thread:   47638 lr:  0.038865 avg.loss:  1.961607 ETA:   0h 1m5Progress:  22.3% words/sec/thread:   47642 lr:  0.038831 avg.loss:  1.961528 ETA:   0h 1m5Progress:  22.4% words/sec/thread:   47645 lr:  0.038796 avg.loss:  1.961446 ETA:   0h 1m5Progress:  22.5% words/sec/thread:   47648 lr:  0.038762 avg.loss:  1.959910 ETA:   0h 1m5Progress:  22.5% words/sec/thread:   47655 lr:  0.038726 avg.loss:  1.959914 ETA:   0h 1m5Progress:  22.6% words/sec/thread:   47655 lr:  0.038692 avg.loss:  1.959722 ETA:   0h 1m5Progress:  22.7% words/sec/thread:   47659 lr:  0.038658 avg.loss:  1.959591 ETA:   0h 1m5Progress:  22.8% words/sec/thread:   47662 lr:  0.038623 avg.loss:  1.959710 ETA:   0h 1m5Progress:  22.8% words/sec/thread:   47660 lr:  0.038590 avg.loss:  1.959456 ETA:   0h 1m5Progress:  22.9% words/sec/thread:   47663 lr:  0.038555 avg.loss:  1.959199 ETA:   0h 1m5Progress:  23.0% words/sec/thread:   47664 lr:  0.038521 avg.loss:  1.959096 ETA:   0h 1m5Progress:  23.0% words/sec/thread:   47667 lr:  0.038486 avg.loss:  1.958971 ETA:   0h 1m5Progress:  23.1% words/sec/thread:   47671 lr:  0.038452 avg.loss:  1.958821 ETA:   0h 1m5Progress:  23.2% words/sec/thread:   47672 lr:  0.038418 avg.loss:  1.958608 ETA:   0h 1m5Progress:  23.2% words/sec/thread:   47675 lr:  0.038383 avg.loss:  1.958645 ETA:   0h 1m5Progress:  23.3% words/sec/thread:   47678 lr:  0.038348 avg.loss:  1.958429 ETA:   0h 1m5Progress:  23.4% words/sec/thread:   47682 lr:  0.038314 avg.loss:  1.958347 ETA:   0h 1m5Progress:  23.4% words/sec/thread:   47683 lr:  0.038279 avg.loss:  1.957859 ETA:   0h 1m5Progress:  23.5% words/sec/thread:   47685 lr:  0.038245 avg.loss:  1.957645 ETA:   0h 1m5Progress:  23.6% words/sec/thread:   47684 lr:  0.038211 avg.loss:  1.957606 ETA:   0h 1m5Progress:  23.6% words/sec/thread:   47686 lr:  0.038177 avg.loss:  1.957411 ETA:   0h 1m5Progress:  23.7% words/sec/thread:   47688 lr:  0.038143 avg.loss:  1.957204 ETA:   0h 1m5Progress:  23.8% words/sec/thread:   47691 lr:  0.038108 avg.loss:  1.957119 ETA:   0h 1m5Progress:  23.9% words/sec/thread:   47692 lr:  0.038074 avg.loss:  1.957080 ETA:   0h 1m5Progress:  23.9% words/sec/thread:   47695 lr:  0.038040 avg.loss:  1.956544 ETA:   0h 1m5Progress:  24.0% words/sec/thread:   47696 lr:  0.038005 avg.loss:  1.956007 ETA:   0h 1m5Progress:  24.1% words/sec/thread:   47701 lr:  0.037970 avg.loss:  1.955821 ETA:   0h 1m5Progress:  24.1% words/sec/thread:   47702 lr:  0.037936 avg.loss:  1.955665 ETA:   0h 1m5Progress:  24.2% words/sec/thread:   47704 lr:  0.037902 avg.loss:  1.955064 ETA:   0h 1m5Progress:  24.3% words/sec/thread:   47704 lr:  0.037868 avg.loss:  1.954859 ETA:   0h 1m5Progress:  24.3% words/sec/thread:   47702 lr:  0.037835 avg.loss:  1.954437 ETA:   0h 1m5Progress:  24.4% words/sec/thread:   47704 lr:  0.037800 avg.loss:  1.954162 ETA:   0h 1m5Progress:  24.5% words/sec/thread:   47706 lr:  0.037766 avg.loss:  1.954121 ETA:   0h 1m5Progress:  24.5% words/sec/thread:   47709 lr:  0.037731 avg.loss:  1.954088 ETA:   0h 1m5Progress:  24.6% words/sec/thread:   47712 lr:  0.037697 avg.loss:  1.953974 ETA:   0h 1m5Progress:  24.7% words/sec/thread:   47713 lr:  0.037662 avg.loss:  1.953785 ETA:   0h 1m5Progress:  24.7% words/sec/thread:   47716 lr:  0.037628 avg.loss:  1.953672 ETA:   0h 1m5Progress:  24.8% words/sec/thread:   47718 lr:  0.037593 avg.loss:  1.953428 ETA:   0h 1m5Progress:  24.9% words/sec/thread:   47721 lr:  0.037559 avg.loss:  1.953296 ETA:   0h 1m5Progress:  25.0% words/sec/thread:   47724 lr:  0.037524 avg.loss:  1.953138 ETA:   0h 1m5Progress:  25.0% words/sec/thread:   47721 lr:  0.037491 avg.loss:  1.953066 ETA:   0h 1m5Progress:  25.1% words/sec/thread:   47721 lr:  0.037457 avg.loss:  1.952833 ETA:   0h 1m5Progress:  25.2% words/sec/thread:   47722 lr:  0.037423 avg.loss:  1.952802 ETA:   0h 1m5Progress:  25.2% words/sec/thread:   47724 lr:  0.037388 avg.loss:  1.952670 ETA:   0h 1m5Progress:  25.3% words/sec/thread:   47727 lr:  0.037354 avg.loss:  1.952466 ETA:   0h 1m5Progress:  25.4% words/sec/thread:   47731 lr:  0.037319 avg.loss:  1.952368 ETA:   0h 1m5Progress:  25.4% words/sec/thread:   47733 lr:  0.037284 avg.loss:  1.952271 ETA:   0h 1m5Progress:  25.5% words/sec/thread:   47735 lr:  0.037250 avg.loss:  1.952162 ETA:   0h 1m5Progress:  25.6% words/sec/thread:   47738 lr:  0.037215 avg.loss:  1.951982 ETA:   0h 1m4Progress:  25.6% words/sec/thread:   47740 lr:  0.037181 avg.loss:  1.951980 ETA:   0h 1m4Progress:  25.7% words/sec/thread:   47743 lr:  0.037146 avg.loss:  1.951537 ETA:   0h 1m4Progress:  25.8% words/sec/thread:   47742 lr:  0.037112 avg.loss:  1.950950 ETA:   0h 1m4Progress:  25.8% words/sec/thread:   47740 lr:  0.037079 avg.loss:  1.950755 ETA:   0h 1m4Progress:  25.9% words/sec/thread:   47739 lr:  0.037045 avg.loss:  1.950697 ETA:   0h 1m4Progress:  26.0% words/sec/thread:   47742 lr:  0.037011 avg.loss:  1.950384 ETA:   0h 1m4Progress:  26.0% words/sec/thread:   47744 lr:  0.036976 avg.loss:  1.950025 ETA:   0h 1m4Progress:  26.1% words/sec/thread:   47746 lr:  0.036942 avg.loss:  1.949712 ETA:   0h 1m4Progress:  26.2% words/sec/thread:   47749 lr:  0.036907 avg.loss:  1.949597 ETA:   0h 1m4Progress:  26.3% words/sec/thread:   47752 lr:  0.036872 avg.loss:  1.949319 ETA:   0h 1m4Progress:  26.3% words/sec/thread:   47755 lr:  0.036838 avg.loss:  1.949227 ETA:   0h 1m4Progress:  26.4% words/sec/thread:   47759 lr:  0.036803 avg.loss:  1.949054 ETA:   0h 1m4Progress:  26.5% words/sec/thread:   47762 lr:  0.036768 avg.loss:  1.949094 ETA:   0h 1m4Progress:  26.5% words/sec/thread:   47760 lr:  0.036734 avg.loss:  1.949093 ETA:   0h 1m4Progress:  26.6% words/sec/thread:   47759 lr:  0.036701 avg.loss:  1.948441 ETA:   0h 1m4Progress:  26.7% words/sec/thread:   47761 lr:  0.036666 avg.loss:  1.948208 ETA:   0h 1m4Progress:  26.7% words/sec/thread:   47765 lr:  0.036631 avg.loss:  1.947941 ETA:   0h 1m4Progress:  26.8% words/sec/thread:   47766 lr:  0.036597 avg.loss:  1.947776 ETA:   0h 1m4Progress:  26.9% words/sec/thread:   47769 lr:  0.036562 avg.loss:  1.947479 ETA:   0h 1m4Progress:  26.9% words/sec/thread:   47773 lr:  0.036527 avg.loss:  1.947414 ETA:   0h 1m4Progress:  27.0% words/sec/thread:   47776 lr:  0.036492 avg.loss:  1.947087 ETA:   0h 1m4Progress:  27.1% words/sec/thread:   47779 lr:  0.036458 avg.loss:  1.947050 ETA:   0h 1m4Progress:  27.2% words/sec/thread:   47783 lr:  0.036423 avg.loss:  1.946941 ETA:   0h 1m4Progress:  27.2% words/sec/thread:   47785 lr:  0.036388 avg.loss:  1.946805 ETA:   0h 1m4Progress:  27.3% words/sec/thread:   47784 lr:  0.036354 avg.loss:  1.946690 ETA:   0h 1m4Progress:  27.4% words/sec/thread:   47783 lr:  0.036321 avg.loss:  1.946110 ETA:   0h 1m4Progress:  27.4% words/sec/thread:   47784 lr:  0.036287 avg.loss:  1.946093 ETA:   0h 1m4Progress:  27.5% words/sec/thread:   47785 lr:  0.036253 avg.loss:  1.945987 ETA:   0h 1m4Progress:  27.6% words/sec/thread:   47786 lr:  0.036218 avg.loss:  1.945710 ETA:   0h 1m4Progress:  27.6% words/sec/thread:   47787 lr:  0.036184 avg.loss:  1.945659 ETA:   0h 1m4Progress:  27.7% words/sec/thread:   47792 lr:  0.036149 avg.loss:  1.945471 ETA:   0h 1m4Progress:  27.8% words/sec/thread:   47791 lr:  0.036115 avg.loss:  1.945422 ETA:   0h 1m4Progress:  27.8% words/sec/thread:   47793 lr:  0.036080 avg.loss:  1.945381 ETA:   0h 1m4Progress:  27.9% words/sec/thread:   47795 lr:  0.036046 avg.loss:  1.945382 ETA:   0h 1m4Progress:  28.0% words/sec/thread:   47797 lr:  0.036011 avg.loss:  1.945282 ETA:   0h 1m4Progress:  28.0% words/sec/thread:   47797 lr:  0.035978 avg.loss:  1.945261 ETA:   0h 1m4Progress:  28.1% words/sec/thread:   47797 lr:  0.035944 avg.loss:  1.945148 ETA:   0h 1m4Progress:  28.2% words/sec/thread:   47799 lr:  0.035909 avg.loss:  1.944907 ETA:   0h 1m4Progress:  28.3% words/sec/thread:   47800 lr:  0.035875 avg.loss:  1.944710 ETA:   0h 1m4Progress:  28.3% words/sec/thread:   47803 lr:  0.035840 avg.loss:  1.944515 ETA:   0h 1m4Progress:  28.4% words/sec/thread:   47804 lr:  0.035806 avg.loss:  1.943331 ETA:   0h 1m4Progress:  28.5% words/sec/thread:   47806 lr:  0.035771 avg.loss:  1.943280 ETA:   0h 1m4Progress:  28.5% words/sec/thread:   47809 lr:  0.035736 avg.loss:  1.943072 ETA:   0h 1m4Progress:  28.6% words/sec/thread:   47810 lr:  0.035702 avg.loss:  1.943050 ETA:   0h 1m4Progress:  28.7% words/sec/thread:   47813 lr:  0.035667 avg.loss:  1.943036 ETA:   0h 1m4Progress:  28.7% words/sec/thread:   47814 lr:  0.035633 avg.loss:  1.942577 ETA:   0h 1m4Progress:  28.8% words/sec/thread:   47813 lr:  0.035599 avg.loss:  1.942103 ETA:   0h 1m4Progress:  28.9% words/sec/thread:   47812 lr:  0.035566 avg.loss:  1.941999 ETA:   0h 1m4Progress:  28.9% words/sec/thread:   47815 lr:  0.035531 avg.loss:  1.941913 ETA:   0h 1m4Progress:  29.0% words/sec/thread:   47811 lr:  0.035498 avg.loss:  1.941888 ETA:   0h 1m4Progress:  29.1% words/sec/thread:   47812 lr:  0.035464 avg.loss:  1.941908 ETA:   0h 1m4Progress:  29.1% words/sec/thread:   47814 lr:  0.035429 avg.loss:  1.941484 ETA:   0h 1m4Progress:  29.2% words/sec/thread:   47817 lr:  0.035394 avg.loss:  1.941329 ETA:   0h 1m4Progress:  29.3% words/sec/thread:   47820 lr:  0.035359 avg.loss:  1.941177 ETA:   0h 1m4Progress:  29.4% words/sec/thread:   47824 lr:  0.035324 avg.loss:  1.940811 ETA:   0h 1m4Progress:  29.4% words/sec/thread:   47826 lr:  0.035290 avg.loss:  1.940716 ETA:   0h 1m4Progress:  29.5% words/sec/thread:   47826 lr:  0.035256 avg.loss:  1.940646 ETA:   0h 1m4Progress:  29.6% words/sec/thread:   47825 lr:  0.035222 avg.loss:  1.940598 ETA:   0h 1m4Progress:  29.6% words/sec/thread:   47826 lr:  0.035188 avg.loss:  1.940569 ETA:   0h 1m4Progress:  29.7% words/sec/thread:   47826 lr:  0.035153 avg.loss:  1.940386 ETA:   0h 1m4Progress:  29.8% words/sec/thread:   47827 lr:  0.035119 avg.loss:  1.940266 ETA:   0h 1m4Progress:  29.8% words/sec/thread:   47827 lr:  0.035085 avg.loss:  1.940202 ETA:   0h 1m4Progress:  29.9% words/sec/thread:   47828 lr:  0.035051 avg.loss:  1.940069 ETA:   0h 1m4Progress:  30.0% words/sec/thread:   47829 lr:  0.035017 avg.loss:  1.939821 ETA:   0h 1m4Progress:  30.0% words/sec/thread:   47829 lr:  0.034983 avg.loss:  1.939293 ETA:   0h 1m4Progress:  30.1% words/sec/thread:   47832 lr:  0.034948 avg.loss:  1.939023 ETA:   0h 1m4Progress:  30.2% words/sec/thread:   47833 lr:  0.034914 avg.loss:  1.938930 ETA:   0h 1m4Progress:  30.2% words/sec/thread:   47835 lr:  0.034879 avg.loss:  1.939012 ETA:   0h 1m4Progress:  30.3% words/sec/thread:   47832 lr:  0.034846 avg.loss:  1.938934 ETA:   0h 1m4Progress:  30.4% words/sec/thread:   47834 lr:  0.034811 avg.loss:  1.938812 ETA:   0h 1m4Progress:  30.4% words/sec/thread:   47834 lr:  0.034777 avg.loss:  1.938844 ETA:   0h 1m4Progress:  30.5% words/sec/thread:   47833 lr:  0.034744 avg.loss:  1.938759 ETA:   0h 1m4Progress:  30.6% words/sec/thread:   47835 lr:  0.034709 avg.loss:  1.938646 ETA:   0h 1m4Progress:  30.7% words/sec/thread:   47837 lr:  0.034675 avg.loss:  1.938513 ETA:   0h 1m4Progress:  30.7% words/sec/thread:   47839 lr:  0.034640 avg.loss:  1.938349 ETA:   0h 1m4Progress:  30.8% words/sec/thread:   47840 lr:  0.034606 avg.loss:  1.938204 ETA:   0h 1m4Progress:  30.9% words/sec/thread:   47841 lr:  0.034572 avg.loss:  1.938008 ETA:   0h 1m4Progress:  30.9% words/sec/thread:   47844 lr:  0.034536 avg.loss:  1.937871 ETA:   0h 1m4Progress:  31.0% words/sec/thread:   47845 lr:  0.034502 avg.loss:  1.937708 ETA:   0h 1m4Progress:  31.1% words/sec/thread:   47843 lr:  0.034469 avg.loss:  1.937587 ETA:   0h 1m4Progress:  31.1% words/sec/thread:   47845 lr:  0.034434 avg.loss:  1.937503 ETA:   0h 1m4Progress:  31.2% words/sec/thread:   47847 lr:  0.034400 avg.loss:  1.937284 ETA:   0h 1m4Progress:  31.3% words/sec/thread:   47849 lr:  0.034365 avg.loss:  1.937279 ETA:   0h 1m4Progress:  31.3% words/sec/thread:   47850 lr:  0.034331 avg.loss:  1.937223 ETA:   0h 1m4Progress:  31.4% words/sec/thread:   47853 lr:  0.034296 avg.loss:  1.937231 ETA:   0h 1m4Progress:  31.5% words/sec/thread:   47854 lr:  0.034261 avg.loss:  1.937158 ETA:   0h 1m4Progress:  31.5% words/sec/thread:   47855 lr:  0.034227 avg.loss:  1.937194 ETA:   0h 1m4Progress:  31.6% words/sec/thread:   47857 lr:  0.034193 avg.loss:  1.936589 ETA:   0h 1m4Progress:  31.7% words/sec/thread:   47858 lr:  0.034158 avg.loss:  1.936503 ETA:   0h 1m4Progress:  31.8% words/sec/thread:   47856 lr:  0.034125 avg.loss:  1.936376 ETA:   0h 1m4Progress:  31.8% words/sec/thread:   47856 lr:  0.034091 avg.loss:  1.936197 ETA:   0h 1m4Progress:  31.9% words/sec/thread:   47858 lr:  0.034056 avg.loss:  1.936169 ETA:   0h 1m4Progress:  32.0% words/sec/thread:   47860 lr:  0.034022 avg.loss:  1.936091 ETA:   0h 1m4Progress:  32.0% words/sec/thread:   47861 lr:  0.033987 avg.loss:  1.935953 ETA:   0h 1m4Progress:  32.1% words/sec/thread:   47861 lr:  0.033953 avg.loss:  1.935971 ETA:   0h 1m4Progress:  32.2% words/sec/thread:   47862 lr:  0.033919 avg.loss:  1.935974 ETA:   0h 1m3Progress:  32.2% words/sec/thread:   47865 lr:  0.033884 avg.loss:  1.935857 ETA:   0h 1m3Progress:  32.3% words/sec/thread:   47867 lr:  0.033849 avg.loss:  1.935732 ETA:   0h 1m3Progress:  32.4% words/sec/thread:   47868 lr:  0.033815 avg.loss:  1.935597 ETA:   0h 1m3Progress:  32.4% words/sec/thread:   47867 lr:  0.033781 avg.loss:  1.935485 ETA:   0h 1m3Progress:  32.5% words/sec/thread:   47867 lr:  0.033747 avg.loss:  1.935500 ETA:   0h 1m3Progress:  32.6% words/sec/thread:   47866 lr:  0.033714 avg.loss:  1.935339 ETA:   0h 1m3Progress:  32.6% words/sec/thread:   47867 lr:  0.033679 avg.loss:  1.935017 ETA:   0h 1m3Progress:  32.7% words/sec/thread:   47870 lr:  0.033644 avg.loss:  1.934907 ETA:   0h 1m3Progress:  32.8% words/sec/thread:   47872 lr:  0.033610 avg.loss:  1.934709 ETA:   0h 1m3Progress:  32.8% words/sec/thread:   47874 lr:  0.033575 avg.loss:  1.934455 ETA:   0h 1m3Progress:  32.9% words/sec/thread:   47875 lr:  0.033541 avg.loss:  1.934363 ETA:   0h 1m3Progress:  33.0% words/sec/thread:   47874 lr:  0.033507 avg.loss:  1.934025 ETA:   0h 1m3Progress:  33.1% words/sec/thread:   47876 lr:  0.033472 avg.loss:  1.934024 ETA:   0h 1m3Progress:  33.1% words/sec/thread:   47878 lr:  0.033438 avg.loss:  1.934063 ETA:   0h 1m3Progress:  33.2% words/sec/thread:   47875 lr:  0.033405 avg.loss:  1.933623 ETA:   0h 1m3Progress:  33.3% words/sec/thread:   47874 lr:  0.033371 avg.loss:  1.933436 ETA:   0h 1m3Progress:  33.3% words/sec/thread:   47872 lr:  0.033338 avg.loss:  1.933385 ETA:   0h 1m3Progress:  33.4% words/sec/thread:   47876 lr:  0.033303 avg.loss:  1.933379 ETA:   0h 1m3Progress:  33.5% words/sec/thread:   47877 lr:  0.033268 avg.loss:  1.933276 ETA:   0h 1m3Progress:  33.5% words/sec/thread:   47879 lr:  0.033234 avg.loss:  1.932957 ETA:   0h 1m3Progress:  33.6% words/sec/thread:   47881 lr:  0.033199 avg.loss:  1.932964 ETA:   0h 1m3Progress:  33.7% words/sec/thread:   47880 lr:  0.033165 avg.loss:  1.932904 ETA:   0h 1m3Progress:  33.7% words/sec/thread:   47881 lr:  0.033131 avg.loss:  1.932830 ETA:   0h 1m3Progress:  33.8% words/sec/thread:   47881 lr:  0.033097 avg.loss:  1.932677 ETA:   0h 1m3Progress:  33.9% words/sec/thread:   47883 lr:  0.033062 avg.loss:  1.932485 ETA:   0h 1m3Progress:  33.9% words/sec/thread:   47880 lr:  0.033029 avg.loss:  1.932498 ETA:   0h 1m3Progress:  34.0% words/sec/thread:   47878 lr:  0.032996 avg.loss:  1.932405 ETA:   0h 1m3Progress:  34.1% words/sec/thread:   47879 lr:  0.032962 avg.loss:  1.932400 ETA:   0h 1m3Progress:  34.1% words/sec/thread:   47879 lr:  0.032927 avg.loss:  1.932327 ETA:   0h 1m3Progress:  34.2% words/sec/thread:   47882 lr:  0.032893 avg.loss:  1.932289 ETA:   0h 1m3Progress:  34.3% words/sec/thread:   47882 lr:  0.032859 avg.loss:  1.932146 ETA:   0h 1m3Progress:  34.4% words/sec/thread:   47884 lr:  0.032824 avg.loss:  1.932037 ETA:   0h 1m3Progress:  34.4% words/sec/thread:   47885 lr:  0.032789 avg.loss:  1.931795 ETA:   0h 1m3Progress:  34.5% words/sec/thread:   47885 lr:  0.032756 avg.loss:  1.931657 ETA:   0h 1m3Progress:  34.6% words/sec/thread:   47886 lr:  0.032721 avg.loss:  1.931388 ETA:   0h 1m3Progress:  34.6% words/sec/thread:   47889 lr:  0.032686 avg.loss:  1.931295 ETA:   0h 1m3Progress:  34.7% words/sec/thread:   47889 lr:  0.032652 avg.loss:  1.931120 ETA:   0h 1m3Progress:  34.8% words/sec/thread:   47886 lr:  0.032619 avg.loss:  1.930976 ETA:   0h 1m3Progress:  34.8% words/sec/thread:   47888 lr:  0.032584 avg.loss:  1.930914 ETA:   0h 1m3Progress:  34.9% words/sec/thread:   47889 lr:  0.032550 avg.loss:  1.930817 ETA:   0h 1m3Progress:  35.0% words/sec/thread:   47892 lr:  0.032515 avg.loss:  1.930755 ETA:   0h 1m3Progress:  35.0% words/sec/thread:   47895 lr:  0.032480 avg.loss:  1.930655 ETA:   0h 1m3Progress:  35.1% words/sec/thread:   47896 lr:  0.032445 avg.loss:  1.930358 ETA:   0h 1m3Progress:  35.2% words/sec/thread:   47899 lr:  0.032410 avg.loss:  1.930318 ETA:   0h 1m3Progress:  35.2% words/sec/thread:   47901 lr:  0.032376 avg.loss:  1.930245 ETA:   0h 1m3Progress:  35.3% words/sec/thread:   47903 lr:  0.032341 avg.loss:  1.930228 ETA:   0h 1m3Progress:  35.4% words/sec/thread:   47904 lr:  0.032307 avg.loss:  1.930202 ETA:   0h 1m3Progress:  35.5% words/sec/thread:   47904 lr:  0.032272 avg.loss:  1.930108 ETA:   0h 1m3Progress:  35.5% words/sec/thread:   47901 lr:  0.032240 avg.loss:  1.930086 ETA:   0h 1m3Progress:  35.6% words/sec/thread:   47901 lr:  0.032206 avg.loss:  1.930065 ETA:   0h 1m3Progress:  35.7% words/sec/thread:   47902 lr:  0.032171 avg.loss:  1.929981 ETA:   0h 1m3Progress:  35.7% words/sec/thread:   47904 lr:  0.032136 avg.loss:  1.929853 ETA:   0h 1m3Progress:  35.8% words/sec/thread:   47905 lr:  0.032102 avg.loss:  1.929798 ETA:   0h 1m3Progress:  35.9% words/sec/thread:   47899 lr:  0.032070 avg.loss:  1.929764 ETA:   0h 1m3Progress:  35.9% words/sec/thread:   47900 lr:  0.032036 avg.loss:  1.929447 ETA:   0h 1m3Progress:  36.0% words/sec/thread:   47901 lr:  0.032001 avg.loss:  1.929399 ETA:   0h 1m3Progress:  36.1% words/sec/thread:   47903 lr:  0.031966 avg.loss:  1.929365 ETA:   0h 1m3Progress:  36.1% words/sec/thread:   47904 lr:  0.031932 avg.loss:  1.929303 ETA:   0h 1m3Progress:  36.2% words/sec/thread:   47905 lr:  0.031898 avg.loss:  1.929247 ETA:   0h 1m3Progress:  36.3% words/sec/thread:   47905 lr:  0.031864 avg.loss:  1.929343 ETA:   0h 1m3Progress:  36.3% words/sec/thread:   47907 lr:  0.031829 avg.loss:  1.929292 ETA:   0h 1m3Progress:  36.4% words/sec/thread:   47906 lr:  0.031795 avg.loss:  1.929132 ETA:   0h 1m3Progress:  36.5% words/sec/thread:   47907 lr:  0.031761 avg.loss:  1.929044 ETA:   0h 1m3Progress:  36.5% words/sec/thread:   47909 lr:  0.031726 avg.loss:  1.929143 ETA:   0h 1m3Progress:  36.6% words/sec/thread:   47911 lr:  0.031691 avg.loss:  1.929080 ETA:   0h 1m3Progress:  36.7% words/sec/thread:   47911 lr:  0.031657 avg.loss:  1.929034 ETA:   0h 1m3Progress:  36.8% words/sec/thread:   47913 lr:  0.031622 avg.loss:  1.928789 ETA:   0h 1m3Progress:  36.8% words/sec/thread:   47914 lr:  0.031588 avg.loss:  1.928675 ETA:   0h 1m3Progress:  36.9% words/sec/thread:   47914 lr:  0.031554 avg.loss:  1.928654 ETA:   0h 1m3Progress:  37.0% words/sec/thread:   47913 lr:  0.031521 avg.loss:  1.928379 ETA:   0h 1m3Progress:  37.0% words/sec/thread:   47913 lr:  0.031486 avg.loss:  1.928239 ETA:   0h 1m3Progress:  37.1% words/sec/thread:   47914 lr:  0.031452 avg.loss:  1.928329 ETA:   0h 1m3Progress:  37.2% words/sec/thread:   47916 lr:  0.031417 avg.loss:  1.928085 ETA:   0h 1m3Progress:  37.2% words/sec/thread:   47917 lr:  0.031383 avg.loss:  1.928131 ETA:   0h 1m3Progress:  37.3% words/sec/thread:   47919 lr:  0.031348 avg.loss:  1.927909 ETA:   0h 1m3Progress:  37.4% words/sec/thread:   47921 lr:  0.031313 avg.loss:  1.927866 ETA:   0h 1m3Progress:  37.4% words/sec/thread:   47921 lr:  0.031279 avg.loss:  1.927842 ETA:   0h 1m3Progress:  37.5% words/sec/thread:   47922 lr:  0.031245 avg.loss:  1.927736 ETA:   0h 1m3Progress:  37.6% words/sec/thread:   47923 lr:  0.031211 avg.loss:  1.927656 ETA:   0h 1m3Progress:  37.6% words/sec/thread:   47921 lr:  0.031177 avg.loss:  1.927399 ETA:   0h 1m3Progress:  37.7% words/sec/thread:   47920 lr:  0.031143 avg.loss:  1.927305 ETA:   0h 1m3Progress:  37.8% words/sec/thread:   47920 lr:  0.031110 avg.loss:  1.927208 ETA:   0h 1m3Progress:  37.9% words/sec/thread:   47923 lr:  0.031074 avg.loss:  1.927081 ETA:   0h 1m3Progress:  37.9% words/sec/thread:   47925 lr:  0.031039 avg.loss:  1.927113 ETA:   0h 1m3Progress:  38.0% words/sec/thread:   47925 lr:  0.031005 avg.loss:  1.926934 ETA:   0h 1m3Progress:  38.1% words/sec/thread:   47927 lr:  0.030971 avg.loss:  1.926771 ETA:   0h 1m3Progress:  38.1% words/sec/thread:   47929 lr:  0.030936 avg.loss:  1.926769 ETA:   0h 1m3Progress:  38.2% words/sec/thread:   47930 lr:  0.030901 avg.loss:  1.926740 ETA:   0h 1m3Progress:  38.3% words/sec/thread:   47931 lr:  0.030867 avg.loss:  1.926556 ETA:   0h 1m3Progress:  38.3% words/sec/thread:   47933 lr:  0.030832 avg.loss:  1.926442 ETA:   0h 1m3Progress:  38.4% words/sec/thread:   47932 lr:  0.030798 avg.loss:  1.926479 ETA:   0h 1m3Progress:  38.5% words/sec/thread:   47931 lr:  0.030765 avg.loss:  1.926333 ETA:   0h 1m3Progress:  38.5% words/sec/thread:   47932 lr:  0.030730 avg.loss:  1.926344 ETA:   0h 1m3Progress:  38.6% words/sec/thread:   47934 lr:  0.030695 avg.loss:  1.926266 ETA:   0h 1m3Progress:  38.7% words/sec/thread:   47935 lr:  0.030661 avg.loss:  1.926209 ETA:   0h 1m3Progress:  38.7% words/sec/thread:   47936 lr:  0.030627 avg.loss:  1.926071 ETA:   0h 1m3Progress:  38.8% words/sec/thread:   47938 lr:  0.030592 avg.loss:  1.926088 ETA:   0h 1m3Progress:  38.9% words/sec/thread:   47938 lr:  0.030558 avg.loss:  1.925916 ETA:   0h 1m2Progress:  39.0% words/sec/thread:   47939 lr:  0.030523 avg.loss:  1.925923 ETA:   0h 1m2Progress:  39.0% words/sec/thread:   47941 lr:  0.030489 avg.loss:  1.925798 ETA:   0h 1m2Progress:  39.1% words/sec/thread:   47942 lr:  0.030454 avg.loss:  1.925774 ETA:   0h 1m2Progress:  39.2% words/sec/thread:   47940 lr:  0.030421 avg.loss:  1.925756 ETA:   0h 1m2Progress:  39.2% words/sec/thread:   47941 lr:  0.030386 avg.loss:  1.925708 ETA:   0h 1m2Progress:  39.3% words/sec/thread:   47944 lr:  0.030351 avg.loss:  1.925654 ETA:   0h 1m2Progress:  39.4% words/sec/thread:   47946 lr:  0.030316 avg.loss:  1.925680 ETA:   0h 1m2Progress:  39.4% words/sec/thread:   47947 lr:  0.030282 avg.loss:  1.925708 ETA:   0h 1m2Progress:  39.5% words/sec/thread:   47948 lr:  0.030247 avg.loss:  1.925509 ETA:   0h 1m2Progress:  39.6% words/sec/thread:   47949 lr:  0.030213 avg.loss:  1.925386 ETA:   0h 1m2Progress:  39.6% words/sec/thread:   47951 lr:  0.030178 avg.loss:  1.924374 ETA:   0h 1m2Progress:  39.7% words/sec/thread:   47952 lr:  0.030143 avg.loss:  1.924291 ETA:   0h 1m2Progress:  39.8% words/sec/thread:   47953 lr:  0.030109 avg.loss:  1.924284 ETA:   0h 1m2Progress:  39.9% words/sec/thread:   47955 lr:  0.030074 avg.loss:  1.924253 ETA:   0h 1m2Progress:  39.9% words/sec/thread:   47954 lr:  0.030040 avg.loss:  1.924225 ETA:   0h 1m2Progress:  40.0% words/sec/thread:   47953 lr:  0.030007 avg.loss:  1.924303 ETA:   0h 1m2Progress:  40.1% words/sec/thread:   47956 lr:  0.029972 avg.loss:  1.924311 ETA:   0h 1m2Progress:  40.1% words/sec/thread:   47956 lr:  0.029937 avg.loss:  1.924181 ETA:   0h 1m2Progress:  40.2% words/sec/thread:   47959 lr:  0.029902 avg.loss:  1.924158 ETA:   0h 1m2Progress:  40.3% words/sec/thread:   47957 lr:  0.029869 avg.loss:  1.924108 ETA:   0h 1m2Progress:  40.3% words/sec/thread:   47957 lr:  0.029835 avg.loss:  1.924018 ETA:   0h 1m2Progress:  40.4% words/sec/thread:   47959 lr:  0.029800 avg.loss:  1.923534 ETA:   0h 1m2Progress:  40.5% words/sec/thread:   47960 lr:  0.029765 avg.loss:  1.923371 ETA:   0h 1m2Progress:  40.5% words/sec/thread:   47962 lr:  0.029730 avg.loss:  1.923298 ETA:   0h 1m2Progress:  40.6% words/sec/thread:   47962 lr:  0.029697 avg.loss:  1.923101 ETA:   0h 1m2Progress:  40.7% words/sec/thread:   47961 lr:  0.029663 avg.loss:  1.923069 ETA:   0h 1m2Progress:  40.7% words/sec/thread:   47960 lr:  0.029629 avg.loss:  1.922901 ETA:   0h 1m2Progress:  40.8% words/sec/thread:   47961 lr:  0.029595 avg.loss:  1.922815 ETA:   0h 1m2Progress:  40.9% words/sec/thread:   47962 lr:  0.029560 avg.loss:  1.922773 ETA:   0h 1m2Progress:  40.9% words/sec/thread:   47964 lr:  0.029525 avg.loss:  1.922657 ETA:   0h 1m2Progress:  41.0% words/sec/thread:   47965 lr:  0.029491 avg.loss:  1.922550 ETA:   0h 1m2Progress:  41.1% words/sec/thread:   47966 lr:  0.029457 avg.loss:  1.922433 ETA:   0h 1m2Progress:  41.2% words/sec/thread:   47967 lr:  0.029422 avg.loss:  1.922366 ETA:   0h 1m2Progress:  41.2% words/sec/thread:   47969 lr:  0.029387 avg.loss:  1.922179 ETA:   0h 1m2Progress:  41.3% words/sec/thread:   47971 lr:  0.029352 avg.loss:  1.922023 ETA:   0h 1m2Progress:  41.4% words/sec/thread:   47971 lr:  0.029318 avg.loss:  1.921916 ETA:   0h 1m2Progress:  41.4% words/sec/thread:   47969 lr:  0.029285 avg.loss:  1.921810 ETA:   0h 1m2Progress:  41.5% words/sec/thread:   47969 lr:  0.029251 avg.loss:  1.921739 ETA:   0h 1m2Progress:  41.6% words/sec/thread:   47969 lr:  0.029217 avg.loss:  1.921579 ETA:   0h 1m2Progress:  41.6% words/sec/thread:   47971 lr:  0.029182 avg.loss:  1.921547 ETA:   0h 1m2Progress:  41.7% words/sec/thread:   47973 lr:  0.029147 avg.loss:  1.921460 ETA:   0h 1m2Progress:  41.8% words/sec/thread:   47975 lr:  0.029112 avg.loss:  1.921387 ETA:   0h 1m2Progress:  41.8% words/sec/thread:   47977 lr:  0.029077 avg.loss:  1.921138 ETA:   0h 1m2Progress:  41.9% words/sec/thread:   47979 lr:  0.029042 avg.loss:  1.921108 ETA:   0h 1m2Progress:  42.0% words/sec/thread:   47980 lr:  0.029008 avg.loss:  1.920922 ETA:   0h 1m2Progress:  42.1% words/sec/thread:   47981 lr:  0.028973 avg.loss:  1.920945 ETA:   0h 1m2Progress:  42.1% words/sec/thread:   47981 lr:  0.028939 avg.loss:  1.920894 ETA:   0h 1m2Progress:  42.2% words/sec/thread:   47980 lr:  0.028905 avg.loss:  1.920773 ETA:   0h 1m2Progress:  42.3% words/sec/thread:   47981 lr:  0.028871 avg.loss:  1.920737 ETA:   0h 1m2Progress:  42.3% words/sec/thread:   47983 lr:  0.028836 avg.loss:  1.920696 ETA:   0h 1m2Progress:  42.4% words/sec/thread:   47984 lr:  0.028801 avg.loss:  1.920520 ETA:   0h 1m2Progress:  42.5% words/sec/thread:   47986 lr:  0.028767 avg.loss:  1.920354 ETA:   0h 1m2Progress:  42.5% words/sec/thread:   47987 lr:  0.028732 avg.loss:  1.920240 ETA:   0h 1m2Progress:  42.6% words/sec/thread:   47989 lr:  0.028697 avg.loss:  1.920121 ETA:   0h 1m2Progress:  42.7% words/sec/thread:   47991 lr:  0.028662 avg.loss:  1.919898 ETA:   0h 1m2Progress:  42.7% words/sec/thread:   47991 lr:  0.028628 avg.loss:  1.919768 ETA:   0h 1m2Progress:  42.8% words/sec/thread:   47991 lr:  0.028594 avg.loss:  1.919749 ETA:   0h 1m2Progress:  42.9% words/sec/thread:   47991 lr:  0.028560 avg.loss:  1.919572 ETA:   0h 1m2Progress:  42.9% words/sec/thread:   47991 lr:  0.028526 avg.loss:  1.919511 ETA:   0h 1m2Progress:  43.0% words/sec/thread:   47993 lr:  0.028491 avg.loss:  1.919398 ETA:   0h 1m2Progress:  43.1% words/sec/thread:   47993 lr:  0.028456 avg.loss:  1.919473 ETA:   0h 1m2Progress:  43.2% words/sec/thread:   47995 lr:  0.028422 avg.loss:  1.919451 ETA:   0h 1m2Progress:  43.2% words/sec/thread:   47996 lr:  0.028387 avg.loss:  1.919427 ETA:   0h 1m2Progress:  43.3% words/sec/thread:   47996 lr:  0.028353 avg.loss:  1.919463 ETA:   0h 1m2Progress:  43.4% words/sec/thread:   47996 lr:  0.028319 avg.loss:  1.919366 ETA:   0h 1m2Progress:  43.4% words/sec/thread:   47997 lr:  0.028284 avg.loss:  1.919339 ETA:   0h 1m2Progress:  43.5% words/sec/thread:   47999 lr:  0.028250 avg.loss:  1.919281 ETA:   0h 1m2Progress:  43.6% words/sec/thread:   48000 lr:  0.028215 avg.loss:  1.919155 ETA:   0h 1m2Progress:  43.6% words/sec/thread:   47999 lr:  0.028181 avg.loss:  1.919044 ETA:   0h 1m2Progress:  43.7% words/sec/thread:   47999 lr:  0.028147 avg.loss:  1.918821 ETA:   0h 1m2Progress:  43.8% words/sec/thread:   48000 lr:  0.028112 avg.loss:  1.918726 ETA:   0h 1m2Progress:  43.8% words/sec/thread:   48001 lr:  0.028078 avg.loss:  1.918622 ETA:   0h 1m2Progress:  43.9% words/sec/thread:   48002 lr:  0.028043 avg.loss:  1.918324 ETA:   0h 1m2Progress:  44.0% words/sec/thread:   48004 lr:  0.028009 avg.loss:  1.918319 ETA:   0h 1m2Progress:  44.1% words/sec/thread:   48004 lr:  0.027974 avg.loss:  1.918432 ETA:   0h 1m2Progress:  44.1% words/sec/thread:   48006 lr:  0.027939 avg.loss:  1.918283 ETA:   0h 1m2Progress:  44.2% words/sec/thread:   48007 lr:  0.027905 avg.loss:  1.918194 ETA:   0h 1m2Progress:  44.3% words/sec/thread:   48008 lr:  0.027870 avg.loss:  1.918122 ETA:   0h 1m2Progress:  44.3% words/sec/thread:   48009 lr:  0.027836 avg.loss:  1.918123 ETA:   0h 1m2Progress:  44.4% words/sec/thread:   48007 lr:  0.027802 avg.loss:  1.918088 ETA:   0h 1m2Progress:  44.5% words/sec/thread:   48008 lr:  0.027768 avg.loss:  1.917972 ETA:   0h 1m2Progress:  44.5% words/sec/thread:   48009 lr:  0.027733 avg.loss:  1.917925 ETA:   0h 1m2Progress:  44.6% words/sec/thread:   48011 lr:  0.027699 avg.loss:  1.917780 ETA:   0h 1m2Progress:  44.7% words/sec/thread:   48011 lr:  0.027664 avg.loss:  1.917684 ETA:   0h 1m2Progress:  44.7% words/sec/thread:   48012 lr:  0.027630 avg.loss:  1.917515 ETA:   0h 1m2Progress:  44.8% words/sec/thread:   48013 lr:  0.027595 avg.loss:  1.917388 ETA:   0h 1m2Progress:  44.9% words/sec/thread:   48015 lr:  0.027560 avg.loss:  1.917411 ETA:   0h 1m2Progress:  44.9% words/sec/thread:   48016 lr:  0.027526 avg.loss:  1.917225 ETA:   0h 1m2Progress:  45.0% words/sec/thread:   48017 lr:  0.027491 avg.loss:  1.917174 ETA:   0h 1m2Progress:  45.1% words/sec/thread:   48017 lr:  0.027457 avg.loss:  1.917051 ETA:   0h 1m2Progress:  45.2% words/sec/thread:   48015 lr:  0.027424 avg.loss:  1.916969 ETA:   0h 1m2Progress:  45.2% words/sec/thread:   48014 lr:  0.027390 avg.loss:  1.916839 ETA:   0h 1m2Progress:  45.3% words/sec/thread:   48016 lr:  0.027355 avg.loss:  1.916874 ETA:   0h 1m2Progress:  45.4% words/sec/thread:   48017 lr:  0.027320 avg.loss:  1.916712 ETA:   0h 1m2Progress:  45.4% words/sec/thread:   48019 lr:  0.027286 avg.loss:  1.916647 ETA:   0h 1m2Progress:  45.5% words/sec/thread:   48019 lr:  0.027252 avg.loss:  1.916420 ETA:   0h 1m2Progress:  45.6% words/sec/thread:   48020 lr:  0.027217 avg.loss:  1.916387 ETA:   0h 1m1Progress:  45.6% words/sec/thread:   48022 lr:  0.027182 avg.loss:  1.916388 ETA:   0h 1m1Progress:  45.7% words/sec/thread:   48023 lr:  0.027147 avg.loss:  1.916104 ETA:   0h 1m1Progress:  45.8% words/sec/thread:   48025 lr:  0.027112 avg.loss:  1.916081 ETA:   0h 1m1Progress:  45.8% words/sec/thread:   48025 lr:  0.027078 avg.loss:  1.915916 ETA:   0h 1m1Progress:  45.9% words/sec/thread:   48023 lr:  0.027045 avg.loss:  1.915660 ETA:   0h 1m1Progress:  46.0% words/sec/thread:   48023 lr:  0.027011 avg.loss:  1.915581 ETA:   0h 1m1Progress:  46.0% words/sec/thread:   48025 lr:  0.026976 avg.loss:  1.915557 ETA:   0h 1m1Progress:  46.1% words/sec/thread:   48028 lr:  0.026940 avg.loss:  1.915296 ETA:   0h 1m1Progress:  46.2% words/sec/thread:   48028 lr:  0.026906 avg.loss:  1.915222 ETA:   0h 1m1Progress:  46.3% words/sec/thread:   48030 lr:  0.026871 avg.loss:  1.915146 ETA:   0h 1m1Progress:  46.3% words/sec/thread:   48031 lr:  0.026836 avg.loss:  1.915101 ETA:   0h 1m1Progress:  46.4% words/sec/thread:   48033 lr:  0.026801 avg.loss:  1.915067 ETA:   0h 1m1Progress:  46.5% words/sec/thread:   48034 lr:  0.026767 avg.loss:  1.914982 ETA:   0h 1m1Progress:  46.5% words/sec/thread:   48035 lr:  0.026732 avg.loss:  1.914920 ETA:   0h 1m1Progress:  46.6% words/sec/thread:   48035 lr:  0.026698 avg.loss:  1.914809 ETA:   0h 1m1Progress:  46.7% words/sec/thread:   48034 lr:  0.026664 avg.loss:  1.914798 ETA:   0h 1m1Progress:  46.7% words/sec/thread:   48035 lr:  0.026630 avg.loss:  1.914494 ETA:   0h 1m1Progress:  46.8% words/sec/thread:   48036 lr:  0.026595 avg.loss:  1.914370 ETA:   0h 1m1Progress:  46.9% words/sec/thread:   48036 lr:  0.026561 avg.loss:  1.914142 ETA:   0h 1m1Progress:  46.9% words/sec/thread:   48037 lr:  0.026526 avg.loss:  1.914052 ETA:   0h 1m1Progress:  47.0% words/sec/thread:   48038 lr:  0.026492 avg.loss:  1.913991 ETA:   0h 1m1Progress:  47.1% words/sec/thread:   48039 lr:  0.026457 avg.loss:  1.913630 ETA:   0h 1m1Progress:  47.2% words/sec/thread:   48039 lr:  0.026423 avg.loss:  1.913637 ETA:   0h 1m1Progress:  47.2% words/sec/thread:   48040 lr:  0.026388 avg.loss:  1.913550 ETA:   0h 1m1Progress:  47.3% words/sec/thread:   48040 lr:  0.026354 avg.loss:  1.913368 ETA:   0h 1m1Progress:  47.4% words/sec/thread:   48039 lr:  0.026321 avg.loss:  1.913212 ETA:   0h 1m1Progress:  47.4% words/sec/thread:   48038 lr:  0.026287 avg.loss:  1.913143 ETA:   0h 1m1Progress:  47.5% words/sec/thread:   48038 lr:  0.026253 avg.loss:  1.912805 ETA:   0h 1m1Progress:  47.6% words/sec/thread:   48039 lr:  0.026218 avg.loss:  1.912701 ETA:   0h 1m1Progress:  47.6% words/sec/thread:   48040 lr:  0.026184 avg.loss:  1.912669 ETA:   0h 1m1Progress:  47.7% words/sec/thread:   48041 lr:  0.026149 avg.loss:  1.912635 ETA:   0h 1m1Progress:  47.8% words/sec/thread:   48041 lr:  0.026115 avg.loss:  1.912619 ETA:   0h 1m1Progress:  47.8% words/sec/thread:   48042 lr:  0.026080 avg.loss:  1.912388 ETA:   0h 1m1Progress:  47.9% words/sec/thread:   48043 lr:  0.026046 avg.loss:  1.912312 ETA:   0h 1m1Progress:  48.0% words/sec/thread:   48045 lr:  0.026011 avg.loss:  1.912267 ETA:   0h 1m1Progress:  48.0% words/sec/thread:   48045 lr:  0.025976 avg.loss:  1.912040 ETA:   0h 1m1Progress:  48.1% words/sec/thread:   48043 lr:  0.025943 avg.loss:  1.911900 ETA:   0h 1m1Progress:  48.2% words/sec/thread:   48043 lr:  0.025909 avg.loss:  1.911803 ETA:   0h 1m1Progress:  48.3% words/sec/thread:   48044 lr:  0.025875 avg.loss:  1.911678 ETA:   0h 1m1Progress:  48.3% words/sec/thread:   48045 lr:  0.025840 avg.loss:  1.911514 ETA:   0h 1m1Progress:  48.4% words/sec/thread:   48045 lr:  0.025806 avg.loss:  1.911522 ETA:   0h 1m1Progress:  48.5% words/sec/thread:   48047 lr:  0.025771 avg.loss:  1.911447 ETA:   0h 1m1Progress:  48.5% words/sec/thread:   48047 lr:  0.025736 avg.loss:  1.911360 ETA:   0h 1m1Progress:  48.6% words/sec/thread:   48049 lr:  0.025702 avg.loss:  1.911264 ETA:   0h 1m1Progress:  48.7% words/sec/thread:   48049 lr:  0.025667 avg.loss:  1.911198 ETA:   0h 1m1Progress:  48.7% words/sec/thread:   48049 lr:  0.025633 avg.loss:  1.911111 ETA:   0h 1m1Progress:  48.8% words/sec/thread:   48049 lr:  0.025599 avg.loss:  1.910995 ETA:   0h 1m1Progress:  48.9% words/sec/thread:   48048 lr:  0.025565 avg.loss:  1.910995 ETA:   0h 1m1Progress:  48.9% words/sec/thread:   48048 lr:  0.025531 avg.loss:  1.910900 ETA:   0h 1m1Progress:  49.0% words/sec/thread:   48049 lr:  0.025497 avg.loss:  1.910723 ETA:   0h 1m1Progress:  49.1% words/sec/thread:   48051 lr:  0.025462 avg.loss:  1.910524 ETA:   0h 1m1Progress:  49.1% words/sec/thread:   48052 lr:  0.025427 avg.loss:  1.910345 ETA:   0h 1m1Progress:  49.2% words/sec/thread:   48053 lr:  0.025392 avg.loss:  1.910275 ETA:   0h 1m1Progress:  49.3% words/sec/thread:   48054 lr:  0.025358 avg.loss:  1.910223 ETA:   0h 1m1Progress:  49.4% words/sec/thread:   48055 lr:  0.025323 avg.loss:  1.910019 ETA:   0h 1m1Progress:  49.4% words/sec/thread:   48055 lr:  0.025289 avg.loss:  1.909902 ETA:   0h 1m1Progress:  49.5% words/sec/thread:   48056 lr:  0.025254 avg.loss:  1.909791 ETA:   0h 1m1Progress:  49.6% words/sec/thread:   48056 lr:  0.025220 avg.loss:  1.909691 ETA:   0h 1m1Progress:  49.6% words/sec/thread:   48055 lr:  0.025186 avg.loss:  1.909522 ETA:   0h 1m1Progress:  49.7% words/sec/thread:   48056 lr:  0.025152 avg.loss:  1.909491 ETA:   0h 1m1Progress:  49.8% words/sec/thread:   48057 lr:  0.025118 avg.loss:  1.909445 ETA:   0h 1m1Progress:  49.8% words/sec/thread:   48058 lr:  0.025083 avg.loss:  1.909310 ETA:   0h 1m1Progress:  49.9% words/sec/thread:   48058 lr:  0.025048 avg.loss:  1.909340 ETA:   0h 1m1Progress:  50.0% words/sec/thread:   48060 lr:  0.025013 avg.loss:  1.909339 ETA:   0h 1m1Progress:  50.0% words/sec/thread:   48060 lr:  0.024979 avg.loss:  1.909330 ETA:   0h 1m1Progress:  50.1% words/sec/thread:   48060 lr:  0.024945 avg.loss:  1.908920 ETA:   0h 1m1Progress:  50.2% words/sec/thread:   48060 lr:  0.024911 avg.loss:  1.908843 ETA:   0h 1m1Progress:  50.2% words/sec/thread:   48062 lr:  0.024876 avg.loss:  1.908846 ETA:   0h 1m1Progress:  50.3% words/sec/thread:   48062 lr:  0.024841 avg.loss:  1.908824 ETA:   0h 1m1Progress:  50.4% words/sec/thread:   48061 lr:  0.024808 avg.loss:  1.908482 ETA:   0h 1m1Progress:  50.5% words/sec/thread:   48061 lr:  0.024774 avg.loss:  1.908491 ETA:   0h 1m1Progress:  50.5% words/sec/thread:   48062 lr:  0.024739 avg.loss:  1.908526 ETA:   0h 1m1Progress:  50.6% words/sec/thread:   48062 lr:  0.024705 avg.loss:  1.908416 ETA:   0h 1m1Progress:  50.7% words/sec/thread:   48063 lr:  0.024670 avg.loss:  1.908262 ETA:   0h 1m1Progress:  50.7% words/sec/thread:   48064 lr:  0.024636 avg.loss:  1.908204 ETA:   0h 1m1Progress:  50.8% words/sec/thread:   48065 lr:  0.024601 avg.loss:  1.908081 ETA:   0h 1m1Progress:  50.9% words/sec/thread:   48067 lr:  0.024566 avg.loss:  1.908020 ETA:   0h 1m1Progress:  50.9% words/sec/thread:   48068 lr:  0.024531 avg.loss:  1.908027 ETA:   0h 1m1Progress:  51.0% words/sec/thread:   48069 lr:  0.024497 avg.loss:  1.907976 ETA:   0h 1m1Progress:  51.1% words/sec/thread:   48068 lr:  0.024463 avg.loss:  1.908001 ETA:   0h 1m1Progress:  51.1% words/sec/thread:   48068 lr:  0.024429 avg.loss:  1.907995 ETA:   0h 1m1Progress:  51.2% words/sec/thread:   48068 lr:  0.024395 avg.loss:  1.907859 ETA:   0h 1m1Progress:  51.3% words/sec/thread:   48069 lr:  0.024360 avg.loss:  1.907699 ETA:   0h 1m1Progress:  51.3% words/sec/thread:   48070 lr:  0.024325 avg.loss:  1.907718 ETA:   0h 1m1Progress:  51.4% words/sec/thread:   48071 lr:  0.024290 avg.loss:  1.907611 ETA:   0h 1m1Progress:  51.5% words/sec/thread:   48072 lr:  0.024256 avg.loss:  1.907565 ETA:   0h 1m1Progress:  51.6% words/sec/thread:   48073 lr:  0.024221 avg.loss:  1.907422 ETA:   0h 1m1Progress:  51.6% words/sec/thread:   48075 lr:  0.024186 avg.loss:  1.907431 ETA:   0h 1m1Progress:  51.7% words/sec/thread:   48076 lr:  0.024152 avg.loss:  1.907380 ETA:   0h 1m1Progress:  51.8% words/sec/thread:   48077 lr:  0.024117 avg.loss:  1.907309 ETA:   0h 1m1Progress:  51.8% words/sec/thread:   48077 lr:  0.024083 avg.loss:  1.907207 ETA:   0h 1m1Progress:  51.9% words/sec/thread:   48076 lr:  0.024049 avg.loss:  1.907183 ETA:   0h 1m1Progress:  52.0% words/sec/thread:   48076 lr:  0.024015 avg.loss:  1.907065 ETA:   0h 1m1Progress:  52.0% words/sec/thread:   48077 lr:  0.023980 avg.loss:  1.907060 ETA:   0h 1m1Progress:  52.1% words/sec/thread:   48078 lr:  0.023946 avg.loss:  1.907093 ETA:   0h 1m1Progress:  52.2% words/sec/thread:   48079 lr:  0.023911 avg.loss:  1.907036 ETA:   0h 1m1Progress:  52.2% words/sec/thread:   48080 lr:  0.023876 avg.loss:  1.906905 ETA:   0h 1m1Progress:  52.3% words/sec/thread:   48081 lr:  0.023841 avg.loss:  1.906857 ETA:   0h 1m Progress:  52.4% words/sec/thread:   48082 lr:  0.023807 avg.loss:  1.906753 ETA:   0h 1m Progress:  52.5% words/sec/thread:   48082 lr:  0.023772 avg.loss:  1.906688 ETA:   0h 1m Progress:  52.5% words/sec/thread:   48082 lr:  0.023738 avg.loss:  1.906586 ETA:   0h 1m Progress:  52.6% words/sec/thread:   48083 lr:  0.023704 avg.loss:  1.906557 ETA:   0h 1m Progress:  52.7% words/sec/thread:   48083 lr:  0.023670 avg.loss:  1.906467 ETA:   0h 1m Progress:  52.7% words/sec/thread:   48082 lr:  0.023636 avg.loss:  1.906426 ETA:   0h 1m Progress:  52.8% words/sec/thread:   48083 lr:  0.023601 avg.loss:  1.906337 ETA:   0h 1m Progress:  52.9% words/sec/thread:   48084 lr:  0.023567 avg.loss:  1.906193 ETA:   0h 1m Progress:  52.9% words/sec/thread:   48085 lr:  0.023532 avg.loss:  1.906140 ETA:   0h 1m Progress:  53.0% words/sec/thread:   48086 lr:  0.023497 avg.loss:  1.906116 ETA:   0h 1m Progress:  53.1% words/sec/thread:   48088 lr:  0.023462 avg.loss:  1.906062 ETA:   0h 1m Progress:  53.1% words/sec/thread:   48089 lr:  0.023427 avg.loss:  1.905960 ETA:   0h 1m Progress:  53.2% words/sec/thread:   48090 lr:  0.023393 avg.loss:  1.905893 ETA:   0h 1m Progress:  53.3% words/sec/thread:   48091 lr:  0.023358 avg.loss:  1.905858 ETA:   0h 1m Progress:  53.4% words/sec/thread:   48091 lr:  0.023324 avg.loss:  1.905825 ETA:   0h 1m Progress:  53.4% words/sec/thread:   48091 lr:  0.023290 avg.loss:  1.905740 ETA:   0h 1m Progress:  53.5% words/sec/thread:   48090 lr:  0.023256 avg.loss:  1.905736 ETA:   0h 1m Progress:  53.6% words/sec/thread:   48090 lr:  0.023222 avg.loss:  1.905644 ETA:   0h 1m Progress:  53.6% words/sec/thread:   48090 lr:  0.023188 avg.loss:  1.905588 ETA:   0h 1m Progress:  53.7% words/sec/thread:   48092 lr:  0.023153 avg.loss:  1.905480 ETA:   0h 1m Progress:  53.8% words/sec/thread:   48093 lr:  0.023118 avg.loss:  1.905469 ETA:   0h 1m Progress:  53.8% words/sec/thread:   48094 lr:  0.023083 avg.loss:  1.905439 ETA:   0h 1m Progress:  53.9% words/sec/thread:   48094 lr:  0.023049 avg.loss:  1.905427 ETA:   0h 1m Progress:  54.0% words/sec/thread:   48094 lr:  0.023015 avg.loss:  1.905498 ETA:   0h 1m Progress:  54.0% words/sec/thread:   48093 lr:  0.022981 avg.loss:  1.905419 ETA:   0h 1m Progress:  54.1% words/sec/thread:   48093 lr:  0.022947 avg.loss:  1.905392 ETA:   0h 1m Progress:  54.2% words/sec/thread:   48093 lr:  0.022913 avg.loss:  1.905390 ETA:   0h 1m Progress:  54.2% words/sec/thread:   48093 lr:  0.022879 avg.loss:  1.905385 ETA:   0h 1m Progress:  54.3% words/sec/thread:   48093 lr:  0.022845 avg.loss:  1.905294 ETA:   0h 1m Progress:  54.4% words/sec/thread:   48089 lr:  0.022813 avg.loss:  1.905308 ETA:   0h 1m Progress:  54.4% words/sec/thread:   48088 lr:  0.022779 avg.loss:  1.905305 ETA:   0h 1m Progress:  54.5% words/sec/thread:   48089 lr:  0.022744 avg.loss:  1.905108 ETA:   0h 1m Progress:  54.6% words/sec/thread:   48091 lr:  0.022709 avg.loss:  1.905112 ETA:   0h 1m Progress:  54.7% words/sec/thread:   48092 lr:  0.022675 avg.loss:  1.905074 ETA:   0h 1m Progress:  54.7% words/sec/thread:   48093 lr:  0.022640 avg.loss:  1.905036 ETA:   0h 1m Progress:  54.8% words/sec/thread:   48094 lr:  0.022605 avg.loss:  1.904952 ETA:   0h 1m Progress:  54.9% words/sec/thread:   48094 lr:  0.022571 avg.loss:  1.904948 ETA:   0h 1m Progress:  54.9% words/sec/thread:   48095 lr:  0.022536 avg.loss:  1.904900 ETA:   0h 1m Progress:  55.0% words/sec/thread:   48095 lr:  0.022502 avg.loss:  1.904794 ETA:   0h 1m Progress:  55.1% words/sec/thread:   48097 lr:  0.022466 avg.loss:  1.904690 ETA:   0h 1m Progress:  55.1% words/sec/thread:   48097 lr:  0.022433 avg.loss:  1.904598 ETA:   0h 1m Progress:  55.2% words/sec/thread:   48098 lr:  0.022398 avg.loss:  1.904590 ETA:   0h 1m Progress:  55.3% words/sec/thread:   48099 lr:  0.022363 avg.loss:  1.904547 ETA:   0h 1m Progress:  55.3% words/sec/thread:   48100 lr:  0.022328 avg.loss:  1.904472 ETA:   0h 1m Progress:  55.4% words/sec/thread:   48101 lr:  0.022294 avg.loss:  1.904438 ETA:   0h 1m Progress:  55.5% words/sec/thread:   48102 lr:  0.022259 avg.loss:  1.904439 ETA:   0h 1m Progress:  55.6% words/sec/thread:   48102 lr:  0.022225 avg.loss:  1.904410 ETA:   0h 1m Progress:  55.6% words/sec/thread:   48102 lr:  0.022191 avg.loss:  1.904294 ETA:   0h 1m Progress:  55.7% words/sec/thread:   48103 lr:  0.022156 avg.loss:  1.904227 ETA:   0h 1m Progress:  55.8% words/sec/thread:   48103 lr:  0.022122 avg.loss:  1.904053 ETA:   0h 1m Progress:  55.8% words/sec/thread:   48104 lr:  0.022087 avg.loss:  1.903995 ETA:   0h 1m Progress:  55.9% words/sec/thread:   48104 lr:  0.022053 avg.loss:  1.904001 ETA:   0h 1m Progress:  56.0% words/sec/thread:   48105 lr:  0.022018 avg.loss:  1.903934 ETA:   0h 1m Progress:  56.0% words/sec/thread:   48105 lr:  0.021984 avg.loss:  1.903798 ETA:   0h 1m Progress:  56.1% words/sec/thread:   48104 lr:  0.021950 avg.loss:  1.903813 ETA:   0h 1m Progress:  56.2% words/sec/thread:   48104 lr:  0.021916 avg.loss:  1.903819 ETA:   0h 1m Progress:  56.2% words/sec/thread:   48105 lr:  0.021881 avg.loss:  1.903836 ETA:   0h 1m Progress:  56.3% words/sec/thread:   48104 lr:  0.021848 avg.loss:  1.903791 ETA:   0h 1m Progress:  56.4% words/sec/thread:   48101 lr:  0.021815 avg.loss:  1.903777 ETA:   0h 1m Progress:  56.4% words/sec/thread:   48101 lr:  0.021781 avg.loss:  1.903784 ETA:   0h 1m Progress:  56.5% words/sec/thread:   48101 lr:  0.021747 avg.loss:  1.903755 ETA:   0h 1m Progress:  56.6% words/sec/thread:   48100 lr:  0.021713 avg.loss:  1.903702 ETA:   0h 1m Progress:  56.6% words/sec/thread:   48101 lr:  0.021679 avg.loss:  1.903558 ETA:   0h 1m Progress:  56.7% words/sec/thread:   48101 lr:  0.021645 avg.loss:  1.903440 ETA:   0h 1m Progress:  56.8% words/sec/thread:   48102 lr:  0.021610 avg.loss:  1.903310 ETA:   0h 1m Progress:  56.8% words/sec/thread:   48102 lr:  0.021576 avg.loss:  1.903298 ETA:   0h 1m Progress:  56.9% words/sec/thread:   48101 lr:  0.021542 avg.loss:  1.903286 ETA:   0h 1m Progress:  57.0% words/sec/thread:   48102 lr:  0.021507 avg.loss:  1.903242 ETA:   0h 1m Progress:  57.1% words/sec/thread:   48101 lr:  0.021474 avg.loss:  1.903137 ETA:   0h 1m Progress:  57.1% words/sec/thread:   48102 lr:  0.021439 avg.loss:  1.903110 ETA:   0h 1m Progress:  57.2% words/sec/thread:   48102 lr:  0.021405 avg.loss:  1.903062 ETA:   0h 1m Progress:  57.3% words/sec/thread:   48102 lr:  0.021371 avg.loss:  1.902948 ETA:   0h 1m Progress:  57.3% words/sec/thread:   48101 lr:  0.021337 avg.loss:  1.902905 ETA:   0h 1m Progress:  57.4% words/sec/thread:   48100 lr:  0.021303 avg.loss:  1.902850 ETA:   0h 1m Progress:  57.5% words/sec/thread:   48101 lr:  0.021269 avg.loss:  1.902773 ETA:   0h 1m Progress:  57.5% words/sec/thread:   48101 lr:  0.021234 avg.loss:  1.902823 ETA:   0h 1m Progress:  57.6% words/sec/thread:   48100 lr:  0.021201 avg.loss:  1.902784 ETA:   0h 1m Progress:  57.7% words/sec/thread:   48100 lr:  0.021167 avg.loss:  1.902769 ETA:   0h 1m Progress:  57.7% words/sec/thread:   48100 lr:  0.021133 avg.loss:  1.902641 ETA:   0h 1m Progress:  57.8% words/sec/thread:   48099 lr:  0.021099 avg.loss:  1.902575 ETA:   0h 1m Progress:  57.9% words/sec/thread:   48100 lr:  0.021065 avg.loss:  1.902556 ETA:   0h 1m Progress:  57.9% words/sec/thread:   48097 lr:  0.021032 avg.loss:  1.902506 ETA:   0h 1m Progress:  58.0% words/sec/thread:   48098 lr:  0.020997 avg.loss:  1.902395 ETA:   0h 1m Progress:  58.1% words/sec/thread:   48098 lr:  0.020963 avg.loss:  1.902375 ETA:   0h 1m Progress:  58.1% words/sec/thread:   48099 lr:  0.020929 avg.loss:  1.902364 ETA:   0h 1m Progress:  58.2% words/sec/thread:   48099 lr:  0.020894 avg.loss:  1.902317 ETA:   0h 1m Progress:  58.3% words/sec/thread:   48100 lr:  0.020860 avg.loss:  1.902323 ETA:   0h 1m Progress:  58.3% words/sec/thread:   48100 lr:  0.020825 avg.loss:  1.902180 ETA:   0h 1m Progress:  58.4% words/sec/thread:   48100 lr:  0.020791 avg.loss:  1.902055 ETA:   0h 1m Progress:  58.5% words/sec/thread:   48100 lr:  0.020757 avg.loss:  1.901967 ETA:   0h 1m Progress:  58.6% words/sec/thread:   48099 lr:  0.020724 avg.loss:  1.901808 ETA:   0h 1m Progress:  58.6% words/sec/thread:   48100 lr:  0.020689 avg.loss:  1.901807 ETA:   0h 1m Progress:  58.7% words/sec/thread:   48100 lr:  0.020655 avg.loss:  1.901745 ETA:   0h 1m Progress:  58.8% words/sec/thread:   48101 lr:  0.020620 avg.loss:  1.901647 ETA:   0h 1m Progress:  58.8% words/sec/thread:   48103 lr:  0.020585 avg.loss:  1.901466 ETA:   0h 1m Progress:  58.9% words/sec/thread:   48103 lr:  0.020551 avg.loss:  1.901308 ETA:   0h 1m Progress:  59.0% words/sec/thread:   48103 lr:  0.020517 avg.loss:  1.901192 ETA:   0h 1m Progress:  59.0% words/sec/thread:   48103 lr:  0.020482 avg.loss:  1.901121 ETA:   0h 1m Progress:  59.1% words/sec/thread:   48103 lr:  0.020448 avg.loss:  1.901073 ETA:   0h 0m5Progress:  59.2% words/sec/thread:   48103 lr:  0.020414 avg.loss:  1.900846 ETA:   0h 0m5Progress:  59.2% words/sec/thread:   48103 lr:  0.020380 avg.loss:  1.900765 ETA:   0h 0m5Progress:  59.3% words/sec/thread:   48103 lr:  0.020346 avg.loss:  1.900723 ETA:   0h 0m5Progress:  59.4% words/sec/thread:   48103 lr:  0.020312 avg.loss:  1.900668 ETA:   0h 0m5Progress:  59.4% words/sec/thread:   48102 lr:  0.020278 avg.loss:  1.900740 ETA:   0h 0m5Progress:  59.5% words/sec/thread:   48104 lr:  0.020243 avg.loss:  1.900714 ETA:   0h 0m5Progress:  59.6% words/sec/thread:   48104 lr:  0.020208 avg.loss:  1.900766 ETA:   0h 0m5Progress:  59.7% words/sec/thread:   48105 lr:  0.020173 avg.loss:  1.900741 ETA:   0h 0m5Progress:  59.7% words/sec/thread:   48106 lr:  0.020139 avg.loss:  1.900695 ETA:   0h 0m5Progress:  59.8% words/sec/thread:   48106 lr:  0.020105 avg.loss:  1.900629 ETA:   0h 0m5Progress:  59.9% words/sec/thread:   48106 lr:  0.020070 avg.loss:  1.900543 ETA:   0h 0m5Progress:  59.9% words/sec/thread:   48106 lr:  0.020036 avg.loss:  1.900491 ETA:   0h 0m5Progress:  60.0% words/sec/thread:   48105 lr:  0.020003 avg.loss:  1.900334 ETA:   0h 0m5Progress:  60.1% words/sec/thread:   48105 lr:  0.019968 avg.loss:  1.900372 ETA:   0h 0m5Progress:  60.1% words/sec/thread:   48105 lr:  0.019934 avg.loss:  1.900306 ETA:   0h 0m5Progress:  60.2% words/sec/thread:   48105 lr:  0.019900 avg.loss:  1.900166 ETA:   0h 0m5Progress:  60.3% words/sec/thread:   48105 lr:  0.019866 avg.loss:  1.900161 ETA:   0h 0m5Progress:  60.3% words/sec/thread:   48105 lr:  0.019832 avg.loss:  1.900139 ETA:   0h 0m5Progress:  60.4% words/sec/thread:   48106 lr:  0.019797 avg.loss:  1.900151 ETA:   0h 0m5Progress:  60.5% words/sec/thread:   48105 lr:  0.019763 avg.loss:  1.900010 ETA:   0h 0m5Progress:  60.5% words/sec/thread:   48106 lr:  0.019729 avg.loss:  1.899947 ETA:   0h 0m5Progress:  60.6% words/sec/thread:   48106 lr:  0.019695 avg.loss:  1.899930 ETA:   0h 0m5Progress:  60.7% words/sec/thread:   48106 lr:  0.019661 avg.loss:  1.899788 ETA:   0h 0m5Progress:  60.7% words/sec/thread:   48106 lr:  0.019626 avg.loss:  1.899675 ETA:   0h 0m5Progress:  60.8% words/sec/thread:   48105 lr:  0.019593 avg.loss:  1.899628 ETA:   0h 0m5Progress:  60.9% words/sec/thread:   48105 lr:  0.019559 avg.loss:  1.899570 ETA:   0h 0m5Progress:  60.9% words/sec/thread:   48104 lr:  0.019525 avg.loss:  1.899526 ETA:   0h 0m5Progress:  61.0% words/sec/thread:   48104 lr:  0.019491 avg.loss:  1.899498 ETA:   0h 0m5Progress:  61.1% words/sec/thread:   48105 lr:  0.019457 avg.loss:  1.899418 ETA:   0h 0m5Progress:  61.2% words/sec/thread:   48105 lr:  0.019422 avg.loss:  1.899369 ETA:   0h 0m5Progress:  61.2% words/sec/thread:   48105 lr:  0.019388 avg.loss:  1.899273 ETA:   0h 0m5Progress:  61.3% words/sec/thread:   48104 lr:  0.019354 avg.loss:  1.899336 ETA:   0h 0m5Progress:  61.4% words/sec/thread:   48106 lr:  0.019319 avg.loss:  1.899233 ETA:   0h 0m5Progress:  61.4% words/sec/thread:   48105 lr:  0.019286 avg.loss:  1.899182 ETA:   0h 0m5Progress:  61.5% words/sec/thread:   48105 lr:  0.019252 avg.loss:  1.899156 ETA:   0h 0m5Progress:  61.6% words/sec/thread:   48104 lr:  0.019218 avg.loss:  1.899129 ETA:   0h 0m5Progress:  61.6% words/sec/thread:   48104 lr:  0.019184 avg.loss:  1.899139 ETA:   0h 0m5Progress:  61.7% words/sec/thread:   48104 lr:  0.019150 avg.loss:  1.899055 ETA:   0h 0m5Progress:  61.8% words/sec/thread:   48105 lr:  0.019115 avg.loss:  1.898990 ETA:   0h 0m5Progress:  61.8% words/sec/thread:   48105 lr:  0.019081 avg.loss:  1.898855 ETA:   0h 0m5Progress:  61.9% words/sec/thread:   48106 lr:  0.019046 avg.loss:  1.898859 ETA:   0h 0m5Progress:  62.0% words/sec/thread:   48107 lr:  0.019011 avg.loss:  1.898762 ETA:   0h 0m5Progress:  62.0% words/sec/thread:   48107 lr:  0.018977 avg.loss:  1.898707 ETA:   0h 0m5Progress:  62.1% words/sec/thread:   48109 lr:  0.018941 avg.loss:  1.898727 ETA:   0h 0m5Progress:  62.2% words/sec/thread:   48109 lr:  0.018907 avg.loss:  1.898703 ETA:   0h 0m5Progress:  62.3% words/sec/thread:   48108 lr:  0.018874 avg.loss:  1.898667 ETA:   0h 0m5Progress:  62.3% words/sec/thread:   48109 lr:  0.018839 avg.loss:  1.898642 ETA:   0h 0m5Progress:  62.4% words/sec/thread:   48109 lr:  0.018805 avg.loss:  1.898567 ETA:   0h 0m5Progress:  62.5% words/sec/thread:   48110 lr:  0.018770 avg.loss:  1.898597 ETA:   0h 0m5Progress:  62.5% words/sec/thread:   48110 lr:  0.018736 avg.loss:  1.898609 ETA:   0h 0m5Progress:  62.6% words/sec/thread:   48111 lr:  0.018701 avg.loss:  1.898586 ETA:   0h 0m5Progress:  62.7% words/sec/thread:   48112 lr:  0.018666 avg.loss:  1.898512 ETA:   0h 0m5Progress:  62.7% words/sec/thread:   48111 lr:  0.018632 avg.loss:  1.898260 ETA:   0h 0m5Progress:  62.8% words/sec/thread:   48112 lr:  0.018598 avg.loss:  1.898158 ETA:   0h 0m5Progress:  62.9% words/sec/thread:   48113 lr:  0.018563 avg.loss:  1.898097 ETA:   0h 0m5Progress:  62.9% words/sec/thread:   48113 lr:  0.018529 avg.loss:  1.898041 ETA:   0h 0m5Progress:  63.0% words/sec/thread:   48112 lr:  0.018495 avg.loss:  1.897969 ETA:   0h 0m5Progress:  63.1% words/sec/thread:   48112 lr:  0.018461 avg.loss:  1.897884 ETA:   0h 0m5Progress:  63.1% words/sec/thread:   48113 lr:  0.018427 avg.loss:  1.897603 ETA:   0h 0m5Progress:  63.2% words/sec/thread:   48113 lr:  0.018392 avg.loss:  1.897558 ETA:   0h 0m5Progress:  63.3% words/sec/thread:   48113 lr:  0.018358 avg.loss:  1.897333 ETA:   0h 0m5Progress:  63.4% words/sec/thread:   48114 lr:  0.018323 avg.loss:  1.897285 ETA:   0h 0m5Progress:  63.4% words/sec/thread:   48114 lr:  0.018289 avg.loss:  1.897215 ETA:   0h 0m5Progress:  63.5% words/sec/thread:   48114 lr:  0.018255 avg.loss:  1.897195 ETA:   0h 0m5Progress:  63.6% words/sec/thread:   48115 lr:  0.018220 avg.loss:  1.897152 ETA:   0h 0m5Progress:  63.6% words/sec/thread:   48115 lr:  0.018186 avg.loss:  1.897098 ETA:   0h 0m5Progress:  63.7% words/sec/thread:   48115 lr:  0.018152 avg.loss:  1.897082 ETA:   0h 0m5Progress:  63.8% words/sec/thread:   48114 lr:  0.018119 avg.loss:  1.896967 ETA:   0h 0m5Progress:  63.8% words/sec/thread:   48114 lr:  0.018084 avg.loss:  1.896929 ETA:   0h 0m5Progress:  63.9% words/sec/thread:   48114 lr:  0.018050 avg.loss:  1.896824 ETA:   0h 0m5Progress:  64.0% words/sec/thread:   48115 lr:  0.018015 avg.loss:  1.896744 ETA:   0h 0m5Progress:  64.0% words/sec/thread:   48115 lr:  0.017981 avg.loss:  1.896700 ETA:   0h 0m5Progress:  64.1% words/sec/thread:   48116 lr:  0.017946 avg.loss:  1.896593 ETA:   0h 0m5Progress:  64.2% words/sec/thread:   48116 lr:  0.017912 avg.loss:  1.896520 ETA:   0h 0m5Progress:  64.2% words/sec/thread:   48117 lr:  0.017877 avg.loss:  1.896287 ETA:   0h 0m5Progress:  64.3% words/sec/thread:   48117 lr:  0.017843 avg.loss:  1.896122 ETA:   0h 0m5Progress:  64.4% words/sec/thread:   48117 lr:  0.017809 avg.loss:  1.896077 ETA:   0h 0m5Progress:  64.5% words/sec/thread:   48117 lr:  0.017775 avg.loss:  1.896022 ETA:   0h 0m5Progress:  64.5% words/sec/thread:   48117 lr:  0.017741 avg.loss:  1.895991 ETA:   0h 0m5Progress:  64.6% words/sec/thread:   48117 lr:  0.017706 avg.loss:  1.895841 ETA:   0h 0m5Progress:  64.7% words/sec/thread:   48117 lr:  0.017672 avg.loss:  1.895761 ETA:   0h 0m5Progress:  64.7% words/sec/thread:   48117 lr:  0.017638 avg.loss:  1.895717 ETA:   0h 0m5Progress:  64.8% words/sec/thread:   48118 lr:  0.017603 avg.loss:  1.895660 ETA:   0h 0m5Progress:  64.9% words/sec/thread:   48118 lr:  0.017569 avg.loss:  1.895612 ETA:   0h 0m5Progress:  64.9% words/sec/thread:   48119 lr:  0.017534 avg.loss:  1.895580 ETA:   0h 0m5Progress:  65.0% words/sec/thread:   48120 lr:  0.017500 avg.loss:  1.895588 ETA:   0h 0m5Progress:  65.1% words/sec/thread:   48120 lr:  0.017465 avg.loss:  1.895538 ETA:   0h 0m5Progress:  65.1% words/sec/thread:   48120 lr:  0.017431 avg.loss:  1.895452 ETA:   0h 0m5Progress:  65.2% words/sec/thread:   48119 lr:  0.017397 avg.loss:  1.895458 ETA:   0h 0m5Progress:  65.3% words/sec/thread:   48118 lr:  0.017364 avg.loss:  1.895344 ETA:   0h 0m5Progress:  65.3% words/sec/thread:   48118 lr:  0.017330 avg.loss:  1.895195 ETA:   0h 0m5Progress:  65.4% words/sec/thread:   48118 lr:  0.017296 avg.loss:  1.895181 ETA:   0h 0m5Progress:  65.5% words/sec/thread:   48118 lr:  0.017261 avg.loss:  1.895109 ETA:   0h 0m5Progress:  65.5% words/sec/thread:   48119 lr:  0.017226 avg.loss:  1.894976 ETA:   0h 0m5Progress:  65.6% words/sec/thread:   48120 lr:  0.017192 avg.loss:  1.894939 ETA:   0h 0m5Progress:  65.7% words/sec/thread:   48119 lr:  0.017158 avg.loss:  1.894901 ETA:   0h 0m5Progress:  65.8% words/sec/thread:   48119 lr:  0.017124 avg.loss:  1.894844 ETA:   0h 0m5Progress:  65.8% words/sec/thread:   48120 lr:  0.017089 avg.loss:  1.894755 ETA:   0h 0m5Progress:  65.9% words/sec/thread:   48120 lr:  0.017055 avg.loss:  1.894630 ETA:   0h 0m5Progress:  66.0% words/sec/thread:   48120 lr:  0.017021 avg.loss:  1.894569 ETA:   0h 0m4Progress:  66.0% words/sec/thread:   48120 lr:  0.016987 avg.loss:  1.894518 ETA:   0h 0m4Progress:  66.1% words/sec/thread:   48119 lr:  0.016953 avg.loss:  1.894429 ETA:   0h 0m4Progress:  66.2% words/sec/thread:   48120 lr:  0.016919 avg.loss:  1.894442 ETA:   0h 0m4Progress:  66.2% words/sec/thread:   48120 lr:  0.016884 avg.loss:  1.894262 ETA:   0h 0m4Progress:  66.3% words/sec/thread:   48121 lr:  0.016849 avg.loss:  1.894251 ETA:   0h 0m4Progress:  66.4% words/sec/thread:   48122 lr:  0.016815 avg.loss:  1.894263 ETA:   0h 0m4Progress:  66.4% words/sec/thread:   48122 lr:  0.016780 avg.loss:  1.894154 ETA:   0h 0m4Progress:  66.5% words/sec/thread:   48123 lr:  0.016746 avg.loss:  1.894061 ETA:   0h 0m4Progress:  66.6% words/sec/thread:   48124 lr:  0.016711 avg.loss:  1.894010 ETA:   0h 0m4Progress:  66.6% words/sec/thread:   48124 lr:  0.016677 avg.loss:  1.893943 ETA:   0h 0m4Progress:  66.7% words/sec/thread:   48123 lr:  0.016643 avg.loss:  1.893897 ETA:   0h 0m4Progress:  66.8% words/sec/thread:   48122 lr:  0.016609 avg.loss:  1.893922 ETA:   0h 0m4Progress:  66.8% words/sec/thread:   48122 lr:  0.016575 avg.loss:  1.893891 ETA:   0h 0m4Progress:  66.9% words/sec/thread:   48122 lr:  0.016541 avg.loss:  1.893838 ETA:   0h 0m4Progress:  67.0% words/sec/thread:   48123 lr:  0.016507 avg.loss:  1.893832 ETA:   0h 0m4Progress:  67.1% words/sec/thread:   48122 lr:  0.016473 avg.loss:  1.893775 ETA:   0h 0m4Progress:  67.1% words/sec/thread:   48122 lr:  0.016439 avg.loss:  1.893716 ETA:   0h 0m4Progress:  67.2% words/sec/thread:   48122 lr:  0.016404 avg.loss:  1.893674 ETA:   0h 0m4Progress:  67.3% words/sec/thread:   48123 lr:  0.016370 avg.loss:  1.893585 ETA:   0h 0m4Progress:  67.3% words/sec/thread:   48123 lr:  0.016335 avg.loss:  1.893499 ETA:   0h 0m4Progress:  67.4% words/sec/thread:   48123 lr:  0.016301 avg.loss:  1.893094 ETA:   0h 0m4Progress:  67.5% words/sec/thread:   48122 lr:  0.016267 avg.loss:  1.893114 ETA:   0h 0m4Progress:  67.5% words/sec/thread:   48122 lr:  0.016234 avg.loss:  1.892989 ETA:   0h 0m4Progress:  67.6% words/sec/thread:   48121 lr:  0.016200 avg.loss:  1.892908 ETA:   0h 0m4Progress:  67.7% words/sec/thread:   48122 lr:  0.016165 avg.loss:  1.892939 ETA:   0h 0m4Progress:  67.7% words/sec/thread:   48122 lr:  0.016131 avg.loss:  1.892826 ETA:   0h 0m4Progress:  67.8% words/sec/thread:   48123 lr:  0.016096 avg.loss:  1.892723 ETA:   0h 0m4Progress:  67.9% words/sec/thread:   48124 lr:  0.016061 avg.loss:  1.892694 ETA:   0h 0m4Progress:  67.9% words/sec/thread:   48124 lr:  0.016027 avg.loss:  1.892606 ETA:   0h 0m4Progress:  68.0% words/sec/thread:   48124 lr:  0.015993 avg.loss:  1.892569 ETA:   0h 0m4Progress:  68.1% words/sec/thread:   48125 lr:  0.015958 avg.loss:  1.892436 ETA:   0h 0m4Progress:  68.2% words/sec/thread:   48124 lr:  0.015924 avg.loss:  1.892446 ETA:   0h 0m4Progress:  68.2% words/sec/thread:   48124 lr:  0.015890 avg.loss:  1.892413 ETA:   0h 0m4Progress:  68.3% words/sec/thread:   48123 lr:  0.015857 avg.loss:  1.892390 ETA:   0h 0m4Progress:  68.4% words/sec/thread:   48123 lr:  0.015823 avg.loss:  1.892343 ETA:   0h 0m4Progress:  68.4% words/sec/thread:   48124 lr:  0.015788 avg.loss:  1.892333 ETA:   0h 0m4Progress:  68.5% words/sec/thread:   48125 lr:  0.015753 avg.loss:  1.892336 ETA:   0h 0m4Progress:  68.6% words/sec/thread:   48125 lr:  0.015719 avg.loss:  1.892222 ETA:   0h 0m4Progress:  68.6% words/sec/thread:   48125 lr:  0.015684 avg.loss:  1.892175 ETA:   0h 0m4Progress:  68.7% words/sec/thread:   48125 lr:  0.015650 avg.loss:  1.892110 ETA:   0h 0m4Progress:  68.8% words/sec/thread:   48125 lr:  0.015616 avg.loss:  1.892070 ETA:   0h 0m4Progress:  68.8% words/sec/thread:   48126 lr:  0.015582 avg.loss:  1.891938 ETA:   0h 0m4Progress:  68.9% words/sec/thread:   48125 lr:  0.015548 avg.loss:  1.891855 ETA:   0h 0m4Progress:  69.0% words/sec/thread:   48125 lr:  0.015514 avg.loss:  1.891808 ETA:   0h 0m4Progress:  69.0% words/sec/thread:   48125 lr:  0.015480 avg.loss:  1.891724 ETA:   0h 0m4Progress:  69.1% words/sec/thread:   48125 lr:  0.015446 avg.loss:  1.891753 ETA:   0h 0m4Progress:  69.2% words/sec/thread:   48126 lr:  0.015411 avg.loss:  1.891708 ETA:   0h 0m4Progress:  69.2% words/sec/thread:   48125 lr:  0.015377 avg.loss:  1.891727 ETA:   0h 0m4Progress:  69.3% words/sec/thread:   48126 lr:  0.015342 avg.loss:  1.891642 ETA:   0h 0m4Progress:  69.4% words/sec/thread:   48128 lr:  0.015307 avg.loss:  1.891668 ETA:   0h 0m4Progress:  69.5% words/sec/thread:   48129 lr:  0.015272 avg.loss:  1.891636 ETA:   0h 0m4Progress:  69.5% words/sec/thread:   48130 lr:  0.015237 avg.loss:  1.891577 ETA:   0h 0m4Progress:  69.6% words/sec/thread:   48129 lr:  0.015203 avg.loss:  1.891514 ETA:   0h 0m4Progress:  69.7% words/sec/thread:   48129 lr:  0.015169 avg.loss:  1.891456 ETA:   0h 0m4Progress:  69.7% words/sec/thread:   48129 lr:  0.015135 avg.loss:  1.891469 ETA:   0h 0m4Progress:  69.8% words/sec/thread:   48129 lr:  0.015101 avg.loss:  1.891447 ETA:   0h 0m4Progress:  69.9% words/sec/thread:   48130 lr:  0.015066 avg.loss:  1.891356 ETA:   0h 0m4Progress:  69.9% words/sec/thread:   48130 lr:  0.015032 avg.loss:  1.891160 ETA:   0h 0m4Progress:  70.0% words/sec/thread:   48131 lr:  0.014997 avg.loss:  1.891102 ETA:   0h 0m4Progress:  70.1% words/sec/thread:   48131 lr:  0.014963 avg.loss:  1.891048 ETA:   0h 0m4Progress:  70.1% words/sec/thread:   48131 lr:  0.014929 avg.loss:  1.891028 ETA:   0h 0m4Progress:  70.2% words/sec/thread:   48132 lr:  0.014894 avg.loss:  1.890960 ETA:   0h 0m4Progress:  70.3% words/sec/thread:   48132 lr:  0.014860 avg.loss:  1.890868 ETA:   0h 0m4Progress:  70.3% words/sec/thread:   48132 lr:  0.014825 avg.loss:  1.890852 ETA:   0h 0m4Progress:  70.4% words/sec/thread:   48130 lr:  0.014792 avg.loss:  1.890822 ETA:   0h 0m4Progress:  70.5% words/sec/thread:   48130 lr:  0.014759 avg.loss:  1.890816 ETA:   0h 0m4Progress:  70.6% words/sec/thread:   48130 lr:  0.014725 avg.loss:  1.890744 ETA:   0h 0m4Progress:  70.6% words/sec/thread:   48130 lr:  0.014690 avg.loss:  1.890741 ETA:   0h 0m4Progress:  70.7% words/sec/thread:   48131 lr:  0.014656 avg.loss:  1.890755 ETA:   0h 0m4Progress:  70.8% words/sec/thread:   48131 lr:  0.014621 avg.loss:  1.890694 ETA:   0h 0m4Progress:  70.8% words/sec/thread:   48132 lr:  0.014586 avg.loss:  1.890659 ETA:   0h 0m4Progress:  70.9% words/sec/thread:   48133 lr:  0.014552 avg.loss:  1.890662 ETA:   0h 0m4Progress:  71.0% words/sec/thread:   48133 lr:  0.014517 avg.loss:  1.890683 ETA:   0h 0m4Progress:  71.0% words/sec/thread:   48133 lr:  0.014483 avg.loss:  1.890659 ETA:   0h 0m4Progress:  71.1% words/sec/thread:   48134 lr:  0.014448 avg.loss:  1.890654 ETA:   0h 0m4Progress:  71.2% words/sec/thread:   48134 lr:  0.014414 avg.loss:  1.890603 ETA:   0h 0m4Progress:  71.2% words/sec/thread:   48133 lr:  0.014381 avg.loss:  1.890565 ETA:   0h 0m4Progress:  71.3% words/sec/thread:   48133 lr:  0.014346 avg.loss:  1.890512 ETA:   0h 0m4Progress:  71.4% words/sec/thread:   48133 lr:  0.014312 avg.loss:  1.890417 ETA:   0h 0m4Progress:  71.4% words/sec/thread:   48134 lr:  0.014277 avg.loss:  1.890399 ETA:   0h 0m4Progress:  71.5% words/sec/thread:   48134 lr:  0.014243 avg.loss:  1.890411 ETA:   0h 0m4Progress:  71.6% words/sec/thread:   48134 lr:  0.014208 avg.loss:  1.890374 ETA:   0h 0m4Progress:  71.7% words/sec/thread:   48134 lr:  0.014174 avg.loss:  1.890423 ETA:   0h 0m4Progress:  71.7% words/sec/thread:   48135 lr:  0.014140 avg.loss:  1.890431 ETA:   0h 0m4Progress:  71.8% words/sec/thread:   48135 lr:  0.014106 avg.loss:  1.890336 ETA:   0h 0m4Progress:  71.9% words/sec/thread:   48135 lr:  0.014071 avg.loss:  1.890298 ETA:   0h 0m4Progress:  71.9% words/sec/thread:   48135 lr:  0.014037 avg.loss:  1.890191 ETA:   0h 0m4Progress:  72.0% words/sec/thread:   48134 lr:  0.014004 avg.loss:  1.890147 ETA:   0h 0m4Progress:  72.1% words/sec/thread:   48135 lr:  0.013969 avg.loss:  1.890149 ETA:   0h 0m4Progress:  72.1% words/sec/thread:   48135 lr:  0.013935 avg.loss:  1.890086 ETA:   0h 0m4Progress:  72.2% words/sec/thread:   48135 lr:  0.013900 avg.loss:  1.890038 ETA:   0h 0m4Progress:  72.3% words/sec/thread:   48136 lr:  0.013866 avg.loss:  1.889996 ETA:   0h 0m4Progress:  72.3% words/sec/thread:   48136 lr:  0.013831 avg.loss:  1.889961 ETA:   0h 0m4Progress:  72.4% words/sec/thread:   48136 lr:  0.013797 avg.loss:  1.889933 ETA:   0h 0m4Progress:  72.5% words/sec/thread:   48137 lr:  0.013762 avg.loss:  1.889929 ETA:   0h 0m4Progress:  72.5% words/sec/thread:   48136 lr:  0.013729 avg.loss:  1.889873 ETA:   0h 0m4Progress:  72.6% words/sec/thread:   48133 lr:  0.013697 avg.loss:  1.889833 ETA:   0h 0m4Progress:  72.7% words/sec/thread:   48132 lr:  0.013664 avg.loss:  1.889807 ETA:   0h 0m4Progress:  72.7% words/sec/thread:   48131 lr:  0.013630 avg.loss:  1.889764 ETA:   0h 0m3Progress:  72.8% words/sec/thread:   48131 lr:  0.013596 avg.loss:  1.889641 ETA:   0h 0m3Progress:  72.9% words/sec/thread:   48131 lr:  0.013562 avg.loss:  1.889485 ETA:   0h 0m3Progress:  72.9% words/sec/thread:   48131 lr:  0.013528 avg.loss:  1.889390 ETA:   0h 0m3Progress:  73.0% words/sec/thread:   48131 lr:  0.013493 avg.loss:  1.889350 ETA:   0h 0m3Progress:  73.1% words/sec/thread:   48131 lr:  0.013459 avg.loss:  1.889305 ETA:   0h 0m3Progress:  73.2% words/sec/thread:   48132 lr:  0.013424 avg.loss:  1.889280 ETA:   0h 0m3Progress:  73.2% words/sec/thread:   48131 lr:  0.013390 avg.loss:  1.889275 ETA:   0h 0m3Progress:  73.3% words/sec/thread:   48132 lr:  0.013356 avg.loss:  1.889181 ETA:   0h 0m3Progress:  73.4% words/sec/thread:   48131 lr:  0.013322 avg.loss:  1.889139 ETA:   0h 0m3Progress:  73.4% words/sec/thread:   48129 lr:  0.013290 avg.loss:  1.889107 ETA:   0h 0m3Progress:  73.5% words/sec/thread:   48129 lr:  0.013256 avg.loss:  1.889066 ETA:   0h 0m3Progress:  73.6% words/sec/thread:   48129 lr:  0.013222 avg.loss:  1.889077 ETA:   0h 0m3Progress:  73.6% words/sec/thread:   48129 lr:  0.013187 avg.loss:  1.889045 ETA:   0h 0m3Progress:  73.7% words/sec/thread:   48130 lr:  0.013153 avg.loss:  1.888915 ETA:   0h 0m3Progress:  73.8% words/sec/thread:   48130 lr:  0.013118 avg.loss:  1.888889 ETA:   0h 0m3Progress:  73.8% words/sec/thread:   48130 lr:  0.013084 avg.loss:  1.888777 ETA:   0h 0m3Progress:  73.9% words/sec/thread:   48131 lr:  0.013049 avg.loss:  1.888738 ETA:   0h 0m3Progress:  74.0% words/sec/thread:   48131 lr:  0.013015 avg.loss:  1.888648 ETA:   0h 0m3Progress:  74.0% words/sec/thread:   48132 lr:  0.012980 avg.loss:  1.888574 ETA:   0h 0m3Progress:  74.1% words/sec/thread:   48131 lr:  0.012947 avg.loss:  1.888550 ETA:   0h 0m3Progress:  74.2% words/sec/thread:   48128 lr:  0.012915 avg.loss:  1.888478 ETA:   0h 0m3Progress:  74.2% words/sec/thread:   48129 lr:  0.012880 avg.loss:  1.888425 ETA:   0h 0m3Progress:  74.3% words/sec/thread:   48130 lr:  0.012845 avg.loss:  1.888407 ETA:   0h 0m3Progress:  74.4% words/sec/thread:   48130 lr:  0.012811 avg.loss:  1.888344 ETA:   0h 0m3Progress:  74.4% words/sec/thread:   48131 lr:  0.012776 avg.loss:  1.888321 ETA:   0h 0m3Progress:  74.5% words/sec/thread:   48131 lr:  0.012741 avg.loss:  1.888324 ETA:   0h 0m3Progress:  74.6% words/sec/thread:   48131 lr:  0.012707 avg.loss:  1.888298 ETA:   0h 0m3Progress:  74.7% words/sec/thread:   48133 lr:  0.012672 avg.loss:  1.888242 ETA:   0h 0m3Progress:  74.7% words/sec/thread:   48133 lr:  0.012637 avg.loss:  1.887981 ETA:   0h 0m3Progress:  74.8% words/sec/thread:   48134 lr:  0.012603 avg.loss:  1.887991 ETA:   0h 0m3Progress:  74.9% words/sec/thread:   48133 lr:  0.012569 avg.loss:  1.887927 ETA:   0h 0m3Progress:  74.9% words/sec/thread:   48132 lr:  0.012536 avg.loss:  1.887934 ETA:   0h 0m3Progress:  75.0% words/sec/thread:   48131 lr:  0.012502 avg.loss:  1.887929 ETA:   0h 0m3Progress:  75.1% words/sec/thread:   48131 lr:  0.012468 avg.loss:  1.887854 ETA:   0h 0m3Progress:  75.1% words/sec/thread:   48132 lr:  0.012433 avg.loss:  1.887922 ETA:   0h 0m3Progress:  75.2% words/sec/thread:   48133 lr:  0.012398 avg.loss:  1.887929 ETA:   0h 0m3Progress:  75.3% words/sec/thread:   48133 lr:  0.012364 avg.loss:  1.887848 ETA:   0h 0m3Progress:  75.3% words/sec/thread:   48133 lr:  0.012330 avg.loss:  1.887773 ETA:   0h 0m3Progress:  75.4% words/sec/thread:   48134 lr:  0.012295 avg.loss:  1.887753 ETA:   0h 0m3Progress:  75.5% words/sec/thread:   48134 lr:  0.012261 avg.loss:  1.887635 ETA:   0h 0m3Progress:  75.5% words/sec/thread:   48135 lr:  0.012226 avg.loss:  1.887655 ETA:   0h 0m3Progress:  75.6% words/sec/thread:   48134 lr:  0.012192 avg.loss:  1.887647 ETA:   0h 0m3Progress:  75.7% words/sec/thread:   48134 lr:  0.012158 avg.loss:  1.887615 ETA:   0h 0m3Progress:  75.8% words/sec/thread:   48133 lr:  0.012125 avg.loss:  1.887571 ETA:   0h 0m3Progress:  75.8% words/sec/thread:   48134 lr:  0.012090 avg.loss:  1.887540 ETA:   0h 0m3Progress:  75.9% words/sec/thread:   48135 lr:  0.012055 avg.loss:  1.887553 ETA:   0h 0m3Progress:  76.0% words/sec/thread:   48135 lr:  0.012021 avg.loss:  1.887448 ETA:   0h 0m3Progress:  76.0% words/sec/thread:   48135 lr:  0.011987 avg.loss:  1.887337 ETA:   0h 0m3Progress:  76.1% words/sec/thread:   48135 lr:  0.011952 avg.loss:  1.887340 ETA:   0h 0m3Progress:  76.2% words/sec/thread:   48136 lr:  0.011918 avg.loss:  1.887329 ETA:   0h 0m3Progress:  76.2% words/sec/thread:   48136 lr:  0.011883 avg.loss:  1.887284 ETA:   0h 0m3Progress:  76.3% words/sec/thread:   48136 lr:  0.011849 avg.loss:  1.887194 ETA:   0h 0m3Progress:  76.4% words/sec/thread:   48136 lr:  0.011815 avg.loss:  1.887132 ETA:   0h 0m3Progress:  76.4% words/sec/thread:   48135 lr:  0.011782 avg.loss:  1.887124 ETA:   0h 0m3Progress:  76.5% words/sec/thread:   48135 lr:  0.011747 avg.loss:  1.887069 ETA:   0h 0m3Progress:  76.6% words/sec/thread:   48135 lr:  0.011713 avg.loss:  1.887026 ETA:   0h 0m3Progress:  76.6% words/sec/thread:   48136 lr:  0.011679 avg.loss:  1.886957 ETA:   0h 0m3Progress:  76.7% words/sec/thread:   48136 lr:  0.011644 avg.loss:  1.886953 ETA:   0h 0m3Progress:  76.8% words/sec/thread:   48135 lr:  0.011610 avg.loss:  1.886940 ETA:   0h 0m3Progress:  76.8% words/sec/thread:   48135 lr:  0.011576 avg.loss:  1.886870 ETA:   0h 0m3Progress:  76.9% words/sec/thread:   48135 lr:  0.011542 avg.loss:  1.886788 ETA:   0h 0m3Progress:  77.0% words/sec/thread:   48135 lr:  0.011508 avg.loss:  1.886690 ETA:   0h 0m3Progress:  77.1% words/sec/thread:   48136 lr:  0.011473 avg.loss:  1.886669 ETA:   0h 0m3Progress:  77.1% words/sec/thread:   48135 lr:  0.011440 avg.loss:  1.886620 ETA:   0h 0m3Progress:  77.2% words/sec/thread:   48134 lr:  0.011406 avg.loss:  1.886554 ETA:   0h 0m3Progress:  77.3% words/sec/thread:   48135 lr:  0.011372 avg.loss:  1.886521 ETA:   0h 0m3Progress:  77.3% words/sec/thread:   48135 lr:  0.011337 avg.loss:  1.886484 ETA:   0h 0m3Progress:  77.4% words/sec/thread:   48135 lr:  0.011303 avg.loss:  1.886385 ETA:   0h 0m3Progress:  77.5% words/sec/thread:   48136 lr:  0.011268 avg.loss:  1.886387 ETA:   0h 0m3Progress:  77.5% words/sec/thread:   48135 lr:  0.011234 avg.loss:  1.886380 ETA:   0h 0m3Progress:  77.6% words/sec/thread:   48136 lr:  0.011200 avg.loss:  1.886302 ETA:   0h 0m3Progress:  77.7% words/sec/thread:   48137 lr:  0.011165 avg.loss:  1.886265 ETA:   0h 0m3Progress:  77.7% words/sec/thread:   48137 lr:  0.011130 avg.loss:  1.886233 ETA:   0h 0m3Progress:  77.8% words/sec/thread:   48137 lr:  0.011096 avg.loss:  1.886214 ETA:   0h 0m3Progress:  77.9% words/sec/thread:   48137 lr:  0.011062 avg.loss:  1.886142 ETA:   0h 0m3Progress:  77.9% words/sec/thread:   48136 lr:  0.011029 avg.loss:  1.886103 ETA:   0h 0m3Progress:  78.0% words/sec/thread:   48135 lr:  0.010995 avg.loss:  1.885732 ETA:   0h 0m3Progress:  78.1% words/sec/thread:   48135 lr:  0.010961 avg.loss:  1.885484 ETA:   0h 0m3Progress:  78.1% words/sec/thread:   48136 lr:  0.010926 avg.loss:  1.885477 ETA:   0h 0m3Progress:  78.2% words/sec/thread:   48136 lr:  0.010892 avg.loss:  1.885443 ETA:   0h 0m3Progress:  78.3% words/sec/thread:   48136 lr:  0.010858 avg.loss:  1.885409 ETA:   0h 0m3Progress:  78.4% words/sec/thread:   48135 lr:  0.010824 avg.loss:  1.885458 ETA:   0h 0m3Progress:  78.4% words/sec/thread:   48135 lr:  0.010791 avg.loss:  1.885435 ETA:   0h 0m3Progress:  78.5% words/sec/thread:   48136 lr:  0.010756 avg.loss:  1.885407 ETA:   0h 0m3Progress:  78.6% words/sec/thread:   48136 lr:  0.010721 avg.loss:  1.885428 ETA:   0h 0m3Progress:  78.6% words/sec/thread:   48135 lr:  0.010688 avg.loss:  1.885452 ETA:   0h 0m3Progress:  78.7% words/sec/thread:   48134 lr:  0.010654 avg.loss:  1.885398 ETA:   0h 0m3Progress:  78.8% words/sec/thread:   48135 lr:  0.010620 avg.loss:  1.885387 ETA:   0h 0m3Progress:  78.8% words/sec/thread:   48135 lr:  0.010586 avg.loss:  1.885338 ETA:   0h 0m3Progress:  78.9% words/sec/thread:   48135 lr:  0.010551 avg.loss:  1.885180 ETA:   0h 0m3Progress:  79.0% words/sec/thread:   48136 lr:  0.010517 avg.loss:  1.885131 ETA:   0h 0m3Progress:  79.0% words/sec/thread:   48136 lr:  0.010482 avg.loss:  1.885119 ETA:   0h 0m3Progress:  79.1% words/sec/thread:   48136 lr:  0.010448 avg.loss:  1.885105 ETA:   0h 0m3Progress:  79.2% words/sec/thread:   48136 lr:  0.010413 avg.loss:  1.885062 ETA:   0h 0m3Progress:  79.2% words/sec/thread:   48136 lr:  0.010379 avg.loss:  1.885011 ETA:   0h 0m3Progress:  79.3% words/sec/thread:   48136 lr:  0.010345 avg.loss:  1.884904 ETA:   0h 0m3Progress:  79.4% words/sec/thread:   48135 lr:  0.010312 avg.loss:  1.884805 ETA:   0h 0m3Progress:  79.4% words/sec/thread:   48135 lr:  0.010278 avg.loss:  1.884787 ETA:   0h 0m3Progress:  79.5% words/sec/thread:   48135 lr:  0.010243 avg.loss:  1.884727 ETA:   0h 0m3Progress:  79.6% words/sec/thread:   48136 lr:  0.010208 avg.loss:  1.884654 ETA:   0h 0m2Progress:  79.7% words/sec/thread:   48136 lr:  0.010174 avg.loss:  1.884626 ETA:   0h 0m2Progress:  79.7% words/sec/thread:   48137 lr:  0.010140 avg.loss:  1.884540 ETA:   0h 0m2Progress:  79.8% words/sec/thread:   48137 lr:  0.010106 avg.loss:  1.884536 ETA:   0h 0m2Progress:  79.9% words/sec/thread:   48138 lr:  0.010071 avg.loss:  1.884439 ETA:   0h 0m2Progress:  79.9% words/sec/thread:   48138 lr:  0.010036 avg.loss:  1.884351 ETA:   0h 0m2Progress:  80.0% words/sec/thread:   48138 lr:  0.010002 avg.loss:  1.884334 ETA:   0h 0m2Progress:  80.1% words/sec/thread:   48138 lr:  0.009968 avg.loss:  1.884322 ETA:   0h 0m2Progress:  80.1% words/sec/thread:   48138 lr:  0.009934 avg.loss:  1.884267 ETA:   0h 0m2Progress:  80.2% words/sec/thread:   48138 lr:  0.009900 avg.loss:  1.884219 ETA:   0h 0m2Progress:  80.3% words/sec/thread:   48138 lr:  0.009866 avg.loss:  1.884211 ETA:   0h 0m2Progress:  80.3% words/sec/thread:   48138 lr:  0.009831 avg.loss:  1.883911 ETA:   0h 0m2Progress:  80.4% words/sec/thread:   48139 lr:  0.009796 avg.loss:  1.883945 ETA:   0h 0m2Progress:  80.5% words/sec/thread:   48139 lr:  0.009762 avg.loss:  1.883904 ETA:   0h 0m2Progress:  80.5% words/sec/thread:   48141 lr:  0.009726 avg.loss:  1.883781 ETA:   0h 0m2Progress:  80.6% words/sec/thread:   48141 lr:  0.009692 avg.loss:  1.883694 ETA:   0h 0m2Progress:  80.7% words/sec/thread:   48141 lr:  0.009658 avg.loss:  1.883665 ETA:   0h 0m2Progress:  80.8% words/sec/thread:   48141 lr:  0.009624 avg.loss:  1.883612 ETA:   0h 0m2Progress:  80.8% words/sec/thread:   48141 lr:  0.009589 avg.loss:  1.883520 ETA:   0h 0m2Progress:  80.9% words/sec/thread:   48140 lr:  0.009556 avg.loss:  1.883478 ETA:   0h 0m2Progress:  81.0% words/sec/thread:   48140 lr:  0.009522 avg.loss:  1.883442 ETA:   0h 0m2Progress:  81.0% words/sec/thread:   48139 lr:  0.009488 avg.loss:  1.883346 ETA:   0h 0m2Progress:  81.1% words/sec/thread:   48139 lr:  0.009454 avg.loss:  1.883228 ETA:   0h 0m2Progress:  81.2% words/sec/thread:   48140 lr:  0.009419 avg.loss:  1.883127 ETA:   0h 0m2Progress:  81.2% words/sec/thread:   48140 lr:  0.009385 avg.loss:  1.883079 ETA:   0h 0m2Progress:  81.3% words/sec/thread:   48140 lr:  0.009351 avg.loss:  1.883078 ETA:   0h 0m2Progress:  81.4% words/sec/thread:   48140 lr:  0.009317 avg.loss:  1.883073 ETA:   0h 0m2Progress:  81.4% words/sec/thread:   48140 lr:  0.009283 avg.loss:  1.882979 ETA:   0h 0m2Progress:  81.5% words/sec/thread:   48137 lr:  0.009251 avg.loss:  1.882947 ETA:   0h 0m2Progress:  81.6% words/sec/thread:   48135 lr:  0.009218 avg.loss:  1.882872 ETA:   0h 0m2Progress:  81.6% words/sec/thread:   48135 lr:  0.009184 avg.loss:  1.882746 ETA:   0h 0m2Progress:  81.7% words/sec/thread:   48135 lr:  0.009150 avg.loss:  1.882692 ETA:   0h 0m2Progress:  81.8% words/sec/thread:   48135 lr:  0.009116 avg.loss:  1.882646 ETA:   0h 0m2Progress:  81.8% words/sec/thread:   48136 lr:  0.009081 avg.loss:  1.882612 ETA:   0h 0m2Progress:  81.9% words/sec/thread:   48137 lr:  0.009046 avg.loss:  1.882569 ETA:   0h 0m2Progress:  82.0% words/sec/thread:   48137 lr:  0.009012 avg.loss:  1.882558 ETA:   0h 0m2Progress:  82.0% words/sec/thread:   48136 lr:  0.008978 avg.loss:  1.882514 ETA:   0h 0m2Progress:  82.1% words/sec/thread:   48137 lr:  0.008944 avg.loss:  1.882472 ETA:   0h 0m2Progress:  82.2% words/sec/thread:   48137 lr:  0.008910 avg.loss:  1.882431 ETA:   0h 0m2Progress:  82.2% words/sec/thread:   48137 lr:  0.008875 avg.loss:  1.882443 ETA:   0h 0m2Progress:  82.3% words/sec/thread:   48137 lr:  0.008841 avg.loss:  1.882431 ETA:   0h 0m2Progress:  82.4% words/sec/thread:   48136 lr:  0.008807 avg.loss:  1.882422 ETA:   0h 0m2Progress:  82.5% words/sec/thread:   48136 lr:  0.008773 avg.loss:  1.882374 ETA:   0h 0m2Progress:  82.5% words/sec/thread:   48137 lr:  0.008739 avg.loss:  1.882279 ETA:   0h 0m2Progress:  82.6% words/sec/thread:   48137 lr:  0.008704 avg.loss:  1.882200 ETA:   0h 0m2Progress:  82.7% words/sec/thread:   48137 lr:  0.008670 avg.loss:  1.882212 ETA:   0h 0m2Progress:  82.7% words/sec/thread:   48138 lr:  0.008635 avg.loss:  1.882213 ETA:   0h 0m2Progress:  82.8% words/sec/thread:   48138 lr:  0.008601 avg.loss:  1.882125 ETA:   0h 0m2Progress:  82.9% words/sec/thread:   48138 lr:  0.008567 avg.loss:  1.882055 ETA:   0h 0m2Progress:  82.9% words/sec/thread:   48139 lr:  0.008532 avg.loss:  1.882031 ETA:   0h 0m2Progress:  83.0% words/sec/thread:   48139 lr:  0.008498 avg.loss:  1.881992 ETA:   0h 0m2Progress:  83.1% words/sec/thread:   48139 lr:  0.008463 avg.loss:  1.881960 ETA:   0h 0m2Progress:  83.1% words/sec/thread:   48139 lr:  0.008429 avg.loss:  1.881925 ETA:   0h 0m2Progress:  83.2% words/sec/thread:   48139 lr:  0.008395 avg.loss:  1.881926 ETA:   0h 0m2Progress:  83.3% words/sec/thread:   48139 lr:  0.008361 avg.loss:  1.881891 ETA:   0h 0m2Progress:  83.3% words/sec/thread:   48139 lr:  0.008327 avg.loss:  1.881800 ETA:   0h 0m2Progress:  83.4% words/sec/thread:   48140 lr:  0.008292 avg.loss:  1.881704 ETA:   0h 0m2Progress:  83.5% words/sec/thread:   48140 lr:  0.008258 avg.loss:  1.881639 ETA:   0h 0m2Progress:  83.6% words/sec/thread:   48141 lr:  0.008223 avg.loss:  1.881655 ETA:   0h 0m2Progress:  83.6% words/sec/thread:   48141 lr:  0.008188 avg.loss:  1.881601 ETA:   0h 0m2Progress:  83.7% words/sec/thread:   48141 lr:  0.008154 avg.loss:  1.881534 ETA:   0h 0m2Progress:  83.8% words/sec/thread:   48140 lr:  0.008120 avg.loss:  1.881537 ETA:   0h 0m2Progress:  83.8% words/sec/thread:   48140 lr:  0.008086 avg.loss:  1.881518 ETA:   0h 0m2Progress:  83.9% words/sec/thread:   48140 lr:  0.008052 avg.loss:  1.881428 ETA:   0h 0m2Progress:  84.0% words/sec/thread:   48140 lr:  0.008018 avg.loss:  1.881420 ETA:   0h 0m2Progress:  84.0% words/sec/thread:   48140 lr:  0.007984 avg.loss:  1.881280 ETA:   0h 0m2Progress:  84.1% words/sec/thread:   48140 lr:  0.007949 avg.loss:  1.881289 ETA:   0h 0m2Progress:  84.2% words/sec/thread:   48140 lr:  0.007916 avg.loss:  1.881198 ETA:   0h 0m2Progress:  84.2% words/sec/thread:   48141 lr:  0.007881 avg.loss:  1.881207 ETA:   0h 0m2Progress:  84.3% words/sec/thread:   48141 lr:  0.007846 avg.loss:  1.881210 ETA:   0h 0m2Progress:  84.4% words/sec/thread:   48141 lr:  0.007812 avg.loss:  1.881175 ETA:   0h 0m2Progress:  84.4% words/sec/thread:   48142 lr:  0.007777 avg.loss:  1.881120 ETA:   0h 0m2Progress:  84.5% words/sec/thread:   48141 lr:  0.007744 avg.loss:  1.881069 ETA:   0h 0m2Progress:  84.6% words/sec/thread:   48142 lr:  0.007709 avg.loss:  1.881073 ETA:   0h 0m2Progress:  84.6% words/sec/thread:   48141 lr:  0.007675 avg.loss:  1.881016 ETA:   0h 0m2Progress:  84.7% words/sec/thread:   48142 lr:  0.007640 avg.loss:  1.880939 ETA:   0h 0m2Progress:  84.8% words/sec/thread:   48143 lr:  0.007606 avg.loss:  1.880906 ETA:   0h 0m2Progress:  84.9% words/sec/thread:   48143 lr:  0.007572 avg.loss:  1.880882 ETA:   0h 0m2Progress:  84.9% words/sec/thread:   48143 lr:  0.007537 avg.loss:  1.880808 ETA:   0h 0m2Progress:  85.0% words/sec/thread:   48143 lr:  0.007503 avg.loss:  1.880737 ETA:   0h 0m2Progress:  85.1% words/sec/thread:   48143 lr:  0.007469 avg.loss:  1.880677 ETA:   0h 0m2Progress:  85.1% words/sec/thread:   48143 lr:  0.007434 avg.loss:  1.880564 ETA:   0h 0m2Progress:  85.2% words/sec/thread:   48143 lr:  0.007400 avg.loss:  1.880549 ETA:   0h 0m2Progress:  85.3% words/sec/thread:   48142 lr:  0.007367 avg.loss:  1.880510 ETA:   0h 0m2Progress:  85.3% words/sec/thread:   48142 lr:  0.007333 avg.loss:  1.880489 ETA:   0h 0m2Progress:  85.4% words/sec/thread:   48142 lr:  0.007299 avg.loss:  1.880494 ETA:   0h 0m2Progress:  85.5% words/sec/thread:   48142 lr:  0.007264 avg.loss:  1.880345 ETA:   0h 0m2Progress:  85.5% words/sec/thread:   48142 lr:  0.007230 avg.loss:  1.880256 ETA:   0h 0m2Progress:  85.6% words/sec/thread:   48143 lr:  0.007195 avg.loss:  1.880222 ETA:   0h 0m2Progress:  85.7% words/sec/thread:   48143 lr:  0.007161 avg.loss:  1.880142 ETA:   0h 0m2Progress:  85.7% words/sec/thread:   48143 lr:  0.007127 avg.loss:  1.880061 ETA:   0h 0m2Progress:  85.8% words/sec/thread:   48143 lr:  0.007093 avg.loss:  1.879982 ETA:   0h 0m2Progress:  85.9% words/sec/thread:   48143 lr:  0.007059 avg.loss:  1.879942 ETA:   0h 0m2Progress:  86.0% words/sec/thread:   48143 lr:  0.007024 avg.loss:  1.879842 ETA:   0h 0m2Progress:  86.0% words/sec/thread:   48142 lr:  0.006991 avg.loss:  1.879800 ETA:   0h 0m2Progress:  86.1% words/sec/thread:   48142 lr:  0.006957 avg.loss:  1.879770 ETA:   0h 0m2Progress:  86.2% words/sec/thread:   48142 lr:  0.006923 avg.loss:  1.879734 ETA:   0h 0m2Progress:  86.2% words/sec/thread:   48142 lr:  0.006888 avg.loss:  1.879710 ETA:   0h 0m2Progress:  86.3% words/sec/thread:   48143 lr:  0.006854 avg.loss:  1.879633 ETA:   0h 0m2Progress:  86.4% words/sec/thread:   48144 lr:  0.006819 avg.loss:  1.879554 ETA:   0h 0m1Progress:  86.4% words/sec/thread:   48144 lr:  0.006784 avg.loss:  1.879554 ETA:   0h 0m1Progress:  86.5% words/sec/thread:   48144 lr:  0.006750 avg.loss:  1.879479 ETA:   0h 0m1Progress:  86.6% words/sec/thread:   48145 lr:  0.006715 avg.loss:  1.879435 ETA:   0h 0m1Progress:  86.6% words/sec/thread:   48145 lr:  0.006681 avg.loss:  1.879417 ETA:   0h 0m1Progress:  86.7% words/sec/thread:   48146 lr:  0.006646 avg.loss:  1.879231 ETA:   0h 0m1Progress:  86.8% words/sec/thread:   48145 lr:  0.006612 avg.loss:  1.879190 ETA:   0h 0m1Progress:  86.8% words/sec/thread:   48145 lr:  0.006579 avg.loss:  1.879129 ETA:   0h 0m1Progress:  86.9% words/sec/thread:   48146 lr:  0.006544 avg.loss:  1.879166 ETA:   0h 0m1Progress:  87.0% words/sec/thread:   48146 lr:  0.006509 avg.loss:  1.879052 ETA:   0h 0m1Progress:  87.1% words/sec/thread:   48146 lr:  0.006475 avg.loss:  1.879030 ETA:   0h 0m1Progress:  87.1% words/sec/thread:   48147 lr:  0.006440 avg.loss:  1.878989 ETA:   0h 0m1Progress:  87.2% words/sec/thread:   48147 lr:  0.006406 avg.loss:  1.878973 ETA:   0h 0m1Progress:  87.3% words/sec/thread:   48147 lr:  0.006372 avg.loss:  1.878991 ETA:   0h 0m1Progress:  87.3% words/sec/thread:   48147 lr:  0.006337 avg.loss:  1.878988 ETA:   0h 0m1Progress:  87.4% words/sec/thread:   48147 lr:  0.006303 avg.loss:  1.878933 ETA:   0h 0m1Progress:  87.5% words/sec/thread:   48146 lr:  0.006269 avg.loss:  1.878939 ETA:   0h 0m1Progress:  87.5% words/sec/thread:   48146 lr:  0.006236 avg.loss:  1.878946 ETA:   0h 0m1Progress:  87.6% words/sec/thread:   48146 lr:  0.006202 avg.loss:  1.878951 ETA:   0h 0m1Progress:  87.7% words/sec/thread:   48146 lr:  0.006168 avg.loss:  1.878872 ETA:   0h 0m1Progress:  87.7% words/sec/thread:   48146 lr:  0.006133 avg.loss:  1.878837 ETA:   0h 0m1Progress:  87.8% words/sec/thread:   48147 lr:  0.006098 avg.loss:  1.878773 ETA:   0h 0m1Progress:  87.9% words/sec/thread:   48146 lr:  0.006064 avg.loss:  1.878729 ETA:   0h 0m1Progress:  87.9% words/sec/thread:   48147 lr:  0.006029 avg.loss:  1.878688 ETA:   0h 0m1Progress:  88.0% words/sec/thread:   48148 lr:  0.005995 avg.loss:  1.878665 ETA:   0h 0m1Progress:  88.1% words/sec/thread:   48148 lr:  0.005960 avg.loss:  1.878636 ETA:   0h 0m1Progress:  88.1% words/sec/thread:   48148 lr:  0.005926 avg.loss:  1.878651 ETA:   0h 0m1Progress:  88.2% words/sec/thread:   48148 lr:  0.005892 avg.loss:  1.878754 ETA:   0h 0m1Progress:  88.3% words/sec/thread:   48147 lr:  0.005858 avg.loss:  1.878853 ETA:   0h 0m1Progress:  88.4% words/sec/thread:   48148 lr:  0.005824 avg.loss:  1.878946 ETA:   0h 0m1Progress:  88.4% words/sec/thread:   48148 lr:  0.005789 avg.loss:  1.879011 ETA:   0h 0m1Progress:  88.5% words/sec/thread:   48149 lr:  0.005754 avg.loss:  1.879075 ETA:   0h 0m1Progress:  88.6% words/sec/thread:   48149 lr:  0.005720 avg.loss:  1.879164 ETA:   0h 0m1Progress:  88.6% words/sec/thread:   48149 lr:  0.005686 avg.loss:  1.879275 ETA:   0h 0m1Progress:  88.7% words/sec/thread:   48149 lr:  0.005652 avg.loss:  1.879384 ETA:   0h 0m1Progress:  88.8% words/sec/thread:   48149 lr:  0.005617 avg.loss:  1.879484 ETA:   0h 0m1Progress:  88.8% words/sec/thread:   48149 lr:  0.005583 avg.loss:  1.879595 ETA:   0h 0m1Progress:  88.9% words/sec/thread:   48149 lr:  0.005549 avg.loss:  1.879683 ETA:   0h 0m1Progress:  89.0% words/sec/thread:   48150 lr:  0.005514 avg.loss:  1.879782 ETA:   0h 0m1Progress:  89.0% words/sec/thread:   48148 lr:  0.005482 avg.loss:  1.879870 ETA:   0h 0m1Progress:  89.1% words/sec/thread:   48148 lr:  0.005447 avg.loss:  1.879969 ETA:   0h 0m1Progress:  89.2% words/sec/thread:   48148 lr:  0.005413 avg.loss:  1.880062 ETA:   0h 0m1Progress:  89.2% words/sec/thread:   48149 lr:  0.005378 avg.loss:  1.880137 ETA:   0h 0m1Progress:  89.3% words/sec/thread:   48149 lr:  0.005344 avg.loss:  1.880214 ETA:   0h 0m1Progress:  89.4% words/sec/thread:   48150 lr:  0.005309 avg.loss:  1.880307 ETA:   0h 0m1Progress:  89.5% words/sec/thread:   48150 lr:  0.005275 avg.loss:  1.880437 ETA:   0h 0m1Progress:  89.5% words/sec/thread:   48150 lr:  0.005240 avg.loss:  1.880519 ETA:   0h 0m1Progress:  89.6% words/sec/thread:   48151 lr:  0.005206 avg.loss:  1.880638 ETA:   0h 0m1Progress:  89.7% words/sec/thread:   48151 lr:  0.005171 avg.loss:  1.880739 ETA:   0h 0m1Progress:  89.7% words/sec/thread:   48151 lr:  0.005137 avg.loss:  1.880814 ETA:   0h 0m1Progress:  89.8% words/sec/thread:   48150 lr:  0.005104 avg.loss:  1.880935 ETA:   0h 0m1Progress:  89.9% words/sec/thread:   48150 lr:  0.005069 avg.loss:  1.881032 ETA:   0h 0m1Progress:  89.9% words/sec/thread:   48151 lr:  0.005035 avg.loss:  1.881157 ETA:   0h 0m1Progress:  90.0% words/sec/thread:   48150 lr:  0.005001 avg.loss:  1.881257 ETA:   0h 0m1Progress:  90.1% words/sec/thread:   48151 lr:  0.004966 avg.loss:  1.881352 ETA:   0h 0m1Progress:  90.1% words/sec/thread:   48152 lr:  0.004931 avg.loss:  1.881438 ETA:   0h 0m1Progress:  90.2% words/sec/thread:   48152 lr:  0.004897 avg.loss:  1.881547 ETA:   0h 0m1Progress:  90.3% words/sec/thread:   48153 lr:  0.004862 avg.loss:  1.881636 ETA:   0h 0m1Progress:  90.3% words/sec/thread:   48153 lr:  0.004828 avg.loss:  1.881713 ETA:   0h 0m1Progress:  90.4% words/sec/thread:   48153 lr:  0.004793 avg.loss:  1.881814 ETA:   0h 0m1Progress:  90.5% words/sec/thread:   48153 lr:  0.004759 avg.loss:  1.881909 ETA:   0h 0m1Progress:  90.5% words/sec/thread:   48153 lr:  0.004725 avg.loss:  1.881979 ETA:   0h 0m1Progress:  90.6% words/sec/thread:   48153 lr:  0.004691 avg.loss:  1.882049 ETA:   0h 0m1Progress:  90.7% words/sec/thread:   48154 lr:  0.004656 avg.loss:  1.882123 ETA:   0h 0m1Progress:  90.8% words/sec/thread:   48153 lr:  0.004622 avg.loss:  1.882242 ETA:   0h 0m1Progress:  90.8% words/sec/thread:   48154 lr:  0.004587 avg.loss:  1.882306 ETA:   0h 0m1Progress:  90.9% words/sec/thread:   48154 lr:  0.004553 avg.loss:  1.882403 ETA:   0h 0m1Progress:  91.0% words/sec/thread:   48152 lr:  0.004518 avg.loss:  1.882499 ETA:   0h 0m1Progress:  91.0% words/sec/thread:   48152 lr:  0.004484 avg.loss:  1.882590 ETA:   0h 0m1Progress:  91.1% words/sec/thread:   48151 lr:  0.004451 avg.loss:  1.882717 ETA:   0h 0m1Progress:  91.2% words/sec/thread:   48151 lr:  0.004417 avg.loss:  1.882807 ETA:   0h 0m1Progress:  91.2% words/sec/thread:   48151 lr:  0.004382 avg.loss:  1.882908 ETA:   0h 0m1Progress:  91.3% words/sec/thread:   48150 lr:  0.004349 avg.loss:  1.882981 ETA:   0h 0m1Progress:  91.4% words/sec/thread:   48148 lr:  0.004316 avg.loss:  1.883047 ETA:   0h 0m1Progress:  91.4% words/sec/thread:   48148 lr:  0.004282 avg.loss:  1.883143 ETA:   0h 0m1Progress:  91.5% words/sec/thread:   48149 lr:  0.004247 avg.loss:  1.883238 ETA:   0h 0m1Progress:  91.6% words/sec/thread:   48149 lr:  0.004213 avg.loss:  1.883330 ETA:   0h 0m1Progress:  91.6% words/sec/thread:   48149 lr:  0.004179 avg.loss:  1.883457 ETA:   0h 0m1Progress:  91.7% words/sec/thread:   48150 lr:  0.004144 avg.loss:  1.883572 ETA:   0h 0m1Progress:  91.8% words/sec/thread:   48149 lr:  0.004110 avg.loss:  1.883672 ETA:   0h 0m1Progress:  91.8% words/sec/thread:   48149 lr:  0.004076 avg.loss:  1.883774 ETA:   0h 0m1Progress:  91.9% words/sec/thread:   48149 lr:  0.004042 avg.loss:  1.883870 ETA:   0h 0m1Progress:  92.0% words/sec/thread:   48149 lr:  0.004008 avg.loss:  1.883995 ETA:   0h 0m1Progress:  92.1% words/sec/thread:   48149 lr:  0.003973 avg.loss:  1.884105 ETA:   0h 0m1Progress:  92.1% words/sec/thread:   48149 lr:  0.003939 avg.loss:  1.884201 ETA:   0h 0m1Progress:  92.2% words/sec/thread:   48149 lr:  0.003905 avg.loss:  1.884280 ETA:   0h 0m1Progress:  92.3% words/sec/thread:   48149 lr:  0.003871 avg.loss:  1.884365 ETA:   0h 0m1Progress:  92.3% words/sec/thread:   48149 lr:  0.003836 avg.loss:  1.884466 ETA:   0h 0m1Progress:  92.4% words/sec/thread:   48149 lr:  0.003802 avg.loss:  1.884513 ETA:   0h 0m1Progress:  92.5% words/sec/thread:   48149 lr:  0.003768 avg.loss:  1.884579 ETA:   0h 0m1Progress:  92.5% words/sec/thread:   48149 lr:  0.003733 avg.loss:  1.884666 ETA:   0h 0m1Progress:  92.6% words/sec/thread:   48149 lr:  0.003699 avg.loss:  1.884736 ETA:   0h 0m1Progress:  92.7% words/sec/thread:   48148 lr:  0.003666 avg.loss:  1.884812 ETA:   0h 0m1Progress:  92.7% words/sec/thread:   48149 lr:  0.003631 avg.loss:  1.884891 ETA:   0h 0m1Progress:  92.8% words/sec/thread:   48149 lr:  0.003597 avg.loss:  1.884984 ETA:   0h 0m1Progress:  92.9% words/sec/thread:   48149 lr:  0.003563 avg.loss:  1.885074 ETA:   0h 0m1Progress:  92.9% words/sec/thread:   48149 lr:  0.003528 avg.loss:  1.885178 ETA:   0h 0m1Progress:  93.0% words/sec/thread:   48149 lr:  0.003493 avg.loss:  1.885226 ETA:   0h 0m1Progress:  93.1% words/sec/thread:   48150 lr:  0.003459 avg.loss:  1.885316 ETA:   0h 0m1Progress:  93.2% words/sec/thread:   48151 lr:  0.003424 avg.loss:  1.885403 ETA:   0h 0m1Progress:  93.2% words/sec/thread:   48151 lr:  0.003389 avg.loss:  1.885508 ETA:   0h 0m Progress:  93.3% words/sec/thread:   48152 lr:  0.003354 avg.loss:  1.885620 ETA:   0h 0m Progress:  93.4% words/sec/thread:   48153 lr:  0.003319 avg.loss:  1.885701 ETA:   0h 0m Progress:  93.4% words/sec/thread:   48151 lr:  0.003286 avg.loss:  1.885792 ETA:   0h 0m Progress:  93.5% words/sec/thread:   48152 lr:  0.003252 avg.loss:  1.885876 ETA:   0h 0m Progress:  93.6% words/sec/thread:   48151 lr:  0.003218 avg.loss:  1.885967 ETA:   0h 0m Progress:  93.6% words/sec/thread:   48151 lr:  0.003183 avg.loss:  1.886058 ETA:   0h 0m Progress:  93.7% words/sec/thread:   48152 lr:  0.003149 avg.loss:  1.886146 ETA:   0h 0m Progress:  93.8% words/sec/thread:   48152 lr:  0.003115 avg.loss:  1.886226 ETA:   0h 0m Progress:  93.8% words/sec/thread:   48152 lr:  0.003080 avg.loss:  1.886309 ETA:   0h 0m Progress:  93.9% words/sec/thread:   48152 lr:  0.003045 avg.loss:  1.886397 ETA:   0h 0m Progress:  94.0% words/sec/thread:   48153 lr:  0.003011 avg.loss:  1.886476 ETA:   0h 0m Progress:  94.0% words/sec/thread:   48153 lr:  0.002977 avg.loss:  1.886543 ETA:   0h 0m Progress:  94.1% words/sec/thread:   48152 lr:  0.002943 avg.loss:  1.886624 ETA:   0h 0m Progress:  94.2% words/sec/thread:   48152 lr:  0.002909 avg.loss:  1.886709 ETA:   0h 0m Progress:  94.3% words/sec/thread:   48153 lr:  0.002874 avg.loss:  1.886790 ETA:   0h 0m Progress:  94.3% words/sec/thread:   48152 lr:  0.002840 avg.loss:  1.886847 ETA:   0h 0m Progress:  94.4% words/sec/thread:   48153 lr:  0.002806 avg.loss:  1.886938 ETA:   0h 0m Progress:  94.5% words/sec/thread:   48154 lr:  0.002770 avg.loss:  1.887003 ETA:   0h 0m Progress:  94.5% words/sec/thread:   48154 lr:  0.002736 avg.loss:  1.887089 ETA:   0h 0m Progress:  94.6% words/sec/thread:   48154 lr:  0.002702 avg.loss:  1.887174 ETA:   0h 0m Progress:  94.7% words/sec/thread:   48154 lr:  0.002667 avg.loss:  1.887288 ETA:   0h 0m Progress:  94.7% words/sec/thread:   48155 lr:  0.002632 avg.loss:  1.887380 ETA:   0h 0m Progress:  94.8% words/sec/thread:   48155 lr:  0.002598 avg.loss:  1.887507 ETA:   0h 0m Progress:  94.9% words/sec/thread:   48155 lr:  0.002564 avg.loss:  1.887581 ETA:   0h 0m Progress:  94.9% words/sec/thread:   48155 lr:  0.002530 avg.loss:  1.887644 ETA:   0h 0m Progress:  95.0% words/sec/thread:   48155 lr:  0.002495 avg.loss:  1.887743 ETA:   0h 0m Progress:  95.1% words/sec/thread:   48155 lr:  0.002461 avg.loss:  1.887819 ETA:   0h 0m Progress:  95.1% words/sec/thread:   48155 lr:  0.002427 avg.loss:  1.887913 ETA:   0h 0m Progress:  95.2% words/sec/thread:   48155 lr:  0.002392 avg.loss:  1.888002 ETA:   0h 0m Progress:  95.3% words/sec/thread:   48156 lr:  0.002358 avg.loss:  1.888115 ETA:   0h 0m Progress:  95.4% words/sec/thread:   48155 lr:  0.002324 avg.loss:  1.888213 ETA:   0h 0m Progress:  95.4% words/sec/thread:   48156 lr:  0.002289 avg.loss:  1.888294 ETA:   0h 0m Progress:  95.5% words/sec/thread:   48156 lr:  0.002255 avg.loss:  1.888358 ETA:   0h 0m Progress:  95.6% words/sec/thread:   48156 lr:  0.002220 avg.loss:  1.888431 ETA:   0h 0m Progress:  95.6% words/sec/thread:   48155 lr:  0.002187 avg.loss:  1.888503 ETA:   0h 0m Progress:  95.7% words/sec/thread:   48156 lr:  0.002152 avg.loss:  1.888562 ETA:   0h 0m Progress:  95.8% words/sec/thread:   48156 lr:  0.002118 avg.loss:  1.888609 ETA:   0h 0m Progress:  95.8% words/sec/thread:   48155 lr:  0.002084 avg.loss:  1.888699 ETA:   0h 0m Progress:  95.9% words/sec/thread:   48156 lr:  0.002049 avg.loss:  1.888763 ETA:   0h 0m Progress:  96.0% words/sec/thread:   48156 lr:  0.002014 avg.loss:  1.888854 ETA:   0h 0m Progress:  96.0% words/sec/thread:   48157 lr:  0.001980 avg.loss:  1.888925 ETA:   0h 0m Progress:  96.1% words/sec/thread:   48157 lr:  0.001945 avg.loss:  1.888976 ETA:   0h 0m Progress:  96.2% words/sec/thread:   48158 lr:  0.001910 avg.loss:  1.889032 ETA:   0h 0m Progress:  96.2% words/sec/thread:   48158 lr:  0.001875 avg.loss:  1.889097 ETA:   0h 0m Progress:  96.3% words/sec/thread:   48159 lr:  0.001841 avg.loss:  1.889171 ETA:   0h 0m Progress:  96.4% words/sec/thread:   48158 lr:  0.001807 avg.loss:  1.889245 ETA:   0h 0m Progress:  96.5% words/sec/thread:   48159 lr:  0.001772 avg.loss:  1.889309 ETA:   0h 0m Progress:  96.5% words/sec/thread:   48159 lr:  0.001738 avg.loss:  1.889352 ETA:   0h 0m Progress:  96.6% words/sec/thread:   48159 lr:  0.001704 avg.loss:  1.889423 ETA:   0h 0m Progress:  96.7% words/sec/thread:   48159 lr:  0.001669 avg.loss:  1.889521 ETA:   0h 0m Progress:  96.7% words/sec/thread:   48160 lr:  0.001634 avg.loss:  1.889625 ETA:   0h 0m Progress:  96.8% words/sec/thread:   48161 lr:  0.001599 avg.loss:  1.889693 ETA:   0h 0m Progress:  96.9% words/sec/thread:   48161 lr:  0.001564 avg.loss:  1.889781 ETA:   0h 0m Progress:  96.9% words/sec/thread:   48162 lr:  0.001529 avg.loss:  1.889865 ETA:   0h 0m Progress:  97.0% words/sec/thread:   48163 lr:  0.001494 avg.loss:  1.889966 ETA:   0h 0m Progress:  97.1% words/sec/thread:   48163 lr:  0.001460 avg.loss:  1.890041 ETA:   0h 0m Progress:  97.1% words/sec/thread:   48163 lr:  0.001426 avg.loss:  1.890135 ETA:   0h 0m Progress:  97.2% words/sec/thread:   48164 lr:  0.001391 avg.loss:  1.890211 ETA:   0h 0m Progress:  97.3% words/sec/thread:   48164 lr:  0.001356 avg.loss:  1.890302 ETA:   0h 0m Progress:  97.4% words/sec/thread:   48164 lr:  0.001322 avg.loss:  1.890388 ETA:   0h 0m Progress:  97.4% words/sec/thread:   48164 lr:  0.001287 avg.loss:  1.890491 ETA:   0h 0m Progress:  97.5% words/sec/thread:   48165 lr:  0.001253 avg.loss:  1.890568 ETA:   0h 0m Progress:  97.6% words/sec/thread:   48165 lr:  0.001218 avg.loss:  1.890660 ETA:   0h 0m Progress:  97.6% words/sec/thread:   48166 lr:  0.001183 avg.loss:  1.890745 ETA:   0h 0m Progress:  97.7% words/sec/thread:   48166 lr:  0.001148 avg.loss:  1.890830 ETA:   0h 0m Progress:  97.8% words/sec/thread:   48167 lr:  0.001113 avg.loss:  1.890924 ETA:   0h 0m Progress:  97.8% words/sec/thread:   48167 lr:  0.001079 avg.loss:  1.890997 ETA:   0h 0m Progress:  97.9% words/sec/thread:   48166 lr:  0.001046 avg.loss:  1.891093 ETA:   0h 0m Progress:  98.0% words/sec/thread:   48167 lr:  0.001011 avg.loss:  1.891179 ETA:   0h 0m Progress:  98.0% words/sec/thread:   48167 lr:  0.000976 avg.loss:  1.891258 ETA:   0h 0m Progress:  98.1% words/sec/thread:   48168 lr:  0.000941 avg.loss:  1.891335 ETA:   0h 0m Progress:  98.2% words/sec/thread:   48168 lr:  0.000907 avg.loss:  1.891434 ETA:   0h 0m Progress:  98.3% words/sec/thread:   48169 lr:  0.000872 avg.loss:  1.891531 ETA:   0h 0m Progress:  98.3% words/sec/thread:   48169 lr:  0.000837 avg.loss:  1.891671 ETA:   0h 0m Progress:  98.4% words/sec/thread:   48169 lr:  0.000803 avg.loss:  1.891743 ETA:   0h 0m Progress:  98.5% words/sec/thread:   48169 lr:  0.000769 avg.loss:  1.891830 ETA:   0h 0m Progress:  98.5% words/sec/thread:   48170 lr:  0.000734 avg.loss:  1.891917 ETA:   0h 0m Progress:  98.6% words/sec/thread:   48170 lr:  0.000699 avg.loss:  1.892037 ETA:   0h 0m Progress:  98.7% words/sec/thread:   48170 lr:  0.000665 avg.loss:  1.892085 ETA:   0h 0m Progress:  98.7% words/sec/thread:   48170 lr:  0.000630 avg.loss:  1.892147 ETA:   0h 0m Progress:  98.8% words/sec/thread:   48171 lr:  0.000596 avg.loss:  1.892243 ETA:   0h 0m Progress:  98.9% words/sec/thread:   48170 lr:  0.000562 avg.loss:  1.892335 ETA:   0h 0m Progress:  98.9% words/sec/thread:   48171 lr:  0.000527 avg.loss:  1.892421 ETA:   0h 0m Progress:  99.0% words/sec/thread:   48171 lr:  0.000493 avg.loss:  1.892512 ETA:   0h 0m Progress:  99.1% words/sec/thread:   48172 lr:  0.000458 avg.loss:  1.892609 ETA:   0h 0m Progress:  99.2% words/sec/thread:   48172 lr:  0.000423 avg.loss:  1.892697 ETA:   0h 0m Progress:  99.2% words/sec/thread:   48173 lr:  0.000388 avg.loss:  1.892766 ETA:   0h 0m Progress:  99.3% words/sec/thread:   48174 lr:  0.000353 avg.loss:  1.892870 ETA:   0h 0m Progress:  99.4% words/sec/thread:   48174 lr:  0.000319 avg.loss:  1.892960 ETA:   0h 0m Progress:  99.4% words/sec/thread:   48173 lr:  0.000285 avg.loss:  1.893021 ETA:   0h 0m Progress:  99.5% words/sec/thread:   48174 lr:  0.000250 avg.loss:  1.893088 ETA:   0h 0m Progress:  99.6% words/sec/thread:   48174 lr:  0.000216 avg.loss:  1.893192 ETA:   0h 0m Progress:  99.6% words/sec/thread:   48173 lr:  0.000182 avg.loss:  1.893282 ETA:   0h 0m Progress:  99.7% words/sec/thread:   48174 lr:  0.000147 avg.loss:  1.893361 ETA:   0h 0m Progress:  99.8% words/sec/thread:   48174 lr:  0.000113 avg.loss:  1.893452 ETA:   0h 0m Progress:  99.8% words/sec/thread:   48174 lr:  0.000078 avg.loss:  1.893523 ETA:   0h 0m Progress:  99.9% words/sec/thread:   48175 lr:  0.000043 avg.loss:  1.893565 ETA:   0h 0m Progress: 100.0% words/sec/thread:   48176 lr:  0.000008 avg.loss:  1.893657 ETA:   0h 0m Progress: 100.0% words/sec/thread:   48151 lr: -0.000000 avg.loss:  1.893676 ETA:   0h 0m Progress: 100.0% words/sec/thread:   48151 lr:  0.000000 avg.loss:  1.893676 ETA:   0h 0m 0s

real    2m29.285s
user    75m19.959s
sys     0m10.405s
+ python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word အိပ်မက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'အိပ်မက်':
[-4.8458789e-02 -2.4486806e-02  5.1058471e-01 -9.8131195e-02
  1.7729288e-01  2.7946243e-01 -2.4123581e-01 -6.2306511e-01
  2.1663684e-01  6.2643629e-01  4.1385987e-01  3.2314926e-02
 -2.9310057e-01 -8.6910439e-01 -2.8973854e-01 -3.7574703e-01
 -5.0859851e-01  5.8768922e-01 -4.8046789e-01  1.0515047e-01
  2.4784786e-01  1.6641980e-01  7.2318059e-01  6.7487024e-02
 -2.2673577e-01 -1.7776145e-01  3.1949058e-01 -3.0548224e-01
  5.0424176e-01 -1.1092866e-01 -1.0390022e-01  3.5861087e-01
  1.4319155e-01 -6.3946456e-01 -3.7639141e-01  4.5002848e-01
 -1.3165213e-01 -1.5153673e-01 -5.7670856e-01  2.1287592e-01
 -2.5345209e-01  9.8429032e-02 -4.6397787e-01  5.8103931e-01
 -6.0314775e-01  2.4319604e-01  6.7873704e-01 -1.1321589e-03
  3.0353791e-01  4.4204384e-02 -4.6922183e-01  1.5668480e-01
 -1.1890617e-01 -5.5016968e-03 -5.4999548e-01 -3.1320879e-01
  1.0855770e-01 -4.4565946e-02  6.8322676e-01  2.2341900e-01
 -5.7226998e-01  2.9931358e-01  2.0298180e-01  2.5418356e-01
 -4.5725068e-01  3.4808102e-01  1.7415519e-01  2.1237148e-01
  1.7538239e-01  1.2887250e-01 -2.4321577e-01  3.2841793e-01
  5.6977099e-01  3.4155554e-01 -3.0711904e-01  4.6865499e-01
 -8.0100441e-01 -3.7291056e-01 -7.2513923e-02  6.6177286e-02
 -3.5532293e-01  6.2899642e-02  1.1552530e-01  5.8236036e-02
 -3.6463708e-01  1.1728733e+00 -5.3349084e-01 -2.8017882e-01
 -2.9709616e-01 -2.7054167e-01  3.8002115e-01 -3.0764794e-01
 -3.3946174e-01  8.6696818e-02 -3.2582587e-01  4.1524164e-02
  2.3727676e-01  8.0608028e-01 -5.1396793e-01  6.6342480e-02]

real    0m1.084s
user    0m1.870s
sys     0m2.679s
+ python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အိပ်မက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အိပ်မက်':
Score: 0.7488265633583069, Word: မက်
Score: 0.7464785575866699, Word: အိပ်မက်ဆိုး
Score: 0.7380164861679077, Word: အိပ်မက်လေး
Score: 0.7047110199928284, Word: အိပ်မက်မက်
Score: 0.646929144859314, Word: ကောသလ
Score: 0.6423190236091614, Word: မြင်မက်
Score: 0.5184760093688965, Word: စိတ်ကူးယဉ်
Score: 0.5184512734413147, Word: ဧကဒသမ
Score: 0.5149016976356506, Word: အမရာဖုန်း
Score: 0.5139212608337402, Word: အတိတ်နိမိတ်

real    0m1.290s
user    0m1.978s
sys     0m2.777s
+ python3 fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy 'အချစ် အမုန်း စိတ်ဆိုး' --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အချစ် - အမုန်း + စိတ်ဆိုး
Analogies result:
Word: စိတ်ကောက်, Score: 0.5393816828727722
Word: ခါးခါးသီးသီး, Score: 0.5151046514511108
Word: အလျှော့, Score: 0.5079465508460999
Word: အိပ်မက်ဆိုး, Score: 0.5047312378883362
Word: ရင်ဖွင့်, Score: 0.5040906667709351
Word: မယုံမကြည်, Score: 0.5007020831108093
Word: စကားနာထိုး, Score: 0.4958913028240204
Word: အစန်း, Score: 0.4908232092857361
Word: သည်းခံမပေး, Score: 0.4880407154560089
Word: ကာသာ, Score: 0.4840039908885956
+ set +x
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$
```

## Prepared a Python code for Testing with Input File

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

## Prepared a Shell Script for Testing with Input File

ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ chmod +x ./run_ftlm_test_with_file.sh  

```bash
#!/bin/bash

# for word_vector
python3 ./ftlm_test_with_file.py --input ./test1.txt --operation word_vector

# for nearest_neighbors
python3 ./ftlm_test_with_file.py --input ./test1.txt --operation nearest_neighbors

# for word_analogies
python3 ./ftlm_test_with_file.py --input ./test2.txt --operation word_analogies
```

## Prepare Test-Data Files

test1.txt is as follows:  

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ cat test1.txt
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

Test file (test2.txt) for word_analogies testing:  

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ cat test2.txt
ဝက် ဝက်သား ကြက်
ဘုရင် မိဖုရား ဘုန်းကြီး
အထီး အမ ယောက်ျား
ရေ ရေခွက် အရက်
လက်ရှည် လက်တို ဘောင်းဘီရှည်
အချစ် အမုန်း အပြုံး
```

## Testing with Input Files

Run the shell script ...  

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ ./run_ftlm_test_with_file.sh | tee test_with_file_input.log
Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word စိတ္တဇ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'စိတ္တဇ':
[-4.61243570e-01  3.59516054e-01  1.10111272e+00 -1.23498619e+00
  3.86580616e-01  5.50562680e-01 -1.95744246e-01 -2.79098004e-01
 -1.44110814e-01  9.07426238e-01 -4.88572121e-01 -4.17411894e-01
  1.00684807e-01 -9.90772426e-01 -6.27999067e-01  2.06491128e-01
 -9.92151022e-01  7.98848689e-01 -1.02826461e-01 -3.88897002e-01
  1.43366873e-01  6.96307480e-01  6.34460151e-01 -6.80318326e-02
  3.43423218e-01  1.33263171e-01 -1.76689804e-01 -4.79032725e-01
  2.44270056e-01 -8.68480504e-01 -2.20922649e-01 -6.12425148e-01
 -1.37158945e-01 -2.37383783e-01 -4.00406092e-01 -2.30984315e-01
 -6.60826713e-02 -4.75721478e-01  1.65775210e-01 -1.35185510e-01
 -5.29746175e-01  1.20370224e-01  1.86605245e-01  2.71222740e-01
  1.00021839e+00  4.97763038e-01  7.00700760e-01  4.74556625e-01
  6.33076787e-01  1.05251156e-01 -6.10619962e-01  2.18991712e-01
  1.62523985e-01 -7.88495421e-01 -4.81464297e-01 -3.55965160e-02
  8.40244353e-01 -3.93840551e-01  4.57118094e-01 -9.46300402e-02
  2.93241948e-01 -2.59939373e-01  1.12112188e+00  6.88830853e-01
 -2.17285514e-01  6.46571219e-01  5.36031365e-01  7.53298402e-04
 -1.40864700e-01 -5.04136860e-01 -8.68239462e-01  4.94253695e-01
 -1.31907329e-01 -3.78319740e-01 -7.06739843e-01  9.14467126e-02
  1.85969010e-01  1.95539474e-01  4.16892767e-02 -5.42600930e-01
 -1.55656934e-01  3.72658372e-01 -1.78509764e-02 -7.73138851e-02
  5.80567122e-03  1.16516851e-01  1.71922848e-01  8.15192163e-02
  1.69001177e-01  5.57840526e-01 -3.68318856e-01  1.48532495e-01
 -2.22696349e-01 -3.37793052e-01 -6.00888729e-01  6.78536892e-02
  9.48494673e-02  4.21288311e-02  5.31411320e-02 -6.39567494e-01]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ရည်းစား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ရည်းစား':
[ 0.18350312  0.11539231  0.72136104  0.43853816  0.1774953   0.04232936
 -0.03577008  0.04299934  0.03878647  0.884873    0.03926616  0.20777826
  0.31533027 -0.61309564 -0.26909956 -0.65250427  0.1314337   0.33463043
 -0.2678067  -0.96479785 -0.20676254 -0.01190126 -0.28153118 -0.23327512
 -0.23918214  0.10819263 -0.6776352  -0.1775321   0.10618776  0.10535552
 -0.4467323  -0.3828028  -0.2735994  -0.5214353  -0.36003298  0.39651796
  0.01039605 -0.34373754 -0.14448686 -0.25234994 -0.01796346 -0.3464214
  0.7556571   0.40079516  0.3995157   0.56787354  0.05639415  0.33831933
 -0.40227887  0.17785409 -0.3384434   0.47514674 -0.22792937 -0.16378747
 -0.49558538 -0.15207076  0.3190234   0.5221266   0.4660445  -0.38964435
 -0.83155626  0.19413783  0.6262      0.34703618  0.08021066  0.11998545
  0.25351274  0.3859742  -0.45298553 -0.51110256 -0.48014316  0.3036761
  0.2107512   0.26069978 -0.33036503 -0.30511546 -0.35517168 -0.15387945
 -0.10906395 -0.71284795  0.35965884 -0.14760953  0.12717156  0.59973615
  0.0996118   0.41719234 -0.32435372  0.26942688 -0.5197583   0.05725256
  0.19144583 -0.7555786   0.306573   -0.72335994 -0.2389975   0.16689983
 -0.1940737  -0.03712358  0.24944346 -0.18530971]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word အမေ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'အမေ':
[ 0.03071883 -0.25971985  0.40830743  0.11242703 -0.12839618 -0.00550127
  0.05469747 -0.10745972 -0.15699431  0.3023142  -0.29259813  0.16690251
  0.07785437 -0.58479047 -0.7412099  -0.04547881 -0.03287222 -0.11044414
 -0.08638554 -0.02459145 -0.08973993 -0.02339625 -0.28159484  0.24005242
  0.0358529  -0.6657557   0.27617294 -0.59123087  0.1455806   0.18249877
  0.12091456 -0.4804478  -0.00294562 -0.56233424  0.278252    0.11192498
  0.14295132  0.05967402 -0.12034112  0.05577437 -0.293318   -0.31646758
  0.21822222 -0.40633217  0.17665516  0.2565288  -0.14461318 -0.08262646
  0.4971917   0.3262872   0.09940107  0.18980542 -0.04641127  0.9501322
  0.08271138  0.02752739 -0.17911749 -0.22868471  0.34966385  0.13285655
 -0.06082508 -0.1977889   0.9427577   0.50436085  0.2823574  -0.19498166
  0.1311327  -0.09055237  0.31270525  0.13989182 -0.84258276  0.30009115
 -0.3908675   0.14674334 -0.4403673  -0.3262866  -0.26670656  0.24394107
  0.18048933 -0.23953764  0.02176909 -0.29563728  0.10838298  0.12806904
  0.09947888  0.0433741  -0.11379734  0.20521459  0.01840506  0.24994595
  0.24415538 -0.19377986 -0.1143683  -0.30197594  0.12075205 -0.24896991
 -0.11793793  0.49135238  0.0792672   0.16126719]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word သာဓု --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'သာဓု':
[-0.98352873 -0.0695949   0.3714132   0.5298216   0.05769559  0.12682979
 -1.0482336  -0.27413246  0.36196014  0.4132363  -1.5299553   0.23318763
  0.48894048 -0.47652707  0.20415807 -0.4201265  -0.19519183 -0.54136795
  0.1900705  -1.2804891  -0.40513307 -0.06873322 -0.33222723 -0.5652567
 -0.54555476 -0.47325775  0.52416986  0.01625465 -0.16371305 -0.16311078
  0.37537968  0.1431944  -0.37065732 -1.0512786  -0.22825406 -0.6039058
 -0.23366335  0.54515165  0.05307398 -0.2989023  -0.38226736 -0.60125357
 -0.60638714  0.17668483  0.5587475  -0.34886274 -0.07461213  0.18462121
  0.7460933   0.576233   -0.76363945 -0.7422677  -0.56196225 -0.04852536
  0.6577258   0.14395425  0.38339487  0.37458548  0.18185237 -0.3491058
 -0.52669203 -0.53742     0.5456631   0.0324105  -0.522795   -0.15123408
  0.521301   -0.07944807 -0.18765166  0.08098649 -0.25905928  0.32374802
 -0.38589165  0.10780024  0.13277574 -0.50468236 -0.70396155 -0.76891667
  0.8336255  -0.09163614 -0.00314118  1.0390295  -0.4873732  -0.22306018
  0.16167276  0.25150904 -0.11911882 -0.4026206   0.21783903 -0.35505015
  0.03703986 -0.2567889   0.15904881 -0.45394665 -0.21197641 -1.5640644
 -0.14581154  1.1145556  -0.31788006 -0.01123831]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word မုန့်ဟင်းခါး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'မုန့်ဟင်းခါး':
[ 0.02072911 -0.33968386 -0.00712556  0.3429807   0.38542584 -0.8341492
  0.29026207  0.2922137   0.04039382  0.44566974 -0.10547614 -0.11653781
  0.2035024  -0.22189981 -0.26649544 -0.02591226 -0.20875455 -0.49668196
  0.02908725  0.0972037  -0.28819057  0.6714998   0.25353217  0.07176629
 -0.6297372   0.04526541 -0.80546224 -0.300375    0.42683533  0.50956
 -0.4328399   0.37141195  0.09998427 -0.9005982   0.09338199  0.7211069
 -0.03976711 -0.16917999 -0.50410086  0.23897766  0.38801482 -0.09667145
 -0.5514925  -0.68928313  0.86968315  0.58271474  0.44007394 -0.35681865
  0.06056396  0.4614208   0.9760795   0.16010152 -0.50962526  0.11868954
  0.58964235 -0.11125648 -0.17581423  0.23699535 -0.01459764 -0.18870556
 -0.8227549   0.3161526   1.0388361   0.85891026 -0.45570007 -0.070025
  0.7118411  -0.02797711 -0.13516368 -0.15966047 -0.7897511   0.95739925
  0.5297775   0.6391254  -0.3390045  -0.3692309   0.2724196   1.0055679
  0.62526786  0.22983114 -0.39362374  0.4997484  -0.36732307  0.24460736
 -0.40372536  0.5350609  -0.8402607  -0.33668005  1.2955524   0.5557153
 -0.1464518  -0.28226998  0.27271658 -0.34058365 -0.05151579 -0.0763374
  0.30214277 -0.30948433 -0.1329393  -0.43750456]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word အင်တာနက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'အင်တာနက်':
[ 0.02461799 -0.4431483   0.40922284  0.12563924  0.2722572  -1.288857
  0.06817558 -0.03444771 -0.081062   -0.27401862  0.29866892  0.20236981
  0.58547574 -0.5498527  -0.41020113  0.05787311  0.3199483  -0.59399354
  0.34097305  0.06043766 -0.37805536  0.26828137  0.98806375 -0.00550441
 -0.39155293 -0.74719656 -0.00755718 -0.4063354  -0.1110691  -0.37200257
  0.15717864 -0.26558068  0.26360613 -0.9740983  -0.3815031  -0.41300339
  0.26984027 -0.18501376  0.8520442   0.631234    0.14000505  1.0974772
  0.15302046  0.10405287 -0.6867668  -0.20986141  0.1332902   0.05378478
 -0.07629456 -0.29041228  0.18000452 -0.6115938  -0.44820562 -0.54375345
 -0.33489463  0.72252595  0.12722687  0.5527463   0.6825161  -0.6390982
 -0.06817158  0.2984414   0.2557105   0.13732181  0.5614249   0.25027475
  0.46363178  0.39790303  0.06236941 -0.03253197 -0.03003915  0.73207664
  0.26094547  0.5225181  -0.41999203  0.4743654   0.3807453  -0.2704268
  0.14386329  0.19669594  0.24841078  0.07408433 -0.47021824  0.8097635
  0.4291805   0.38897836 -0.02447556 -0.07200308  0.34446022  0.09325077
 -0.19339983 -0.5036389   0.04551039 -0.2953481   0.8242626  -0.40197667
  0.6710595  -0.09562401  0.37285838  0.13070965]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ရန်ကုန် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ရန်ကုန်':
[ 0.1290069  -0.03592684 -0.11867675  0.2257954  -0.473563   -0.35239777
 -0.57181484 -0.03475319 -0.23708783  0.65030825 -0.10124014 -0.13400957
  0.35240486 -0.31402165 -0.06719279 -0.13503654 -0.3156866   0.26883408
  0.21558973 -0.19340332  0.08023257  0.2563325  -0.4438472   0.0402977
 -0.02622619 -0.02527681 -0.1377785  -0.14589903  0.07671191  0.20021753
  0.06076101 -0.21933049  0.31538692 -0.51681095 -0.46547598  0.27212393
  0.18232009 -0.25668526  0.3435244   0.5222832   0.25110954  0.1394268
  0.61469513  0.01020287  0.19071501  0.02437381  0.15632175  0.5767516
  0.04862933  0.53299165  0.13623665  0.33232126 -0.33950406  0.13628983
  0.01701202 -0.16348657  0.11445231  0.14815888  0.80946743 -0.21395455
 -0.07798062 -0.13582835  0.5317322  -0.33269858  0.294773   -0.26937526
  0.27690625  0.34209117  0.02261608  0.49219635  0.21363184  0.07988419
 -0.05811987  0.02318041  0.13980088  0.04466502  0.50008696 -0.48551032
  0.0749235   0.10014639 -0.27442455  0.15959047  0.03612575  0.10304827
  0.10890328  0.31755283  0.26686567 -0.18268637  0.30847842  0.00947756
 -0.59516424  0.630735   -0.1476929  -0.36211884  0.61772114 -0.2904968
 -0.48713648  0.10415425 -0.03689265 -0.02923396]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ဆီးသွား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ဆီးသွား':
[ 0.30889457 -0.24022423  0.6738354  -0.09143853  0.0238545  -0.39983255
  0.12452907  0.1890093   0.24707654  0.2498872  -0.30960083 -0.7372539
  0.42957556 -0.34163505  0.11622167 -0.7438044  -0.34981978 -0.51832503
 -0.39606157 -0.05553234  0.00231808  0.6269972   0.10348926  0.33396992
  0.12302213 -0.11410822  0.24557325  0.00379447  0.4236756   0.12663548
  0.18407924  0.02252115  0.13579771 -0.6514597  -0.53494865  0.33799398
 -0.6177018  -0.22036874 -0.12875856  0.6231622  -0.5091494   0.13618074
 -0.01086953 -0.19985373  0.19994856  0.39508855  0.11878891  0.05710852
  0.05556532 -0.3811469   0.2926302   0.18426585  0.24741025  0.20425892
 -0.08479438 -0.02059691 -0.07126204  0.51409423 -0.17675117  0.39609286
 -0.3106801  -0.22710319  0.93982136 -0.08874829  0.31514803 -0.25552866
  0.18808317 -0.1803307  -0.16162358 -0.20018442 -0.08266675  0.96403706
  0.37243214  0.61621135 -0.5130176   0.45905706  0.63896435 -0.16088215
  0.36281252 -0.5353707  -0.37864256  0.4023435  -0.75810784  0.27769092
  0.40118644  0.19029775 -0.08754174  0.17557608  0.22842206 -0.45689037
 -0.5243021   0.19055322  0.05155192 -0.5410387  -0.1626779  -0.7710871
  0.06063039 -0.7033961   0.2709069   0.81557333]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word ဇာတ်ပို့ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'ဇာတ်ပို့':
[ 0.42967802  0.06222415  0.32258934  0.74104357  0.6136585   0.5638834
 -0.19919515 -0.62080586  0.14988399  0.77782017 -0.290407    0.13919571
  0.7496261  -0.11823046 -0.38165146  0.46824044 -0.34447688  0.10193388
  0.21913485 -0.4019656   0.13324502  0.67584676 -0.25668386  0.30223966
 -0.4505775  -0.69542354  0.00951281 -0.14878854  0.10965131 -0.340871
  0.26378822 -0.3833829   0.167806   -0.906731    0.59496224  0.55628663
  0.26787353 -0.23471022  0.6428358   0.8261384  -0.6044568  -0.29376
 -0.15058315 -0.387981    0.34866467 -0.63532734  0.44170386  0.05479419
 -0.24394608 -0.6073834   0.04890009  0.30766934 -0.33786878 -0.34087625
 -0.33116215 -0.07938308  0.25266856  0.21834025 -0.5017361  -0.17699541
 -0.09011719  0.07833123  0.649292   -0.5736984  -0.43354297 -0.39860043
  0.724592    0.35849246 -0.07274796 -0.94739145 -0.08727514  0.73910064
  0.08633166  0.70521563 -0.9183612   0.04892223 -0.7648514  -0.28440505
  0.08033073  0.06013325  0.74668765  0.388712   -0.19079779  0.47967753
  0.38138676  1.3278297  -0.43962085 -0.5748396   0.40653312  0.0720482
  0.35342944 -0.69833887  0.7918739   0.12838788 -0.6222508  -0.314533
  0.8493724   0.35461915  0.50917065  0.22309946]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_vector --word တင်္ခဏုပ္ပတ္တိဉာဏ် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Vector for 'တင်္ခဏုပ္ပတ္တိဉာဏ်':
[-3.6252519e-01 -3.0949891e-01 -2.7171924e-04  1.6744243e-01
 -1.8561958e-01  3.5400495e-02  6.5129362e-02 -4.2849746e-01
  8.3449000e-01  9.5084769e-01  1.2962839e-01 -1.8867044e-01
 -1.5725384e-02 -4.7682467e-01 -1.7319387e-01 -2.1641649e-01
 -8.9325339e-02  3.3020240e-01  6.3709714e-02  2.8195310e-01
 -1.7241758e-01 -6.9780841e-02 -6.9425836e-02  2.7824530e-02
 -1.8123594e-01 -3.0149928e-01  1.9423731e-01 -2.4474090e-01
  5.0549179e-01 -2.4687904e-01  1.7687345e-01  1.1030598e-01
 -3.3118302e-01 -5.7657820e-01 -2.1268226e-01  8.4286436e-02
  4.2713130e-01 -2.2583288e-01  3.0705658e-01  2.5753587e-01
  2.1591781e-01 -2.2626346e-02 -5.1623034e-01  1.4342192e-01
 -4.2802465e-01  4.8864338e-01  4.5662701e-02 -1.3786264e-01
  2.4476588e-01 -1.5040088e-01 -1.8311977e-01  3.4235847e-01
 -3.8464418e-01 -4.3917122e-01  1.4084108e-01 -2.5692081e-01
  4.0236440e-01  2.8275117e-01 -5.7646304e-01 -2.5643867e-01
  8.4712775e-03  2.0903388e-01  1.7546982e-01 -2.6228231e-01
  7.0875943e-01  3.6593717e-02  1.8138285e-01 -4.6774086e-02
 -5.9045102e-03 -2.1474726e-01 -5.2226430e-01  7.2871947e-01
  2.1999292e-01  3.7599854e-02 -5.0268906e-01 -1.0626889e-01
 -3.8652360e-01  2.3077419e-01  2.1548398e-01 -3.0149430e-01
 -5.0856608e-01  1.0031799e-01  3.4728828e-01 -1.4690076e-01
  6.2533629e-01  1.3482949e-01 -3.0025688e-01  6.3554621e-01
  1.7992024e-01  2.3680243e-01  2.0809354e-01 -1.3708320e-01
  5.7401109e-02  4.1160006e-02 -7.3975539e-01 -2.1292947e-01
 -3.1068232e-02  1.1903800e+00 -1.0617174e-01  2.9745075e-01]

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word စိတ္တဇ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'စိတ္တဇ':
Score: 0.6108500957489014, Word: စိတ္တ
Score: 0.5902635455131531, Word: စိတ္တဗေဒ
Score: 0.5444585680961609, Word: စွဲလမ်း
Score: 0.5171483755111694, Word: အစွဲ
Score: 0.4977812170982361, Word: စိတ္တသုခ
Score: 0.49112340807914734, Word: အစွဲအလမ်း
Score: 0.4869803786277771, Word: စိတ်တုံးတုံးချ
Score: 0.48271381855010986, Word: ခေါင်းထဲစွဲ
Score: 0.47994092106819153, Word: တွေးမိတွေးရာ
Score: 0.4793800115585327, Word: နစ်မြှုပ်

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ရည်းစား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ရည်းစား':
Score: 0.7490476965904236, Word: ရည်းစားစာ
Score: 0.6610181927680969, Word: တောဂေါ်လီ
Score: 0.6460698246955872, Word: သမီးရည်းစား
Score: 0.6383684873580933, Word: ရည်းစားဟောင်း
Score: 0.6370531320571899, Word: ဒိတ်ဒိတ်ကျဲ
Score: 0.6323522925376892, Word: အနမ်း
Score: 0.6254004836082458, Word: လရိပ်ချို
Score: 0.5798743367195129, Word: ရွှေရင်အေး
Score: 0.5657164454460144, Word: သူငယ်ချင်း
Score: 0.5643782615661621, Word: သူငယ်ချင်းလေး

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အမေ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အမေ':
Score: 0.770022988319397, Word: အဖေ
Score: 0.7500655055046082, Word: အမေ့
Score: 0.7253955602645874, Word: အမေအမေ
Score: 0.6909012198448181, Word: ကအမေ
Score: 0.6774681210517883, Word: သမီး
Score: 0.6317156553268433, Word: အမေစု
Score: 0.6112778782844543, Word: အမေကြီး
Score: 0.5977816581726074, Word: အဖေ့
Score: 0.5932369828224182, Word: အောင်အောင်
Score: 0.5837813019752502, Word: အောင်အောင့်

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word သာဓု --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'သာဓု':
Score: 0.8327741622924805, Word: သာဓုပါ
Score: 0.7131559252738953, Word: မွန်မြတ်
Score: 0.7059281468391418, Word: လှူနိုင်
Score: 0.6986103057861328, Word: နေယံ
Score: 0.6942534446716309, Word: ကိုနေယံ
Score: 0.688531219959259, Word: ဒါနအလှူ
Score: 0.6542786955833435, Word: ဆထက်
Score: 0.645128607749939, Word: လှူနိုင်တန်းနိုင်
Score: 0.6399545669555664, Word: သုထု
Score: 0.6270649433135986, Word: မက

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word မုန့်ဟင်းခါး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'မုန့်ဟင်းခါး':
Score: 0.7990289330482483, Word: ဟင်းခါး
Score: 0.7077637314796448, Word: ကြက်ဟင်းခါး
Score: 0.6973205804824829, Word: လက်ဖက်သုပ်
Score: 0.6608697175979614, Word: သံပရာသီး
Score: 0.6341961622238159, Word: မုန့်
Score: 0.6330466866493225, Word: မုန့်ဖုတ်
Score: 0.6302824020385742, Word: ငါးဟင်း
Score: 0.628375768661499, Word: မုန့်ဟင်းခါး
Score: 0.6252753138542175, Word: ကြက်ဟင်းခါးသီး
Score: 0.6249695420265198, Word: မုန့်တီ

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word အင်တာနက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'အင်တာနက်':
Score: 0.697070837020874, Word: မြန်မာနက်
Score: 0.6930655837059021, Word: တာနကာ
Score: 0.6491116881370544, Word: ဘောနက်
Score: 0.6279654502868652, Word: အင်တာနာ
Score: 0.6255528926849365, Word: တာဝါတိုင်
Score: 0.609035849571228, Word: ကွန်ရက်လိုင်း
Score: 0.598670482635498, Word: ဖေ့စဘုတ်
Score: 0.5967662334442139, Word: မိုဘိုင်းဖုန်း
Score: 0.5892794132232666, Word: ဒေတာ
Score: 0.5861119627952576, Word: လူမှုကွန်ရက်

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ရန်ကုန် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ရန်ကုန်':
Score: 0.7396889328956604, Word: ရန်ကုန်သား
Score: 0.708025336265564, Word: မန္တလေး
Score: 0.6985551118850708, Word: ရန်ကုန်သူ
Score: 0.6839996576309204, Word: မြို့
Score: 0.6617465019226074, Word: တက္ကသိုလ်ရိပ်သာ
Score: 0.6561608910560608, Word: မင်္ဂလာဒုံ
Score: 0.6377002000808716, Word: ပန်းဘဲတန်း
Score: 0.625712513923645, Word: ချမ်းမြသာစည်
Score: 0.6229033470153809, Word: မိုးမခ
Score: 0.6081750392913818, Word: လှိုင်သာယာ

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ဆီးသွား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ဆီးသွား':
Score: 0.7424295544624329, Word: စီးသွား
Score: 0.6789516806602478, Word: ဆီးသီး
Score: 0.6463682651519775, Word: ပြီးသွား
Score: 0.6091898679733276, Word: ခရီးသွားချက်လက်မှတ်
Score: 0.6015713810920715, Word: ခရီးသွား
Score: 0.5920159816741943, Word: ချောင်းဆိုးပျောက်ဆေး
Score: 0.5881614089012146, Word: ဆီးသား
Score: 0.5750332474708557, Word: သံပရာရည်
Score: 0.5727888345718384, Word: ဝမ်းသွား
Score: 0.5692495703697205, Word: သွားနာပျောက်ဆေး

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word ဇာတ်ပို့ --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'ဇာတ်ပို့':
Score: 0.7363746762275696, Word: ဇာတ်ဆောင်
Score: 0.7230051755905151, Word: ဇာတ်ဆောင်ဆု
Score: 0.6887322664260864, Word: ဇာတ်ရှိန်
Score: 0.6832404136657715, Word: ဇာတ်ပျက်
Score: 0.6633386611938477, Word: ဇာတ်ရံ
Score: 0.6571233868598938, Word: သရုပ်ဆောင်
Score: 0.6473250985145569, Word: ဇာတ်ကြီး
Score: 0.6449819207191467, Word: ဇာတ်နာ
Score: 0.6347267627716064, Word: ဇာတ်ပေါင်း
Score: 0.6328849792480469, Word: ဇာတ်သမား

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation nearest_neighbors --word တင်္ခဏုပ္ပတ္တိဉာဏ် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Nearest neighbors for 'တင်္ခဏုပ္ပတ္တိဉာဏ်':
Score: 0.6440856456756592, Word: ဝိပ္ပတ္တိ
Score: 0.6375711560249329, Word: ကမ္မည်း
Score: 0.6332984566688538, Word: အရာထင်
Score: 0.6266775131225586, Word: စိတ်ကူးဉာဏ်
Score: 0.616396427154541, Word: ကဗျာစု
Score: 0.614463746547699, Word: ဥဿဟ
Score: 0.6117307543754578, Word: ကဗျာစာပေ
Score: 0.6089282631874084, Word: သမ္ပတ္တိ
Score: 0.6034379005432129, Word: ဉာဏ်
Score: 0.6027851104736328, Word: ဖခမည်းတော်

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy ဝက် ဝက်သား ကြက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ဝက် - ဝက်သား + ကြက်
Analogies result:
Word: တောကြက်, Score: 0.5436771512031555
Word: ဥစားကြက်, Score: 0.5163474082946777
Word: ခဘဲ, Score: 0.5094403028488159
Word: ကြက်ကလေး, Score: 0.49058791995048523
Word: ရေကြက်, Score: 0.48684030771255493
Word: အသားစားကြက်, Score: 0.4804704189300537
Word: ကြိုးကြာငှက်, Score: 0.478249728679657
Word: တိန်ညင်, Score: 0.47800424695014954
Word: ငမြှောင်တောင်, Score: 0.4747859537601471
Word: ကြက်ကြီး, Score: 0.4715502858161926

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy ဘုရင် မိဖုရား ဘုန်းကြီး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ဘုရင် - မိဖုရား + ဘုန်းကြီး
Analogies result:
Word: ဘုန်းကြီးကျောင်းသား, Score: 0.4998887777328491
Word: ဘုန်းတော်ကြီး, Score: 0.4904579818248749
Word: ကိုနီ, Score: 0.48667111992836
Word: ကိုပါကြီး, Score: 0.4843829274177551
Word: ဘုန်းတော်, Score: 0.48367300629615784
Word: ဘုန်းကြီးကျောင်းဝင်း, Score: 0.47713154554367065
Word: သံဃာ, Score: 0.46965277194976807
Word: ရခီး, Score: 0.46067744493484497
Word: အရှင်ဗုဒ္ဓဉာဏ, Score: 0.4575707018375397
Word: ဘုန်းဘုန်း, Score: 0.4531809091567993

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy အထီး အမ ယောက်ျား --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အထီး - အမ + ယောက်ျား
Analogies result:
Word: ကျွဲရိုင်း, Score: 0.5402471423149109
Word: ယောက်ျားသား, Score: 0.5387493371963501
Word: ယောက်ျားကြီး, Score: 0.5383455157279968
Word: လင်ယောက်ျား, Score: 0.5317496657371521
Word: မိန်းမ, Score: 0.5178396105766296
Word: မိမိရရ, Score: 0.4896197021007538
Word: မဆီမဆိုင်, Score: 0.47792020440101624
Word: ရန်မူ, Score: 0.4776657521724701
Word: အမျက်ထွက်, Score: 0.47466450929641724
Word: ယောက်ျားပျို, Score: 0.47288307547569275

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy ရေ ရေခွက် အရက် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: ရေ - ရေခွက် + အရက်
Analogies result:
Word: ဘီယာ, Score: 0.5928601622581482
Word: လရည်, Score: 0.5563825964927673
Word: အားပါး, Score: 0.5348815321922302
Word: ကိုရခိုင်, Score: 0.5229480862617493
Word: သောက်, Score: 0.5224330425262451
Word: ဗိုက်ပူ, Score: 0.5142745971679688
Word: တမြမြ, Score: 0.5138983726501465
Word: ဂျူးဂျူး, Score: 0.4900066554546356
Word: မွှမွှ, Score: 0.4892961084842682
Word: ကိုချမ်း, Score: 0.48911252617836

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy လက်ရှည် လက်တို ဘောင်းဘီရှည် --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: လက်ရှည် - လက်တို + ဘောင်းဘီရှည်
Analogies result:
Word: ဝတ်, Score: 0.5567076206207275
Word: ဖိုသီဖတ်သီ, Score: 0.5551380515098572
Word: အင်္ကျီ, Score: 0.5383158326148987
Word: ထိုင်မသိမ်း, Score: 0.5366981625556946
Word: ထဘီ, Score: 0.5333731174468994
Word: အဝါနု, Score: 0.5322700142860413
Word: ညအိပ်ဝတ်ရုံ, Score: 0.5307892560958862
Word: ဝတ်ဆင်, Score: 0.5197224020957947
Word: အကျီ, Score: 0.519253671169281
Word: ရေညှိရောင်, Score: 0.5191075205802917

Running command: python3 ./fasttext_lm.py test --model ./model/fasttext.5gram.30ep.model --operation word_analogies --analogy အချစ် အမုန်း အပြုံး --k 10
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Querying analogy for: အချစ် - အမုန်း + အပြုံး
Analogies result:
Word: အပြုံးရိပ်, Score: 0.5692172646522522
Word: အချစ်စစ်, Score: 0.5567272305488586
Word: ရည်းစား, Score: 0.5194999575614929
Word: စိတ်ကလေး, Score: 0.5109435319900513
Word: နှင်းဆီပန်း, Score: 0.5032280683517456
Word: နူးညံ, Score: 0.49851325154304504
Word: အချစ်ရူး, Score: 0.4959734082221985
Word: အချစ်ကလေး, Score: 0.49558645486831665
Word: အနမ်း, Score: 0.4931322932243347
Word: နှလုံးသား, Score: 0.4912441074848175

ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$
```

## Prepared a Shell Script for Testing Interactive Mode

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

## Testing interactive mode with above shell script on 197 Server

Results of testing interactively with the trained FastText LM model:  

```
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$ ./run_ftlm_interactive_test.sh
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ငြိမ်းချမ်းရေး
Vector for 'ငြိမ်းချမ်းရေး':
[ 0.09019148 -0.01960137  0.2569467   0.38976547 -0.31092373 -0.15332252
 -0.30632052 -0.21447527  0.3296599   1.0983757  -0.31802794 -0.28116792
 -0.05917757  0.08754324 -0.11376742 -0.2332934   0.03384474 -0.14380324
 -0.46496373  0.36183578 -0.30610856  0.36684886 -0.6988009   0.16636996
  0.03131565 -0.0034734  -0.04295224 -0.4501159  -0.22021197 -0.16217521
 -0.3270543  -0.13563952  0.05130111 -0.7868437  -0.5418598  -0.45402437
  0.06534928  0.05430216  0.08712118  0.5603811  -0.25525302  0.10072706
 -0.26798603 -0.14316739 -0.12512895  0.24595232  0.26982608  0.17504571
  0.3884824   0.01866618  0.14008282  0.07917123  0.33030948 -0.22486301
  0.04919017 -0.01522301 -0.38999376  0.2403936  -0.7351026  -0.0499537
  0.14640345  0.31977755  0.24091582  0.6769453   0.18631817 -0.05112279
 -0.40215665  0.2745652   0.03602925  0.39117286  0.08957123  0.4116364
  0.32594427  0.18975691  0.45594773  0.2109034   0.12114381 -0.2824832
  0.07604205 -0.28073722 -0.25546253 -0.6957502   0.06869821  0.5669182
  0.65264636  0.58202857  0.00158503  0.4985524   0.19716214 -0.17365934
 -0.32187817 -0.24929409 -0.29349452 -0.1685136  -0.05888272 -0.4737351
 -0.08975589  0.70425934  0.10582624  0.07150444]
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ငြိမ်းချမ်းရေး
Nearest neighbors for 'ငြိမ်းချမ်းရေး':
Score: 0.8256531357765198, Word: ငြိမ်းချမ်းပါ
Score: 0.7763380408287048, Word: ငြိမ်းချမ်း
Score: 0.7754710912704468, Word: ငြိမ်းငြိမ်းချမ်းချမ်း
Score: 0.7691569328308105, Word: ငြိမ်းချမ်းစွာ
Score: 0.7418473958969116, Word: ငြိမ်းချမ်းသာယာ
Score: 0.7276175022125244, Word: ဦးငြိမ်းချမ်းဖြိုး
Score: 0.6876803040504456, Word: ငြိမ်းချမ်းအောင်
Score: 0.6364005208015442, Word: အတွင်းရေး
Score: 0.6126285195350647, Word: ခင်ငြိမ်းချမ်း
Score: 0.5829322934150696, Word: ကိုငြိမ်းချမ်းစိုး
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
Entering interactive mode...
Enter word or analogy (Ctrl+D or 'quit' to exit): ခေါက်ဆွဲ ခေါက်ဆွဲကြော် ထမင်း
Querying analogy for: ခေါက်ဆွဲ - ခေါက်ဆွဲကြော် + ထမင်း
Analogies result:
Word: ထမင်းဗူး, Score: 0.6233041882514954
Word: စား, Score: 0.6202290654182434
Word: ဟင်း, Score: 0.6037296652793884
Word: ခေါက်ဆွဲပြုတ်, Score: 0.5885267853736877
Word: ထမင်းစား, Score: 0.5807790160179138
Word: ငတ်, Score: 0.5805908441543579
Word: ထမင်းနပ်, Score: 0.5801066756248474
Word: ထမင်းအိုး, Score: 0.5789756774902344
Word: ဆီကျန်ရေကျန်, Score: 0.5699730515480042
Word: ထမင်းပေါင်းအိုး, Score: 0.5618475675582886
Enter word or analogy (Ctrl+D or 'quit' to exit): အမေ သမီး အဖေ
Querying analogy for: အမေ - သမီး + အဖေ
Analogies result:
Word: အဖေ့, Score: 0.6298395991325378
Word: အောင်အောင်, Score: 0.6093142628669739
Word: အောင်အောင့်, Score: 0.5858247876167297
Word: အမေ့, Score: 0.5792707204818726
Word: အမေအမေ, Score: 0.5743736028671265
Word: အောင်အောင့်, Score: 0.5402972102165222
Word: မောင်အောင်, Score: 0.5393268465995789
Word: တစ်ထေရာတည်း, Score: 0.5258970260620117
Word: အမေက, Score: 0.5168067216873169
Word: ပက်လက်ကုလားထိုင်, Score: 0.4823192358016968
Enter word or analogy (Ctrl+D or 'quit' to exit): အရက် အမြည်း ဝိုင်
Querying analogy for: အရက် - အမြည်း + ဝိုင်
Analogies result:
Word: ဘီယာ, Score: 0.5908976197242737
Word: အရက်သေစာ, Score: 0.556129515171051
Word: ဝိုင်အနီ, Score: 0.5386541485786438
Word: ဆေးလိပ်ငွေ့, Score: 0.520714521408081
Word: သောက်, Score: 0.5195865631103516
Word: ဆေးလိပ်သောက်, Score: 0.5083991289138794
Word: အရက်ငွေ့, Score: 0.5051696300506592
Word: သောက်လာ, Score: 0.49392056465148926
Word: ဝီစကီ, Score: 0.4925500750541687
Word: အရက်သောက်, Score: 0.4839438498020172
Enter word or analogy (Ctrl+D or 'quit' to exit): နေ လ ရွှေ
Querying analogy for: နေ - လ + ရွှေ
Analogies result:
Word: လှောင်အိမ်, Score: 0.5051524639129639
Word: မေဘရဏီသော်, Score: 0.5045770406723022
Word: ရွှေရွှေ, Score: 0.5040063858032227
Word: သောက်ကျင့်ယုတ်, Score: 0.503052294254303
Word: ကိုဇွဲ, Score: 0.49939659237861633
Word: တောင့်တောင့်ကြီး, Score: 0.49819591641426086
Word: ကြောင်အိမ်, Score: 0.48471328616142273
Word: ဆယ်ဖီ, Score: 0.47906041145324707
Word: ကျားကြီး, Score: 0.47842469811439514
Word: ယျောင့်, Score: 0.4756355285644531
Enter word or analogy (Ctrl+D or 'quit' to exit): နေပူ ချွေးထွက် အေး
Querying analogy for: နေပူ - ချွေးထွက် + အေး
Analogies result:
Word: နှင်း, Score: 0.4781414568424225
Word: ငမှုန်, Score: 0.46163904666900635
Word: ဦးဂကျွန်ကြီး, Score: 0.45714619755744934
Word: ချမ်း, Score: 0.45541757345199585
Word: ခ်ခ်ခ်, Score: 0.45358458161354065
Word: အေးဆေး, Score: 0.4497550129890442
Word: ရေ, Score: 0.44852906465530396
Word: ဘာဘီ, Score: 0.4484654664993286
Word: နွယ်, Score: 0.4426880478858948
Word: မိုးသက်ဒင်, Score: 0.44257068634033203
Enter word or analogy (Ctrl+D or 'quit' to exit): quit
Exiting interactive mode...
ye@lst-gpu-server-197:~/ye/exp/lm/fasttext$
```

ကမ္ဘောဒီးယားဘက်က ဆာဗာက အရေးထဲမှာ ဒေါင်းသွားခဲ့လို့...  
python နဲ့ shell script တွေက local machine မှာ log မှတ်ထားတာလို့ တော်သေးတယ်။  
အဲဒါနဲ့ log ကနေပဲ script တွေကို ကော်ပီကူးပြီး ကမမ်းကတမ်း Lab ရဲ့ ဆာဗာနောက်တစ်လုံးမှာ ပြန် training/testing လုပ်ခဲ့ရတာ။ အဆင်ပြေတာကို ဝမ်းသာတယ်။  

## To Do

- Add more monolingual data
- Normalization on that big corpus and train/test again
- Check and send all fasttext-lm folder to Thura Aung for myNLP module



