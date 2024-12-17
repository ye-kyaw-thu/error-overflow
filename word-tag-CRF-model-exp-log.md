# Word/Tag CRF Model Exp Log

## Training Data Preparation

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data$ cp ../../dummy/*.hyp .
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data$ wc *.hyp
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
   
check ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data$ head -n 1 *.hyp
==> AdaBoost.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/O

==> CRF.train.hyp <==
နား/B လည်/N ပါ/N ပြီ/E

==> Decision-Tree.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E

==> GradientBoosting.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E

==> Logistic-Regression.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/O

==> MLP.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E

==> Random-Forest.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E

==> Voting.train.hyp <==
နား/O လည်/O ပါ/N ပြီ/E
```

replacing "/" with "_" ...    

```python
import argparse
import os
import glob

def replace_in_file(file_path, search, replace):
    """Replace occurrences of a string in a file."""
    try:
        with open(file_path, 'r', encoding='utf-8') as file:
            content = file.read()
        
        new_content = content.replace(search, replace)
        
        with open(file_path, 'w', encoding='utf-8') as file:
            file.write(new_content)
        
        print(f"Processed: {file_path}")
    except Exception as e:
        print(f"Error processing {file_path}: {e}")

def process_files(folder, extension, search, replace):
    """Find files by extension and replace content."""
    # Construct the search pattern for files
    search_pattern = os.path.join(folder, f"*.{extension}")
    
    # Use glob to find all matching files
    files = glob.glob(search_pattern)
    
    if not files:
        print(f"No files with extension '{extension}' found in folder '{folder}'.")
        return
    
    # Replace content in each file
    for file_path in files:
        replace_in_file(file_path, search, replace)

def main():
    # Set up argument parser
    parser = argparse.ArgumentParser(
        description="Search and replace text in files under a specific folder."
    )
    parser.add_argument('--search', required=True, help="String to search for")
    parser.add_argument('--replace', required=True, help="String to replace with")
    parser.add_argument('--folder', required=True, help="Folder containing the files")
    parser.add_argument('--extension', required=True, help="File extension to process")

    # Parse arguments
    args = parser.parse_args()
    
    # Validate folder
    if not os.path.isdir(args.folder):
        print(f"Error: Folder '{args.folder}' does not exist.")
        return
    
    # Process files
    process_files(args.folder, args.extension, args.search, args.replace)

if __name__ == "__main__":
    main()

```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag$ python ./batch_replace.py --help
usage: batch_replace.py [-h] --search SEARCH --replace REPLACE --folder FOLDER --extension EXTENSION

Search and replace text in files under a specific folder.

options:
  -h, --help            show this help message and exit
  --search SEARCH       String to search for
  --replace REPLACE     String to replace with
  --folder FOLDER       Folder containing the files
  --extension EXTENSION
                        File extension to process
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag$ time python batch_replace.py --search "/" --replace "_" --folder "./data" --extension "hyp"
Processed: ./data/Logistic-Regression.train.hyp
Processed: ./data/CRF.train.hyp
Processed: ./data/Random-Forest.train.hyp
Processed: ./data/Decision-Tree.train.hyp
Processed: ./data/Voting.train.hyp
Processed: ./data/GradientBoosting.train.hyp
Processed: ./data/AdaBoost.train.hyp
Processed: ./data/MLP.train.hyp

real    0m1.139s
user    0m0.691s
sys     0m0.443s
```

check file ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data$ head -n 1 *.hyp
==> AdaBoost.train.hyp <==
နား_O လည်_O ပါ_N ပြီ_O

==> CRF.train.hyp <==
နား_B လည်_N ပါ_N ပြီ_E

==> Decision-Tree.train.hyp <==
နား_O လည်_O ပါ_N ပြီ_E

==> GradientBoosting.train.hyp <==
နား_O လည်_O ပါ_N ပြီ_E

==> Logistic-Regression.train.hyp <==
နား_O လည်_O ပါ_N ပြီ_O

==> MLP.train.hyp <==
နား_O လည်_O ပါ_N ပြီ_E

==> Random-Forest.train.hyp <==
နား_O လည်_O ပါ_N ပြီ_E

==> Voting.train.hyp <==
နား_O လည်_O ပါ_N ပြီ_E
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data$ mv *.hyp ./preprocess/
```

for tagging, I can use make-pair.sh.  
 ./make-pair.sh ./models/fasttext/wordtag/data/preprocess train.hyp tag.pair ./models/fasttext/dummy/train-valid.tagged.bone.tag  
 
```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time  ./make-pair.sh ./mode
ls/fasttext/wordtag/data/preprocess train.hyp tag.pair ./models/fasttext/dummy/train-valid.tagged.bone.ta
g
Processing: ./models/fasttext/wordtag/data/preprocess/AdaBoost.train.hyp -> ./models/fasttext/wordtag/data/preprocess/AdaBoost.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/CRF.train.hyp -> ./models/fasttext/wordtag/data/preprocess/CRF.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/Decision-Tree.train.hyp -> ./models/fasttext/wordtag/data/preprocess/Decision-Tree.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/GradientBoosting.train.hyp -> ./models/fasttext/wordtag/data/preprocess/GradientBoosting.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/Logistic-Regression.train.hyp -> ./models/fasttext/wordtag/data/preprocess/Logistic-Regression.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/MLP.train.hyp -> ./models/fasttext/wordtag/data/preprocess/MLP.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/Random-Forest.train.hyp -> ./models/fasttext/wordtag/data/preprocess/Random-Forest.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/Voting.train.hyp -> ./models/fasttext/wordtag/data/preprocess/Voting.tag.pair

real    0m8.150s
user    0m7.951s
sys     0m0.184s
```

check the tagged files:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess$ head -n 1 *.tag.pair
==> AdaBoost.tag.pair <==
နား_O/B လည်_O/N ပါ_N/N ပြီ_O/E

==> CRF.tag.pair <==
နား_B/B လည်_N/N ပါ_N/N ပြီ_E/E

==> Decision-Tree.tag.pair <==
နား_O/B လည်_O/N ပါ_N/N ပြီ_E/E

==> GradientBoosting.tag.pair <==
နား_O/B လည်_O/N ပါ_N/N ပြီ_E/E

==> Logistic-Regression.tag.pair <==
နား_O/B လည်_O/N ပါ_N/N ပြီ_O/E

==> MLP.tag.pair <==
နား_O/B လည်_O/N ပါ_N/N ပြီ_E/E

==> Random-Forest.tag.pair <==
နား_O/B လည်_O/N ပါ_N/N ပြီ_E/E

==> Voting.tag.pair <==
နား_O/B လည်_O/N ပါ_N/N ပြီ_E/E
```

## Build FastText Model for word_tag dataset

training command:  

```
time python ./build-fasttext-model.py --input ./models/fasttext/wordtag/data/preprocess/CRF.train.hyp --output ./models/fasttext/wordtag/word_tag.fasttext.model.bin  
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./build-fasttext-model.py --input ./models/fasttext/wordtag/data/preprocess/CRF.train.hyp --output ./models/fasttext/wordtag/word_tag.fasttext.model.bin
2024-12-17 21:53:08,972 - Starting FastText model training with model_type=skipgram, dim=100, epoch=5, lr=0.05, ws=5...
Read 1M words
Number of words:  3920
Number of labels: 0
Progress: 100.0% words/sec/thread:   37725 lr:  0.000000 avg.loss:  2.312994 ETA:   0h 0m 0s
2024-12-17 21:53:15,926 - Saving FastText model to './models/fasttext/wordtag/word_tag.fasttext.model.bin'...
2024-12-17 21:53:16,616 - FastText model training completed successfully.

real    0m7.893s
user    3m6.753s
sys     0m3.220s
```

check filesize information:  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ll -h  ./models/fasttext/wordtag/word_tag.fasttext.model.bin
-rw-rw-r-- 1 ye ye 767M Dec 17 21:53 ./models/fasttext/wordtag/word_tag.fasttext.model.bin
```


## Training with word_tag/tag Data (2nd Model)  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data$ cp ./preprocess/*.tag.pair .
```

training data path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data  

fasttext model path: 
./models/fasttext/wordtag/word_tag.fasttext.model.bin  

model path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models  

shell command running pattern:  
$0 <training_data_path> <training_file_extension> <ft_model_path> <output_model_path>  

Running command:  
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./build-2nd-models.sh ./models/fasttext/wordtag/data/ tag.pair ./models/fasttext/wordtag/word_tag.fasttext.model.bin ./models/fasttext/wordtag/models/ | tee word_tag-model-building.log  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./build-2nd-models.sh ./models/fasttext/wordtag/data/ tag.pair ./models/fasttext/wordtag/word_tag.fasttext.model.bin ./models/fasttext/wordtag/models/ | tee word_tag-model-building.log
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//AdaBoost.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//AdaBoost.tag.model --method AdaBoost
2024-12-17 22:01:18,484 - Loading training data for AdaBoost...
2024-12-17 22:01:19,233 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-17 22:01:19,963 - Preparing features for AdaBoost...
2024-12-17 22:01:29,528 - Training AdaBoost model...
/home/ye/.local/lib/python3.10/site-packages/sklearn/ensemble/_weight_boosting.py:519: FutureWarning: The SAMME.R algorithm (the default) is deprecated and will be removed in 1.6. Use the SAMME algorithm to circumvent this warning.
  warnings.warn(
2024-12-17 22:07:29,904 - Saving trained model to ./models/fasttext/wordtag/models//AdaBoost.tag.model...
2024-12-17 22:07:29,996 - Training for AdaBoost completed.

real    6m13.173s
user    6m11.849s
sys     0m7.993s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//CRF.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//CRF.tag.model --method CRF
2024-12-17 22:07:31,404 - Loading training data for CRF...
2024-12-17 22:07:32,127 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-17 22:07:32,902 - Preparing features for CRF...
2024-12-17 22:08:42,843 - Training CRF model...
2024-12-17 22:14:17,004 - Saving trained model to ./models/fasttext/wordtag/models//CRF.tag.model...
2024-12-17 22:14:17,024 - Training for CRF completed.

real    6m55.851s
user    6m40.260s
sys     0m22.395s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//Decision-Tree.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Decision-Tree.tag.model --method Decision-Tree
2024-12-17 22:14:27,266 - Loading training data for Decision-Tree...
2024-12-17 22:14:27,994 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-17 22:14:28,731 - Preparing features for Decision-Tree...
2024-12-17 22:14:38,614 - Training Decision-Tree model...
2024-12-17 22:15:36,874 - Saving trained model to ./models/fasttext/wordtag/models//Decision-Tree.tag.model...
2024-12-17 22:15:36,878 - Training for Decision-Tree completed.

real    1m11.068s
user    1m12.652s
sys     0m5.124s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//GradientBoosting.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//GradientBoosting.tag.model --method GradientBoosting
2024-12-17 22:15:38,334 - Loading training data for GradientBoosting...
2024-12-17 22:15:39,057 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-17 22:15:39,789 - Preparing features for GradientBoosting...
2024-12-17 22:15:51,470 - Training GradientBoosting model...




2024-12-18 00:18:06,608 - Saving trained model to ./models/fasttext/wordtag/models//GradientBoosting.tag.model...
2024-12-18 00:18:06,698 - Training for GradientBoosting completed.

real    122m29.774s
user    122m19.469s
sys     0m15.795s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//Logistic-Regression.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Logistic-Regression.tag.model --method Logistic-Regression
2024-12-18 00:18:08,104 - Loading training data for Logistic-Regression...
2024-12-18 00:18:08,827 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 00:18:09,559 - Preparing features for Logistic-Regression...
2024-12-18 00:18:19,596 - Training Logistic-Regression model...
2024-12-18 00:19:14,462 - Saving trained model to ./models/fasttext/wordtag/models//Logistic-Regression.tag.model...
2024-12-18 00:19:14,465 - Training for Logistic-Regression completed.

real    1m7.858s
user    16m59.127s
sys     7m19.813s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//MLP.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//MLP.tag.model --method MLP
2024-12-18 00:19:15,963 - Loading training data for MLP...
2024-12-18 00:19:16,684 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 00:19:17,418 - Preparing features for MLP...
2024-12-18 00:19:27,234 - Training MLP model...
2024-12-18 00:34:44,468 - Saving trained model to ./models/fasttext/wordtag/models//MLP.tag.model...
2024-12-18 00:34:44,585 - Training for MLP completed.

real    15m30.030s
user    267m47.089s
sys     215m34.562s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//Random-Forest.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Random-Forest.tag.model --method Random-Forest
2024-12-18 00:34:45,996 - Loading training data for Random-Forest...
2024-12-18 00:34:46,716 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 00:34:47,450 - Preparing features for Random-Forest...
2024-12-18 00:34:58,847 - Training Random-Forest model...

2024-12-18 00:43:19,312 - Saving trained model to ./models/fasttext/wordtag/models//Random-Forest.tag.model...
2024-12-18 00:43:19,524 - Training for Random-Forest completed.

real    8m34.935s
user    8m35.139s
sys     0m6.684s
Running: time python ./fasttext-ml.version2.py --train ./models/fasttext/wordtag/data//Voting.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Voting.tag.model --method Voting
2024-12-18 00:43:20,944 - Loading training data for Voting...
2024-12-18 00:43:21,665 - Loading existing FastText model from ./models/fasttext/wordtag/word_tag.fasttext.model.bin...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 00:43:22,411 - Preparing features for Voting...
2024-12-18 00:43:32,314 - Training Voting model...


2024-12-18 00:53:11,416 - Saving trained model to ./models/fasttext/wordtag/models//Voting.tag.model...
2024-12-18 00:53:11,708 - Training for Voting completed.

real    9m52.664s
user    26m10.491s
sys     7m33.879s

real    171m55.382s
user    455m56.097s
sys     231m26.259s
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
(

```

check output model files ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models$ ll -h *.model
-rw-rw-r-- 1 ye ye  36K Dec 17 22:07 AdaBoost.tag.model
-rw-rw-r-- 1 ye ye  48K Dec 17 22:14 CRF.tag.model
-rw-rw-r-- 1 ye ye 544K Dec 17 22:15 Decision-Tree.tag.model
-rw-rw-r-- 1 ye ye 706K Dec 18 00:18 GradientBoosting.tag.model
-rw-rw-r-- 1 ye ye 4.0K Dec 18 00:19 Logistic-Regression.tag.model
-rw-rw-r-- 1 ye ye 252K Dec 18 00:34 MLP.tag.model
-rw-rw-r-- 1 ye ye  51M Dec 18 00:43 Random-Forest.tag.model
-rw-rw-r-- 1 ye ye  52M Dec 18 00:53 Voting.tag.model
```

## Preparing word_tag Test Data  
 
အရင်ဆုံး baseline model နဲ့ ရထားတဲ့ model output hyp ဖိုင်တွေကို ကော်ပီကူး။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data$ cp ~/data/hello-sayarwon/coding/model-based/models/fasttext/*.hyp .
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data$ wc *.hyp
    5512   143788  1714263 AdaBoost.hyp
    5512   143788  1714263 CRF.hyp
    5512   143788  1714263 Decision-Tree.hyp
    5512   143788  1714263 GradientBoosting.hyp
    5512   143788  1714263 Logistic-Regression.hyp
    5512   143788  1714263 MLP.hyp
    5512   143788  1714263 Random-Forest.hyp
    5512   143788  1714263 Voting.hyp
   44096  1150304 13714104 total
```

format ပြောင်းခဲ့ (syl/tag to syl_tag)  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag$ python ./batch_replace.py --search "/" --replace "_" --folder /home/ye/data/hello-sayarwon/coding/model-based/model
s/fasttext/wordtag/data/preprocess/test-data/ --extension hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/Random-Forest.hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/MLP.hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/GradientBoosting.hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/Decision-Tree.hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/Logistic-Regression.hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/Voting.hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/CRF.hyp
Processed: /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/AdaBoost.hyp
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag$
```

format ပြောင်းပြီး ထွက်လာတဲ့ဖိုင်တွေကို confirm လုပ်ခဲ့...  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data$ head -n 1 *.hyp
==> AdaBoost.hyp <==
ရင်_O ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_O ပါ_N

==> CRF.hyp <==
ရင်_B ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_N ပါ_E

==> Decision-Tree.hyp <==
ရင်_O ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_O ပါ_N

==> GradientBoosting.hyp <==
ရင်_O ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_O ပါ_N

==> Logistic-Regression.hyp <==
ရင်_O ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_O ပါ_N

==> MLP.hyp <==
ရင်_O ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_O ပါ_N

==> Random-Forest.hyp <==
ရင်_O ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_O ပါ_N

==> Voting.hyp <==
ရင်_O ဘတ်_O အောင့်_O လာ_O ရင်_O သ_O တိ_O ထား_O ပါ_N
```

 ./make-pair.sh ./models/fasttext/wordtag/data/preprocess/test-data  hyp tag.pair /home/ye/data/hello-sayarwon/coding/model-based/data/syl/bone/test.tagged.bone.tag    
 
```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ ./make-pair.sh ./models/fasttext/w
ordtag/data/preprocess/test-data  hyp tag.pair /home/ye/data/hello-sayarwon/coding/model-based/data/syl/b
one/test.tagged.bone.tag
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/AdaBoost.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/AdaBoost.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/CRF.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/CRF.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/Decision-Tree.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/Decision-Tree.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/GradientBoosting.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/GradientBoosting.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/Logistic-Regression.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/Logistic-Regression.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/MLP.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/MLP.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/Random-Forest.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/Random-Forest.tag.pair
Processing: ./models/fasttext/wordtag/data/preprocess/test-data/Voting.hyp -> ./models/fasttext/wordtag/data/preprocess/test-data/Voting.tag.pair
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$
```

format ပြောင်းပြီး testing လုပ်ဖို့ အဆင်သင့်ဖြစ်သွားတဲ့ syl_tag/tag ဖိုင်တွေကို ဝင်ကြည့်ခဲ့...  
ဒီနေရာမှာ syl က input, "_tag" က baseline model ရဲ့ predicted output.   
"/tag" က reference tag ပါ။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data$ ll -h ./*.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./AdaBoost.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./CRF.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./Decision-Tree.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./GradientBoosting.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./Logistic-Regression.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./MLP.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./Random-Forest.tag.pair
-rw-rw-r-- 1 ye ye 2.0M Dec 18 00:13 ./Voting.tag.pair
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data$ wc *.tag.pair
    5512   143788  2001809 AdaBoost.tag.pair
    5512   143788  2001809 CRF.tag.pair
    5512   143788  2001809 Decision-Tree.tag.pair
    5512   143788  2001809 GradientBoosting.tag.pair
    5512   143788  2001809 Logistic-Regression.tag.pair
    5512   143788  2001809 MLP.tag.pair
    5512   143788  2001809 Random-Forest.tag.pair
    5512   143788  2001809 Voting.tag.pair
   44096  1150304 16014472 total
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data$ head -n 1 *.tag.pair
==> AdaBoost.tag.pair <==
ရင်_O/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_O/N ပါ_N/E

==> CRF.tag.pair <==
ရင်_B/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_N/N ပါ_E/E

==> Decision-Tree.tag.pair <==
ရင်_O/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_O/N ပါ_N/E

==> GradientBoosting.tag.pair <==
ရင်_O/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_O/N ပါ_N/E

==> Logistic-Regression.tag.pair <==
ရင်_O/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_O/N ပါ_N/E

==> MLP.tag.pair <==
ရင်_O/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_O/N ပါ_N/E

==> Random-Forest.tag.pair <==
ရင်_O/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_O/N ပါ_N/E

==> Voting.tag.pair <==
ရင်_O/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/N တိ_O/N ထား_O/N ပါ_N/E
```

preprocessing ကနေ test/ ဖိုလ်ဒါအောက်ကို ကော်ပီကူးယူထည့်...  
တနည်းအားဖြင့် backup လုပ်ခဲ့တာပါပဲ။  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test$ cp /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/preprocess/test-data/*.tag.pair .
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test$ wc *
    5512   143788  2001809 AdaBoost.tag.pair
    5512   143788  2001809 CRF.tag.pair
    5512   143788  2001809 Decision-Tree.tag.pair
    5512   143788  2001809 GradientBoosting.tag.pair
    5512   143788  2001809 Logistic-Regression.tag.pair
    5512   143788  2001809 MLP.tag.pair
    5512   143788  2001809 Random-Forest.tag.pair
    5512   143788  2001809 Voting.tag.pair
   44096  1150304 16014472 total
```
   
test data ပြင်တာ ပြီးသွားပြီ။  

## Testing with 2nd Model or word_tag/tag Format  

အရင်ဆုံး CRF model နဲ့ပဲ testing လုပ်ကြည့်မယ်။  

test data path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test    

word_tag fasttext model path:  
./models/fasttext/wordtag/word_tag.fasttext.model.bin  

2nd model path:  
/home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models  


```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test/CRF.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models/CRF.tag.model --method CRF --output ./models/fasttext/wordtag/models/CRF.hyp
2024-12-18 00:27:18,448 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 00:27:19,994 - Preparing features for CRF testing...
2024-12-18 00:27:49,563 - Saving predictions to ./models/fasttext/wordtag/models/CRF.hyp...
2024-12-18 00:27:49,691 - Predictions saved successfully.
2024-12-18 00:27:49,709 - Calculating custom evaluation metrics...
2024-12-18 00:27:49,876 - Displaying evaluation results...

Tag-wise Metrics:
B: Precision: 0.9842, Recall: 0.8630, F1-Score: 0.9196
E: Precision: 0.9830, Recall: 0.8648, F1-Score: 0.9202
N: Precision: 0.9259, Recall: 0.5070, F1-Score: 0.6552
O: Precision: 0.9053, Recall: 0.9921, F1-Score: 0.9467

Overall Accuracy: 0.9134

Overall F1-Score: 0.8604
2024-12-18 00:27:49,877 - Displaying confusion matrix...

Confusion Matrix:
        B       E       N       O
B       5921    7       29      904
E       12      5906    18      893
N       28      37      10002   9661
O       55      58      754     109488

real    0m34.406s
user    0m30.859s
sys     0m5.385s
```

CRF or Baseline result: 
 
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

Baseline နဲ့ နှိုင်းယှဉ်ရင် confusion matrix ကနေပဲ ကြည့်ကြည့် B, E, N, O အကုန် ရလဒ်က တက်လာတယ်။ 
Overall Accuracy:  0.9072 ===> 0.9134
Overall F1 Score:  0.8480 ===> 0.8604  

တိုးတက်မှုတော့ ရှိလာတယ်။  

## Testing with All 2nd Models  

./run_tests.sh --test-dir <test_files_dir> --model-dir <models_dir> --output-dir <output_dir> --ft-model <fasttext_model>  

Note: run-test-with-err-models.sh နဲ့ run-test-with-wordtag-models.sh ဖိုင် နှစ်ခု အတူတူပါပဲ။ လိုရင်ပြင်ဖို့ copy လိုက်တာ ...  

```
time ./run-test-with-wordtag-models.sh --test-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test/ --model-dir ./models/fasttext/wordtag/models/ --output-dir ./models/fasttext/wordtag/models/ --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin | tee testing_with_wordtagtag_2nd_model.log  

```

CRF မော်ဒယ်မှာထက် တခြား မော်ဒယ်တွေမှာ baseline နဲ့ နှိုင်းယှဉ်ရင် tagging လုပ်တာ ပိုကောင်းလာနိုင်မယ်လို့ ခန့်မှန်းတယ်။  
Let's see ...  

```
(hs-fasttext) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based$ time ./run-test-with-wordtag-models.sh --test-dir /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test/ --model-dir ./models/fasttext/wordtag/models/ --output-dir ./models/fasttext/wordtag/models/ --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin | tee testing_with_wordtagtag_2nd_model.log
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//AdaBoost.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//AdaBoost.tag.model --method AdaBoost --output ./models/fasttext/wordtag/models//AdaBoost.hyp
2024-12-18 01:35:44,080 - Testing AdaBoost model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:35:44,911 - Preparing features for AdaBoost testing...
2024-12-18 01:35:47,087 - Saving predictions to ./models/fasttext/wordtag/models//AdaBoost.hyp...
2024-12-18 01:35:47,197 - Predictions saved successfully.
2024-12-18 01:35:47,241 - Calculating custom evaluation metrics...
2024-12-18 01:35:47,306 - Displaying evaluation results...
2024-12-18 01:35:47,306 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.5270, Recall: 0.0526, F1-Score: 0.0957
E: Precision: 0.6815, Recall: 0.7437, F1-Score: 0.7112
N: Precision: 0.5094, Recall: 0.0944, F1-Score: 0.1593
O: Precision: 0.8106, Recall: 0.9694, F1-Score: 0.8829

Overall Accuracy: 0.7949

Overall F1-Score: 0.4623

Confusion Matrix:
        B       E       N       O
B       361     36      37      6427
E       0       5079    647     1103
N       17      376     1863    17472
O       307     1962    1110    106976

real    0m4.140s
user    0m6.721s
sys     0m4.250s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//CRF.tag.pair .tag.pair
+ BASE_NAME=CRF
+ MODEL_FILE=./models/fasttext/wordtag/models//CRF.tag.model
+ METHOD=CRF
+ OUTPUT_FILE=./models/fasttext/wordtag/models//CRF.hyp
+ [[ ! -f ./models/fasttext/wordtag/models//CRF.tag.model ]]
+ set -x
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//CRF.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//CRF.tag.model --method CRF --output ./models/fasttext/wordtag/models//CRF.hyp
2024-12-18 01:35:48,226 - Testing CRF model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:35:49,046 - Preparing features for CRF testing...
2024-12-18 01:36:02,548 - Saving predictions to ./models/fasttext/wordtag/models//CRF.hyp...
2024-12-18 01:36:02,602 - Predictions saved successfully.
2024-12-18 01:36:02,610 - Calculating custom evaluation metrics...
2024-12-18 01:36:02,668 - Displaying evaluation results...
2024-12-18 01:36:02,668 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.9842, Recall: 0.8630, F1-Score: 0.9196
E: Precision: 0.9830, Recall: 0.8648, F1-Score: 0.9202
N: Precision: 0.9259, Recall: 0.5070, F1-Score: 0.6552
O: Precision: 0.9053, Recall: 0.9921, F1-Score: 0.9467

Overall Accuracy: 0.9134

Overall F1-Score: 0.8604

Confusion Matrix:
        B       E       N       O
B       5921    7       29      904
E       12      5906    18      893
N       28      37      10002   9661
O       55      58      754     109488

real    0m16.148s
user    0m16.904s
sys     0m6.126s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Decision-Tree.tag.pair .tag.pair
+ BASE_NAME=Decision-Tree
+ MODEL_FILE=./models/fasttext/wordtag/models//Decision-Tree.tag.model
+ METHOD=Decision-Tree
+ OUTPUT_FILE=./models/fasttext/wordtag/models//Decision-Tree.hyp
+ [[ ! -f ./models/fasttext/wordtag/models//Decision-Tree.tag.model ]]
+ set -x
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Decision-Tree.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Decision-Tree.tag.model --method Decision-Tree --output ./models/fasttext/wordtag/models//Decision-Tree.hyp
2024-12-18 01:36:04,375 - Testing Decision-Tree model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:36:05,189 - Preparing features for Decision-Tree testing...
2024-12-18 01:36:06,367 - Saving predictions to ./models/fasttext/wordtag/models//Decision-Tree.hyp...
2024-12-18 01:36:06,471 - Predictions saved successfully.
2024-12-18 01:36:06,516 - Calculating custom evaluation metrics...
2024-12-18 01:36:06,581 - Displaying evaluation results...
2024-12-18 01:36:06,581 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.5595, Recall: 0.1883, F1-Score: 0.2818
E: Precision: 0.7089, Recall: 0.7720, F1-Score: 0.7391
N: Precision: 0.6030, Recall: 0.1841, F1-Score: 0.2820
O: Precision: 0.8263, Recall: 0.9584, F1-Score: 0.8874

Overall Accuracy: 0.8066

Overall F1-Score: 0.5476

Confusion Matrix:
        B       E       N       O
B       1292    22      27      5520
E       3       5272    513     1041
N       71      348     3631    15678
O       943     1795    1851    105766

real    0m3.122s
user    0m5.463s
sys     0m4.592s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//GradientBoosting.tag.pair .tag.pair
+ BASE_NAME=GradientBoosting
+ MODEL_FILE=./models/fasttext/wordtag/models//GradientBoosting.tag.model
+ METHOD=GradientBoosting
+ OUTPUT_FILE=./models/fasttext/wordtag/models//GradientBoosting.hyp
+ [[ ! -f ./models/fasttext/wordtag/models//GradientBoosting.tag.model ]]
+ set -x
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//GradientBoosting.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//GradientBoosting.tag.model --method GradientBoosting --output ./models/fasttext/wordtag/models//GradientBoosting.hyp
2024-12-18 01:36:07,499 - Testing GradientBoosting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:36:08,333 - Preparing features for GradientBoosting testing...
2024-12-18 01:36:11,402 - Saving predictions to ./models/fasttext/wordtag/models//GradientBoosting.hyp...
2024-12-18 01:36:11,518 - Predictions saved successfully.
2024-12-18 01:36:11,563 - Calculating custom evaluation metrics...
2024-12-18 01:36:11,628 - Displaying evaluation results...
2024-12-18 01:36:11,628 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.5670, Recall: 0.1697, F1-Score: 0.2612
E: Precision: 0.7082, Recall: 0.7689, F1-Score: 0.7373
N: Precision: 0.6211, Recall: 0.1636, F1-Score: 0.2589
O: Precision: 0.8233, Recall: 0.9632, F1-Score: 0.8877

Overall Accuracy: 0.8063

Overall F1-Score: 0.5363

Confusion Matrix:
        B       E       N       O
B       1164    20      21      5656
E       1       5251    507     1070
N       60      347     3227    16094
O       828     1797    1441    106289

real    0m5.075s
user    0m7.652s
sys     0m4.351s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Logistic-Regression.tag.pair .tag.pair
+ BASE_NAME=Logistic-Regression
+ MODEL_FILE=./models/fasttext/wordtag/models//Logistic-Regression.tag.model
+ METHOD=Logistic-Regression
+ OUTPUT_FILE=./models/fasttext/wordtag/models//Logistic-Regression.hyp
+ [[ ! -f ./models/fasttext/wordtag/models//Logistic-Regression.tag.model ]]
+ set -x
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Logistic-Regression.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Logistic-Regression.tag.model --method Logistic-Regression --output ./models/fasttext/wordtag/models//Logistic-Regression.hyp
2024-12-18 01:36:12,584 - Testing Logistic-Regression model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:36:13,407 - Preparing features for Logistic-Regression testing...
2024-12-18 01:36:14,642 - Saving predictions to ./models/fasttext/wordtag/models//Logistic-Regression.hyp...
2024-12-18 01:36:14,817 - Predictions saved successfully.
2024-12-18 01:36:14,862 - Calculating custom evaluation metrics...
2024-12-18 01:36:14,932 - Displaying evaluation results...
2024-12-18 01:36:14,932 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.5389, Recall: 0.0515, F1-Score: 0.0939
E: Precision: 0.7096, Recall: 0.7462, F1-Score: 0.7274
N: Precision: 0.5878, Recall: 0.1242, F1-Score: 0.2051
O: Precision: 0.8134, Recall: 0.9712, F1-Score: 0.8854

Overall Accuracy: 0.8004

Overall F1-Score: 0.4779

Confusion Matrix:
        B       E       N       O
B       353     17      20      6471
E       43      5096    504     1186
N       8       341     2450    16929
O       251     1728    1194    107182

real    0m3.293s
user    0m7.817s
sys     0m6.357s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//MLP.tag.pair .tag.pair
+ BASE_NAME=MLP
+ MODEL_FILE=./models/fasttext/wordtag/models//MLP.tag.model
+ METHOD=MLP
+ OUTPUT_FILE=./models/fasttext/wordtag/models//MLP.hyp
+ [[ ! -f ./models/fasttext/wordtag/models//MLP.tag.model ]]
+ set -x
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//MLP.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//MLP.tag.model --method MLP --output ./models/fasttext/wordtag/models//MLP.hyp
2024-12-18 01:36:15,870 - Testing MLP model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:36:16,687 - Preparing features for MLP testing...
2024-12-18 01:36:20,185 - Saving predictions to ./models/fasttext/wordtag/models//MLP.hyp...
2024-12-18 01:36:20,329 - Predictions saved successfully.
2024-12-18 01:36:20,373 - Calculating custom evaluation metrics...
2024-12-18 01:36:20,438 - Displaying evaluation results...
2024-12-18 01:36:20,439 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.5938, Recall: 0.1440, F1-Score: 0.2318
E: Precision: 0.7092, Recall: 0.7704, F1-Score: 0.7385
N: Precision: 0.6058, Recall: 0.1835, F1-Score: 0.2817
O: Precision: 0.8243, Recall: 0.9614, F1-Score: 0.8876

Overall Accuracy: 0.8066

Overall F1-Score: 0.5349

Confusion Matrix:
        B       E       N       O
B       988     19      24      5830
E       2       5261    513     1053
N       25      347     3621    15735
O       649     1791    1819    106096

real    0m5.496s
user    0m39.734s
sys     0m25.852s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Random-Forest.tag.pair .tag.pair
+ BASE_NAME=Random-Forest
+ MODEL_FILE=./models/fasttext/wordtag/models//Random-Forest.tag.model
+ METHOD=Random-Forest
+ OUTPUT_FILE=./models/fasttext/wordtag/models//Random-Forest.hyp
+ [[ ! -f ./models/fasttext/wordtag/models//Random-Forest.tag.model ]]
+ set -x
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Random-Forest.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Random-Forest.tag.model --method Random-Forest --output ./models/fasttext/wordtag/models//Random-Forest.hyp
2024-12-18 01:36:21,367 - Testing Random-Forest model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:36:22,303 - Preparing features for Random-Forest testing...
2024-12-18 01:36:25,784 - Saving predictions to ./models/fasttext/wordtag/models//Random-Forest.hyp...
2024-12-18 01:36:25,896 - Predictions saved successfully.
2024-12-18 01:36:25,940 - Calculating custom evaluation metrics...
2024-12-18 01:36:26,013 - Displaying evaluation results...
2024-12-18 01:36:26,013 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.5681, Recall: 0.1867, F1-Score: 0.2810
E: Precision: 0.7092, Recall: 0.7720, F1-Score: 0.7393
N: Precision: 0.6079, Recall: 0.1808, F1-Score: 0.2787
O: Precision: 0.8259, Recall: 0.9596, F1-Score: 0.8877

Overall Accuracy: 0.8069

Overall F1-Score: 0.5467

Confusion Matrix:
        B       E       N       O
B       1281    22      23      5535
E       3       5272    513     1041
N       67      348     3567    15746
O       904     1792    1765    105894

real    0m5.592s
user    0m8.016s
sys     0m4.504s
+ for TEST_FILE in "$TEST_DIR"/*.tag.pair
++ basename /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Voting.tag.pair .tag.pair
+ BASE_NAME=Voting
+ MODEL_FILE=./models/fasttext/wordtag/models//Voting.tag.model
+ METHOD=Voting
+ OUTPUT_FILE=./models/fasttext/wordtag/models//Voting.hyp
+ [[ ! -f ./models/fasttext/wordtag/models//Voting.tag.model ]]
+ set -x
+ python ./fasttext-ml.version3.py --test /home/ye/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/data/test//Voting.tag.pair --ft-model ./models/fasttext/wordtag/word_tag.fasttext.model.bin --model ./models/fasttext/wordtag/models//Voting.tag.model --method Voting --output ./models/fasttext/wordtag/models//Voting.hyp
2024-12-18 01:36:26,959 - Testing Voting model...
Warning : `load_model` does not return WordVectorModel or SupervisedModel any more, but a `FastText` object which is very similar.
2024-12-18 01:36:27,894 - Preparing features for Voting testing...
2024-12-18 01:36:32,450 - Saving predictions to ./models/fasttext/wordtag/models//Voting.hyp...
2024-12-18 01:36:32,561 - Predictions saved successfully.
2024-12-18 01:36:32,606 - Calculating custom evaluation metrics...
2024-12-18 01:36:32,675 - Displaying evaluation results...
2024-12-18 01:36:32,675 - Displaying confusion matrix...

Tag-wise Metrics:
B: Precision: 0.5676, Recall: 0.1866, F1-Score: 0.2808
E: Precision: 0.7092, Recall: 0.7720, F1-Score: 0.7393
N: Precision: 0.6048, Recall: 0.1840, F1-Score: 0.2821
O: Precision: 0.8262, Recall: 0.9590, F1-Score: 0.8876

Overall Accuracy: 0.8069

Overall F1-Score: 0.5475

Confusion Matrix:
        B       E       N       O
B       1280    22      24      5535
E       3       5272    513     1041
N       68      348     3629    15683
O       904     1792    1834    105825

real    0m6.640s
user    0m11.157s
sys     0m6.383s
+ set +x

real    0m49.523s
user    1m43.474s
sys     1m2.427s
```

## Error Analysis  

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models$ head MLP.hyp
ရင်_O/O ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/O တိ_O/O ထား_O/O ပါ_N/N
ဘယ်_O/O လောက်_O/O နောက်_O/O ကျ_O/O သ_O/O လဲ_E/E
ကြို_O/O ပို့_O/O ဘတ်စ်_O/O ကား_O/O က_O/O အ_O/O ဆင်_O/O အ_O/O ပြေ_N/O ဆုံး_O/O ပဲ_O/O
အဲ_B/B ဒီ_O/O အ_O/O ဖွဲ့_O/O ရဲ့_O/O ဥက္ကဋ္ဌ_O/O ဖြစ်_O/O တဲ့_O/O ယို_O/O ကို_O/O ယာ_O/O မာ့_O/O အာ_O/O ကိ_O/O ဟီ_O/O တို_O/O YokoyamaAkihito_O/O က_O/O တ_O/O ခြား_O/O နိုင်_O/O ငံ_O/O တွေ_O/O မှာ_O/O ဖြစ်_O/O ပွား_O/O တဲ့_O/O လူ_O/O နာ_O/O တွေ_O/O ရဲ့_O/O အ_O/O ဆုတ်_O/O လုပ်_O/O ဆောင်_O/O ပုံ_O/O တွေ_O/O က_O/O ဗိုင်း_O/O ရပ်စ်_O/O ကူး_O/O စက်_O/O ခံ_O/O ရ_O/O ပြီး_O/O ကု_O/O သ_O/O လိုက်_N/N လို့_O/O ရော_O/O ဂါ_O/O ပိုး_O/O မ_O/O ရှိ_O/O တော့_O/O ဘူး_E/E လို့_O/O စစ်_O/O ဆေး_O/O ပြီး_O/O နောက်_O/O မှာ_O/O တောင်_O/O မှ_O/O အ_O/O ဆုတ်_O/O က_O/O အ_O/O ပြည့်_O/O အ_O/O ဝ_O/O ပုံ_O/O မှန်_O/O ပြန်_O/O ဖြစ်_O/O မ_O/O လာ_O/O တဲ့_O/O လူ_O/O နာ_O/O တွေ_O/O အ_O/O များ_O/O အ_O/O ပြား_O/O တွေ့_O/O ရ_O/O တယ်_E/E လို့_O/O ပြော_N/N ပါ_N/N တယ်_E/E
အ_O/O ဆင့်_O/O အေ_O/O ဝင်_O/O ငွေ_O/O ခွန်_O/O ကို_O/O လ_O/O စာ_O/O မှ_O/O ဖြတ်_O/O တောက်_O/O သည်_E/E
လို_O/O ကီ_O/O က_O/O အတ်_O/O ဂါ_O/O ဒါ_B/B လို_O/O ကီ_O/O ရဲ့_O/O မျက်_O/O လုံး_O/O တွေ_O/O ကို_O/O သေ_O/O ချာ_O/O တည့်_O/O တည့်_O/O ကြည့်_O/O ရင်း_O/O ငါ_O/O က_O/O လို_O/O ကီ_O/O
ခင်_B/O ဗျား_O/O ကြိုက်_N/N တဲ့_O/O အ_O/O ရောင်_O/O က_O/O ဘာ_O/O လဲ_E/E
သူ_O/O သီ_O/O ချင်း_O/O ဆို_O/O တတ်_O/O သ_O/O လို_O/O က_O/O လည်း_O/O က_O/O တတ်_O/O သည်_E/E
ထို့_B/B ကြောင့်_O/O ဥ_O/O ပါယ်_O/O ဂို့_O/O ဟု_O/O ခေါ်_O/O ကာ_O/O ကာ_O/O လ_O/O ကြာ_O/O သော်_O/O ဥ_O/O ပါယ်_O/O ဂို့_O/O မှ_O/O ပ_O/O ဂိုး_O/O ဟု_O/O ပြောင်း_O/O လဲ_E/E ခေါ်_O/O လာ_O/O ကြ_N/N သည်_E/E
ဒီ_O/O နေ့_O/O ခင်_B/O ဗျား_O/O ဘယ်_O/O လို_O/O ဖြစ်_O/O နေ_O/O တာ_O/O လဲ_E/E
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models$ head Random-Forest.hyp
ရင်_O/O ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/O တိ_O/O ထား_O/O ပါ_N/N
ဘယ်_O/O လောက်_O/O နောက်_O/O ကျ_O/O သ_O/O လဲ_E/E
ကြို_O/O ပို့_O/O ဘတ်စ်_O/O ကား_O/O က_O/O အ_O/O ဆင်_O/O အ_O/O ပြေ_O/O ဆုံး_O/O ပဲ_O/O
အဲ_B/B ဒီ_O/O အ_O/O ဖွဲ့_O/O ရဲ့_O/O ဥက္ကဋ္ဌ_O/O ဖြစ်_O/O တဲ့_O/O ယို_O/O ကို_O/O ယာ_O/O မာ့_O/O အာ_O/O ကိ_O/O ဟီ_O/O တို_O/O YokoyamaAkihito_O/O က_O/O တ_O/O ခြား_O/O နိုင်_O/O ငံ_O/O တွေ_O/O မှာ_O/O ဖြစ်_O/O ပွား_O/O တဲ့_O/O လူ_O/O နာ_O/O တွေ_O/O ရဲ့_O/O အ_O/O ဆုတ်_O/O လုပ်_O/O ဆောင်_O/O ပုံ_O/O တွေ_O/O က_O/O ဗိုင်း_O/O ရပ်စ်_O/O ကူး_O/O စက်_O/O ခံ_O/O ရ_O/O ပြီး_O/O ကု_O/O သ_O/O လိုက်_N/N လို့_O/O ရော_O/O ဂါ_O/O ပိုး_O/O မ_O/O ရှိ_O/O တော့_O/O ဘူး_E/E လို့_O/O စစ်_O/O ဆေး_O/O ပြီး_O/O နောက်_O/O မှာ_O/O တောင်_O/O မှ_O/O အ_O/O ဆုတ်_O/O က_O/O အ_O/O ပြည့်_O/O အ_O/O ဝ_O/O ပုံ_O/O မှန်_O/O ပြန်_O/O ဖြစ်_O/O မ_O/O လာ_O/O တဲ့_O/O လူ_O/O နာ_O/O တွေ_O/O အ_O/O များ_O/O အ_O/O ပြား_O/O တွေ့_O/O ရ_O/O တယ်_E/E လို့_O/O ပြော_N/N ပါ_N/N တယ်_E/E
အ_O/O ဆင့်_O/O အေ_O/O ဝင်_O/O ငွေ_O/O ခွန်_O/O ကို_O/O လ_O/O စာ_O/O မှ_O/O ဖြတ်_O/O တောက်_O/O သည်_E/E
လို_O/O ကီ_O/O က_O/O အတ်_O/O ဂါ_O/O ဒါ_B/B လို_O/O ကီ_O/O ရဲ့_O/O မျက်_O/O လုံး_O/O တွေ_O/O ကို_O/O သေ_O/O ချာ_O/O တည့်_O/O တည့်_O/O ကြည့်_O/O ရင်း_O/O ငါ_O/O က_O/O လို_O/O ကီ_O/O
ခင်_B/B ဗျား_O/O ကြိုက်_N/N တဲ့_O/O အ_O/O ရောင်_O/O က_O/O ဘာ_O/O လဲ_E/E
သူ_O/O သီ_O/O ချင်း_O/O ဆို_O/O တတ်_O/O သ_O/O လို_O/O က_O/O လည်း_O/O က_O/O တတ်_O/O သည်_E/E
ထို့_B/B ကြောင့်_O/O ဥ_O/O ပါယ်_O/O ဂို့_O/O ဟု_O/O ခေါ်_O/O ကာ_O/O ကာ_O/O လ_O/O ကြာ_O/O သော်_O/O ဥ_O/O ပါယ်_O/O ဂို့_O/O မှ_O/O ပ_O/O ဂိုး_O/O ဟု_O/O ပြောင်း_O/O လဲ_E/E ခေါ်_O/O လာ_O/O ကြ_N/N သည်_E/E
ဒီ_O/O နေ့_O/O ခင်_B/B ဗျား_O/O ဘယ်_O/O လို_O/O ဖြစ်_O/O နေ_O/O တာ_O/O လဲ_E/E
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models$ head CRF.hyp
ရင်_B/B ဘတ်_O/O အောင့်_O/O လာ_O/O ရင်_O/O သ_O/O တိ_O/O ထား_N/N ပါ_E/E
ဘယ်_B/B လောက်_N/N နောက်_N/N ကျ_N/N သ_N/N လဲ_E/E
ကြို_B/B ပို့_O/O ဘတ်စ်_O/O ကား_O/O က_O/O အ_O/O ဆင်_O/O အ_O/O ပြေ_N/N ဆုံး_N/N ပဲ_E/E
အဲ_B/B ဒီ_O/O အ_O/O ဖွဲ့_O/O ရဲ့_O/O ဥက္ကဋ္ဌ_O/O ဖြစ်_O/O တဲ့_O/O ယို_O/O ကို_O/O ယာ_O/O မာ့_O/O အာ_O/O ကိ_O/O ဟီ_O/O တို_O/O YokoyamaAkihito_O/O က_O/O တ_O/O ခြား_O/O နိုင်_O/O ငံ_O/O တွေ_O/O မှာ_O/O ဖြစ်_O/O ပွား_O/O တဲ့_O/O လူ_O/O နာ_O/O တွေ_O/O ရဲ့_O/O အ_O/O ဆုတ်_O/O လုပ်_O/O ဆောင်_O/O ပုံ_O/O တွေ_O/O က_O/O ဗိုင်း_O/O ရပ်စ်_O/O ကူး_O/O စက်_O/O ခံ_O/O ရ_O/O ပြီး_O/O ကု_O/O သ_O/O လိုက်_O/O လို့_O/O ရော_O/O ဂါ_O/O ပိုး_O/O မ_O/O ရှိ_O/O တော့_O/O ဘူး_O/O လို့_O/O စစ်_O/O ဆေး_O/O ပြီး_O/O နောက်_O/O မှာ_O/O တောင်_O/O မှ_O/O အ_O/O ဆုတ်_O/O က_O/O အ_O/O ပြည့်_O/O အ_O/O ဝ_O/O ပုံ_O/O မှန်_O/O ပြန်_O/O ဖြစ်_O/O မ_O/O လာ_O/O တဲ့_O/O လူ_O/O နာ_O/O တွေ_O/O အ_O/O များ_O/O အ_O/O ပြား_O/O တွေ့_O/O ရ_O/O တယ်_O/O လို့_O/O ပြော_N/N ပါ_N/N တယ်_E/E
အ_B/B ဆင့်_O/O အေ_O/O ဝင်_O/O ငွေ_O/O ခွန်_O/O ကို_O/O လ_O/O စာ_O/O မှ_O/O ဖြတ်_N/N တောက်_N/N သည်_E/E
လို_B/B ကီ_O/O က_O/O အတ်_O/O ဂါ_O/O ဒါ_O/O လို_O/O ကီ_O/O ရဲ့_O/O မျက်_O/O လုံး_O/O တွေ_O/O ကို_O/O သေ_O/O ချာ_O/O တည့်_O/O တည့်_O/O ကြည့်_O/O ရင်း_O/O ငါ_O/O က_O/O လို_N/N ကီ_E/E
ခင်_B/B ဗျား_O/O ကြိုက်_O/O တဲ့_O/O အ_O/O ရောင်_O/O က_O/O ဘာ_N/N လဲ_E/E
သူ_B/B သီ_O/O ချင်း_O/O ဆို_O/O တတ်_O/O သ_O/O လို_O/O က_O/O လည်း_O/O က_O/O တတ်_N/N သည်_E/E
ထို့_B/B ကြောင့်_O/O ဥ_O/O ပါယ်_O/O ဂို့_O/O ဟု_O/O ခေါ်_O/O ကာ_O/O ကာ_O/O လ_O/O ကြာ_O/O သော်_O/O ဥ_O/O ပါယ်_O/O ဂို့_O/O မှ_O/O ပ_O/O ဂိုး_O/O ဟု_N/N ပြောင်း_N/N လဲ_N/N ခေါ်_N/N လာ_N/N ကြ_N/N သည်_E/E
ဒီ_B/B နေ့_O/O ခင်_O/O ဗျား_O/O ဘယ်_O/O လို_N/N ဖြစ်_N/N နေ_N/N တာ_N/N လဲ_E/E
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models$ tail CRF.hyp
အိမ်_B/B မှာ_O/O ဆ_O/O ရာ_O/O မ_O/O ကြီး_O/O အိမ်_O/O က_O/O ဝယ်_O/O ထား_O/O တာ_O/O ဘာ_O/O ရှိ_N/N လဲ_E/E
ကျွန်_B/B တော့်_O/O အ_O/O တွက်_O/O နည်း_O/O နည်း_O/O ကျပ်_N/N တယ်_E/E
စား_B/B သောက်_O/O ဆိုင်_O/O မှာ_O/O လုပ်_O/O တာ_N/N ပါ_E/E
ဆွဲ_B/B ဆွဲ_O/O ငင်_O/O ငင်_O/O အော်_O/O ကာ_O/O ဖြတ်_O/O သွား_O/O သော_O/O ကောင်_O/O မ_O/O လေး_O/O တစ်_O/O ယောက်_O/O ကို_O/O မြင်_N/N သည်_E/E
အ_B/B သေး_O/O စား_O/O အ_O/O လို_O/O အ_O/O လျောက်_O/O ဂီ_O/O ယာ_O/O ထိုး_O/O တဲ့_O/O ကား_O/O ကို_O/O ဆောင်_N/O ရွက်_N/N ပေး_N/N ပါ_E/E
အဲ_B/B ဒီ_O/O အ_O/O ရပ်_O/O က_O/O တိုင်_O/O ဖွန်း_O/O မုန်_O/O တိုင်း_O/O ကြောင့်_O/O အ_O/O တော်_O/O လေး_O/O ပျက်_O/O စီး_O/O ဆုံး_O/O ရှုံး_O/O ခဲ့_N/N ရ_N/N တယ်_E/E
သူ_B/B က_O/O သာ_O/O ယာ_O/O ကြည်_O/O နူး_O/O ဖွယ်_O/O ကောင်း_O/O သော_O/O ကျေး_O/O လက်_O/O သီ_O/O ချင်း_O/O ကို_O/O သီ_O/O ဆို_O/N ခဲ့_N/N တယ်_E/N မ_B/N ဟုတ်_N/N လား_E/E
အ_B/B ပင်_O/O တို့_O/O တွင်_O/O မူ_O/O အယ်_O/O လ_O/O ဂျေ_O/O ပင်_O/O များ_O/O ဖြစ်_O/O သော_O/O ယူ_O/O ဂ_O/O လီ_O/O နား_O/O နှင့်_O/O ဩ_O/O စီ_O/O လေ_O/O တို_O/O ရီး_O/O ယား_O/O ၌_O/O တွေ့_O/N ရ_N/N သည်_E/E
သုံး_B/B နှစ်_O/O ပျမ်း_O/O မျှ_O/O တစ်_O/O ဦး_O/O ချင်း_O/O တစ်_O/O နှစ်_O/O စု_O/O စု_O/O ပေါင်း_O/O ဝင်_O/O ငွေ_O/O အ_O/O မေ_O/O ရိ_O/O ကန်_O/O ဒေါ်_O/O လာ_O/O ၇_O/O ၅_O/O ဝ_O/O ထက်_O/O လျော့_O/O နည်း_O/O ရ_O/O မည်_O/O ဖြစ်_N/N သည်_E/E
သူ_B/B ၏_O/O ကြွယ်_O/O ဝ_O/O ချမ်း_O/O သာ_O/O မှု_O/O များ_O/O အ_O/O နက်_O/O ထက်_O/O ဝက်_O/O ကျော်_O/O ကို_O/O အာ_O/O မ_O/O ခံ_O/O ရင်း_O/O နှီး_O/O မြှုပ်_O/O နှံ_O/O ခြင်း_O/O ၌_O/O သာ_O/O ထည့်_O/N သွင်း_O/N ခဲ့_N/N သည်_E/E
```

```
(base) ye@lst-gpu-server-197:~/data/hello-sayarwon/coding/model-based/models/fasttext/wordtag/models$ shuf CRF.hyp | head
ခင်_B/B ဗျား_O/O လေ_O/O ယာဉ်_O/O အ_O/O ကြာ_O/O ကြီး_O/O စီး_O/O ပြီး_O/O အ_O/O တော်_O/O ပင်_O/O ပန်း_O/O နေ_O/O ပြီ_O/O လို့_O/O ကျွန်_O/O တော်_O/O ထင်_N/N တယ်_E/E
စောင့်_B/B ကြပ်_O/O မှု_O/O တာ_O/O ဝန်_O/O ကို_O/O ယူ_N/N သည်_E/E
အ_B/B သေ_O/O အ_O/O ချာ_N/N ပဲ_E/E
ဝါ_B/B ဆို_O/O သည်_O/O မြန်_O/O မာ_O/O ပကြ္ခ_O/O ဒိန်_O/O ၏_O/O စ_O/O တုတ္ထ_O/O လ_O/O ဖြစ်_N/N သည်_E/E
ပို_B/B သေ_O/O ချာ_O/O အောင်_O/O ခင်_O/O ဗျား_O/O ကို_O/O ဓာတ်_O/O မှန်_O/O ရိုက်_O/O ကြည့်_N/N မယ်_N/N နော်_E/E
မိုး_B/B နေ_N/N တယ်_E/E
ကျွန်_B/B တော်_N/N သိ_N/N ပါ_N/N တယ်_E/E ဒီ_B/B နာ_O/O မည်_O/O က_O/O ရန်_O/O ကုန်_O/O က_O/O လူ_O/O တွေ_O/O ပေး_O/O ကြ_O/O တဲ့_O/O နာ_O/O မည်_O/O တွေ_O/O လို_O/O မ_O/O လှ_O/O ပါ_N/N ဘူး_E/E ဒါ_B/B ပေ_O/O မယ့်_O/O ကျွန်_O/O တော်_O/O သူ့_O/O ကို_O/O တ_O/O ကယ်_O/O ခဈ်_O/O တာ_O/O ပါ_O/O ဗျာ_O/O သူ့_O/O ကို_O/O တွေ့_O/O က_O/O တည်း_O/O က_O/O တစ်_O/O လျှောက်_O/O လုံး_O/O ကျွန်_O/O တော်_O/O သိ_O/O စေ_O/O ချင်_O/O တာ_O/O က_O/O ကျွန်_O/O တော့်_O/O အ_O/O ခဈ်_O/O ပါ_O/O မ_O/O သိ_O/O စေ_O/O ချင်_O/O တာ_O/O က_O/O ကျွန်_O/O တော့်_O/O နာ_O/O မည်_N/N ပါ_E/E
သွား_B/B ကြည့်_N/N ကြ_N/N စို့_E/E
နေ_B/B ပြည်_O/O တော်_O/O ရှိ_O/O လမ်း_O/O ဆုံ_O/O ဗ_O/O ဟို_O/O ကုန်_O/O တိုက်_O/O တွင်_O/O ရုပ်_O/O ရှင်_O/O ရုံ_O/O တစ်_O/O ရုံ_O/O နှင့်_O/O ပျဉ်း_O/O မ_O/O နား_O/O နှင့်_O/O တပ်_O/O ကုန်း_O/O တို့_O/O တွင်_O/O တစ်_O/O ရုံ_O/O စီ_O/O ရှိ_N/N သည်_E/E
The_B/B Way_O/O We_O/O Were_O/O ဆို_O/N ရင်_N/N ကော_E/E
```

CRF model က ကောင်းကောင်း အလုပ်လုပ်ပေးပေမဲ့ လက်ရှိ ရလဒ်ထက် မြှင့်နိုင်ဖို့ နည်းလမ်းရှာရန်။  
