# Semantic Chunking Experiment Log
## Reference Code  

```
import re


single_sentences_list = re.split(r'(?<=[.?!])\s+', essay)
print(f"{len(single_sentences_list)} sentences were found")

sentences = [{'sentence': x, 'index' :i} for i, x in enumerate(single_sentences_list)]
sentences[:3]

def combine_sentences(sentences, buffer_size=1):
    for i in range(len(sentences)):
        combined_sentence =''
        for j in range(i - buffer_size, i):
            if j >= 0:
                combined_sentence += sentences[j]['sentence'] + ' '
        for j in range(i + 1, i + 1 + buffer_size):
            if j < len(sentences):
                combined_sentence += ' ' + sentences[j]['sentence']

        sentences[i]['combined_sentence'] = combined_sentence
    return sentences

sentences = combine_sentences(sentences)

from langchain.embeddings import OpenAIEmbeddings
oaiembeds = OpenAIEmbeddings()

embeddings = oaiembeds.embed_documents([x['combined_sentence'] for x in sentences])

for i, sentence in enumerate(sentences):
    sentence['combined_sentence_embedding'] = embeddings[i]

from sklearn.metrics.pairwise import cosine_similarity

def calculate_cosine_distances(sentences):

    distances = []
    for i in range(len(sentences) - 1):
        embedding_current = sentences[i]['combined_sentence_embedding']
embedding_next = sentences[i+1]['combined_sentence_embedding']

        similarity = cosine_similarity([embedding_current], [embedding_next])[0][0]
        distance = 1 - similarity
        distances.append(distance)
        sentences[i]['distance_to_next'] = distance

    return distances, sentences

distances, sentences = calculate_cosine_distances(sentences)
distances[:3]

import matplotlib.pyplot as plt
plt.plot(distances)
```

=======

```
import numpy as np

plt.plot(distances);

y_upper_bound = .2
plt.ylim(0, y_upper_bound)
plt.xlim(0, len(distances))

breakpoint_percentile_threshold = 95
breakpoint_distance_threshold = np.percentile(distances, breakpoint_percentile_threshold)
plt.axhline(y=breakpoint_distance_threshold, color='r', linestyle='_');

num_distances_above_threshold = len([x for x in distances if x > breakpoint_distance_threshold])
plt.text(x=(len(distances)*.01), y=y_upper_bound/50, s=f"{num_distances_above_threshold + 1} Chunks");

indices_above_thresh = [i for i, x in enumerate(distances) if x > breakpoint_distance_threshold]

colors = ['b', 'g', 'r', 'c', 'm', 'y', 'k']
for i, breakpoint_index in enumerate(indices_above_thresh):
    start_index = 0 if i == 0 else indices_above_thresh[i -1]
    end_index = breakpoint_index if i < len(indices_above_thresh) - 1 else len(distance)

    plt.axvspan(start_index, end_index, facecolor=colors[i % len(colors)], alpha=0.25)
    plt.text(x=np.average([start_index, end_index]), 
        y=breakpoint_distance_threshold + (y_upper_bound)/ 20,
        s=f"Chunk #{1}", horizontalalignment='center',
        rotation='vertical')

if indices_above_thresh:
    last_breakpoint = indices_above_thresh[-1]
    if last_breakpoint < len(distances):
        plt.axvspan(last_breakpoint, len(distances), facecolor=colors[len(indices_above_thresh) % len(colors)], a
    plt.text(x=np.average([last_breakpoint, len(distances)]),
            y=breakpoint_distance_threshold + (y_upper_bound)/ 20,
            s=f"Chunk #{i+1}",
            rotation='vertical')

plt.title("PG Essay Chunks Based On  Embedding Breakpoints")
plt.xlabel("Index of sentences in essay (Sentence Position)")
plt.ylabel("Cosine distance between sequential sentences")
plt.show()
```

======

```
start_index = 0
chunks = []

for index in indices_above_thresh:
    end_index = index - 1

    group = sentences[start_index:end_index + 1]
    combined_text = ' '.join([d['sentence'] for d in group])
    chunks.append(combined_text)
    start_index = index

if start_index < len(sentences):
    combined_text = ' '.join([d['sentence'] for d in sentences[start_index:]])
chunks.append(combined_text)

now let's manually inspect a few to make sure they look ok.

for i, chunk in enumerate(chunks[:2]):
    buffer = 200
    print (f"Chunk #{i}")
    print (chunk[:buffer].strip())
print ("...")
print (chunk[-buffer:].strip())
print ("\n")
```

## Coding for FastText  

```python
"""
For building a FastText Model
Written by Ye Kyaw Thu, LU Lab., Myanmar
Last updated: 24 Dec 2024
How to run:  
python ./build_fasttext.py --corpus ./data/myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned.syl.normalized --model ./model/myfasttext_v1.bin
python ./build_fasttext.py --help
"""


import argparse
import fasttext

def build_fasttext_model(corpus_path, model_path, minn, maxn, dim, minCount):
    # Train the FastText model
    model = fasttext.train_unsupervised(corpus_path, 
                                        model='skipgram', 
                                        minn=minn, 
                                        maxn=maxn, 
                                        dim=dim,
                                        minCount=minCount)
    # Save the model
    model.save_model(model_path)
    print(f"Model saved to {model_path}")

def main():
    # Set up argument parser
    parser = argparse.ArgumentParser(description="Build a FastText model from a corpus.")
    parser.add_argument('--corpus', required=True, help="Path to the input corpus file.")
    parser.add_argument('--model', required=True, help="Path to save the output FastText model.")
    parser.add_argument('--minn', type=int, default=3, help="Minimum n-gram size. Default is 3.")
    parser.add_argument('--maxn', type=int, default=6, help="Maximum n-gram size. Default is 6.")
    parser.add_argument('--dim', type=int, default=100, help="Size of word vectors. Default is 100.")
    parser.add_argument('--minCount', type=int, default=1, help="Minimal number of word occurrences. Default is 1.")
    
    args = parser.parse_args()
    
    # Build the FastText model
    build_fasttext_model(args.corpus, args.model, args.minn, args.maxn, args.dim, args.minCount)

if __name__ == "__main__":
    main()


```


## FastText Model Building

--help  

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ python ./build_fasttext.py --help
usage: build_fasttext.py [-h] --corpus CORPUS --model MODEL [--minn MINN] [--maxn MAXN] [--dim DIM]
                         [--minCount MINCOUNT]

Build a FastText model from a corpus.

options:
  -h, --help           show this help message and exit
  --corpus CORPUS      Path to the input corpus file.
  --model MODEL        Path to save the output FastText model.
  --minn MINN          Minimum n-gram size. Default is 3.
  --maxn MAXN          Maximum n-gram size. Default is 6.
  --dim DIM            Size of word vectors. Default is 100.
  --minCount MINCOUNT  Minimal number of word occurrences. Default is 1.
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ time python ./build_fasttext.py --corpus ./data/myWord_myPOS_myPara_myNovel1v1_wordseg.shuf.cleaned.syl.normalized --model ./model/myfasttext_v1.bin
Read 10M words
Number of words:  6381
Number of labels: 0
Progress: 100.0% words/sec/thread:   72761 lr:  0.000000 avg.loss:  2.391126 ETA:   0h 0m 0s
Model saved to ./model/myfasttext_v1.bin

real    0m24.921s
user    11m37.243s
sys     0m2.252s
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$
```

```
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/sem-chunk/model$ ll -h myfasttext_v1.bin
-rw-rw-r-- 1 ye ye 768M Dec 24 01:13 myfasttext_v1.bin
(hs-fasttext) ye@lst-gpu-server-197:~/ye/exp/sem-chunk/model$
```

## Draft Code  

အရင်ဆုံး colab မှာ စမ်းခဲ့တဲ့ code တွေကို ချရေး...  

```python
import argparse
import fasttext
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity
import matplotlib.pyplot as plt

model = fasttext.load_model("/content/drive/My Drive/data/my_fasttext.model")

print(len(model.words))   # list of words in dictionary

print(model['ပြော ပြ ပါ'])  

def combine_sentences(sentences, buffer_size=1):
    for i in range(len(sentences)):
        combined_sentence =''
        for j in range(i - buffer_size, i):
            if j >= 0:
                combined_sentence += sentences[j]['sentence'] + ' '
        for j in range(i + 1, i + 1 + buffer_size):
            if j < len(sentences):
                combined_sentence += ' ' + sentences[j]['sentence']

        sentences[i]['combined_sentence'] = combined_sentence
    return sentences
	
def process_file(file_path, group_length=2):
    result = []
    with open(file_path, 'r', encoding='utf-8') as f:
        for line in f:
            words = line.split()  # Split the line into words
            # Create variable-length word groups
            word_groups = [' '.join(words[i:i+group_length]) for i in range(0, len(words), group_length)]
            result.extend(word_groups)  # Add to the result list
    return result

# Example usage
file_path = '/content/drive/My Drive/data/test2.syl'  # Replace with your file name
group_length = 6  # Adjust the group length as needed (e.g., 2, 3, 4, ...)
word_groups = process_file(file_path, group_length)
for group in word_groups:
    print(group)


sentences2 = [{'sentence': x, 'index' :i} for i, x in enumerate(word_groups)]
print(sentences2)

sentences = combine_sentences(sentences2)

def embed_documents(sentences):
    embeddings = [np.mean([model.get_word_vector(word) for word in sentence.split()], axis=0)
                  if sentence.strip() else np.zeros(model.get_dimension())
                  for sentence in sentences]
    return embeddings

# Assuming `sentences` is a list of dictionaries with a key 'combined_sentence'
embeddings = embed_documents([x['combined_sentence'] for x in sentences])

def calculate_cosine_distances(sentences):

    distances = []
    for i in range(len(sentences) - 1):
        embedding_current = sentences[i]['combined_sentence_embedding']
        embedding_next = sentences[i+1]['combined_sentence_embedding']

        similarity = cosine_similarity([embedding_current], [embedding_next])[0][0]
        distance = 1 - similarity
        distances.append(distance)
        sentences[i]['distance_to_next'] = distance

    return distances, sentences

for i, sentence in enumerate(sentences):
    sentence['combined_sentence_embedding'] = embeddings[i]
	
distances, sentences = calculate_cosine_distances(sentences)
print(distances)  

plt.plot(distances)

y_upper_bound = 1 # I need to play this value (original 0.2)
plt.ylim(0, y_upper_bound)
plt.xlim(0, len(distances))

breakpoint_percentile_threshold = 70
#breakpoint_percentile_threshold = 80 # I need to play this value
breakpoint_distance_threshold = np.percentile(distances, breakpoint_percentile_threshold)
plt.axhline(y=breakpoint_distance_threshold, color='r', linestyle='-');

num_distances_above_threshold = len([x for x in distances if x > breakpoint_distance_threshold])
plt.text(x=(len(distances)*.01), y=y_upper_bound/50, s=f"{num_distances_above_threshold + 1} Chunks");

indices_above_thresh = [i for i, x in enumerate(distances) if x > breakpoint_distance_threshold]

colors = ['b', 'g', 'r', 'c', 'm', 'y', 'k']
for i, breakpoint_index in enumerate(indices_above_thresh):
    start_index = 0 if i == 0 else indices_above_thresh[i -1]
    end_index = breakpoint_index if i < len(indices_above_thresh) - 1 else len(distances)

    plt.axvspan(start_index, end_index, facecolor=colors[i % len(colors)], alpha=0.25)
    plt.text(x=np.average([start_index, end_index]),
        y=breakpoint_distance_threshold + (y_upper_bound)/ 20,
        s=f"Chunk #{1}", horizontalalignment='center',
        rotation='vertical')

if indices_above_thresh:
    last_breakpoint = indices_above_thresh[-1]
    if last_breakpoint < len(distances):
        plt.axvspan(last_breakpoint, len(distances), facecolor=colors[len(indices_above_thresh) % len(colors)], alpha=0.25)
    plt.text(x=np.average([last_breakpoint, len(distances)]),
            y=breakpoint_distance_threshold + (y_upper_bound)/ 20,
            s=f"Chunk #{i+1}",
            rotation='vertical')

plt.title("Chunks Based On  Embedding Breakpoints")
plt.xlabel("Index of sentences in input (Sentence Position)")
plt.ylabel("Cosine distance between sequential sentences")
#plt.show()

plt.savefig(distances.png)
plt.savefig(distances.pdf)

start_index = 0
chunks = []

for index in indices_above_thresh:
    end_index = index - 1

    group = sentences[start_index:end_index + 1]
    combined_text = ' '.join([d['sentence'] for d in group])
    chunks.append(combined_text)
    start_index = index

if start_index < len(sentences):
    combined_text = ' '.join([d['sentence'] for d in sentences[start_index:]])
chunks.append(combined_text)

print("No. of chunks: ", len(chunks))

for i, chunk in enumerate(chunks):
    buffer = 3000
    print (f"Chunk #{i}")
    print (chunk[:buffer].strip())
print ("...")
print (chunk[-buffer:].strip())
print ("\n")


```

## FastText Installation Again  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ /home/ye/anaconda3/bin/python -m pip install fasttext
WARNING: Keyring is skipped due to an exception: Failed to unlock the collection!
Processing /home/ye/.cache/pip/wheels/7b/ab/44/06c2149a045ffb2a91d61aaea452674d2e70f00d51de699414/fasttext-0.9.3-cp38-cp38-linux_x86_64.whl
Requirement already satisfied: numpy in /home/ye/anaconda3/lib/python3.8/site-packages (from fasttext) (1.21.6)
Collecting pybind11>=2.2
  Downloading pybind11-2.13.6-py3-none-any.whl (243 kB)
     |████████████████████████████████| 243 kB 7.6 MB/s
Requirement already satisfied: setuptools>=0.7.0 in /home/ye/anaconda3/lib/python3.8/site-packages (from fasttext) (50.3.1.post20201107)
Installing collected packages: pybind11, fasttext
Successfully installed fasttext-0.9.3 pybind11-2.13.6
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$
```

## Code Updating  

```python
"""
Written by Ye Kyaw Thu, LU Lab., Myanmar
Last updated: 24 Dec 2024
How to run:  
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances --chunk_filename chunk1.txt

"""

import argparse
import fasttext
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity
import matplotlib.pyplot as plt

def combine_sentences(sentences, buffer_size=1):
    for i in range(len(sentences)):
        combined_sentence = ''
        for j in range(i - buffer_size, i):
            if j >= 0:
                combined_sentence += sentences[j]['sentence'] + ' '
        for j in range(i + 1, i + 1 + buffer_size):
            if j < len(sentences):
                combined_sentence += ' ' + sentences[j]['sentence']

        sentences[i]['combined_sentence'] = combined_sentence
    return sentences

def process_file(file_path, group_length=2):
    result = []
    with open(file_path, 'r', encoding='utf-8') as f:
        for line in f:
            words = line.split()  # Split the line into words
            # Create variable-length word groups
            word_groups = [' '.join(words[i:i+group_length]) for i in range(0, len(words), group_length)]
            result.extend(word_groups)  # Add to the result list
    return result

def embed_documents(sentences, model):
    embeddings = [np.mean([model.get_word_vector(word) for word in sentence.split()], axis=0)
                  if sentence.strip() else np.zeros(model.get_dimension())
                  for sentence in sentences]
    return embeddings

def calculate_cosine_distances(sentences):
    distances = []
    for i in range(len(sentences) - 1):
        embedding_current = sentences[i]['combined_sentence_embedding']
        embedding_next = sentences[i + 1]['combined_sentence_embedding']

        similarity = cosine_similarity([embedding_current], [embedding_next])[0][0]
        distance = 1 - similarity
        distances.append(distance)
        sentences[i]['distance_to_next'] = distance

    return distances, sentences

def main():
    parser = argparse.ArgumentParser(description="Process text and visualize embeddings.")
    parser.add_argument('--model', required=True, help="Path to the FastText model file.")
    parser.add_argument('--input', required=True, help="Path to the input text file.")
    parser.add_argument('--buffer', type=int, default=3000, help="Buffer size for printing chunks. Default: 3000")
    parser.add_argument('--percentile_threshold', type=int, default=70, help="Breakpoint percentile threshold.")
    parser.add_argument('--y_upper_bound', type=float, default=1.0, help="Upper bound for the Y-axis in the plot. Default: 70")
    parser.add_argument('--graph_filename', required=True, help="Filename for saving the graph (without extension). Default: 1.0")
    parser.add_argument('--chunk_filename', help="Filename to save the segmented chunks.")

    args = parser.parse_args()

    # Load FastText model
    model = fasttext.load_model(args.model)

    # Process input file
    group_length = 6  # Default group length for splitting words
    word_groups = process_file(args.input, group_length)

    # Prepare sentences
    sentences2 = [{'sentence': x, 'index': i} for i, x in enumerate(word_groups)]
    sentences = combine_sentences(sentences2)

    # Embed documents
    embeddings = embed_documents([x['combined_sentence'] for x in sentences], model)
    for i, sentence in enumerate(sentences):
        sentence['combined_sentence_embedding'] = embeddings[i]

    # Calculate cosine distances
    distances, sentences = calculate_cosine_distances(sentences)

    # Plot distances
    plt.plot(distances)
    plt.ylim(0, args.y_upper_bound)
    plt.xlim(0, len(distances))
    breakpoint_distance_threshold = np.percentile(distances, args.percentile_threshold)
    plt.axhline(y=breakpoint_distance_threshold, color='r', linestyle='-')

    # Add breakpoints and regions
    indices_above_thresh = [i for i, x in enumerate(distances) if x > breakpoint_distance_threshold]
    colors = ['b', 'g', 'r', 'c', 'm', 'y', 'k']
    for i, breakpoint_index in enumerate(indices_above_thresh):
        start_index = 0 if i == 0 else indices_above_thresh[i - 1]
        end_index = breakpoint_index if i < len(indices_above_thresh) - 1 else len(distances)
        plt.axvspan(start_index, end_index, facecolor=colors[i % len(colors)], alpha=0.25)

    if indices_above_thresh:
        last_breakpoint = indices_above_thresh[-1]
        if last_breakpoint < len(distances):
            plt.axvspan(last_breakpoint, len(distances), facecolor=colors[len(indices_above_thresh) % len(colors)], alpha=0.25)

    plt.title("Chunks Based On Embedding Breakpoints")
    plt.xlabel("Index of sentences in input (Sentence Position)")
    plt.ylabel("Cosine distance between sequential sentences")
    plt.savefig(f"{args.graph_filename}.png")
    plt.savefig(f"{args.graph_filename}.pdf")

    # Segment into chunks
    start_index = 0
    chunks = []
    for index in indices_above_thresh:
        end_index = index - 1
        group = sentences[start_index:end_index + 1]
        combined_text = ' '.join([d['sentence'] for d in group])
        chunks.append(combined_text)
        start_index = index

    if start_index < len(sentences):
        combined_text = ' '.join([d['sentence'] for d in sentences[start_index:]])
        chunks.append(combined_text)

    print("No. of chunks: ", len(chunks))
    for i, chunk in enumerate(chunks):
        print(f"Chunk #{i}")
        print(chunk[:args.buffer].strip())

    print(chunk[-args.buffer:].strip())

    # Save chunks to file if specified
    if args.chunk_filename:
        with open(args.chunk_filename, 'w', encoding='utf-8') as f:
            for chunk in chunks:
                if chunk.strip():  # Only write non-empty chunks
                    f.write(chunk.strip() + '\n')  # Strip any trailing/leading whitespace
        print(f"Chunks saved to {args.chunk_filename}")


if __name__ == "__main__":
    main()


```

--help  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ python ./semantic_chunk.py --help
usage: semantic_chunk.py [-h] --model MODEL --input INPUT [--buffer BUFFER]
                         [--percentile_threshold PERCENTILE_THRESHOLD] [--y_upper_bound Y_UPPER_BOUND]
                         --graph_filename GRAPH_FILENAME [--chunk_filename CHUNK_FILENAME]

Process text and visualize embeddings.

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL         Path to the FastText model file.
  --input INPUT         Path to the input text file.
  --buffer BUFFER       Buffer size for printing chunks. Default: 3000
  --percentile_threshold PERCENTILE_THRESHOLD
                        Breakpoint percentile threshold. Default: 70
  --y_upper_bound Y_UPPER_BOUND
                        Upper bound for the Y-axis in the plot. Default: 1.0
  --graph_filename GRAPH_FILENAME
                        Filename for saving the graph (without extension). Default: 1.0
  --chunk_filename CHUNK_FILENAME
                        Filename to save the segmented chunks.
```

Running ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
> --graph_filename distances --chunk_filename chunk1.txt
No. of chunks:  18
Chunk #0

Chunk #1
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး - မော် စ ကို အ ထိ ရောက် နေ တဲ့ ယူ က ရိန်း
Chunk #2
ထောက် လှမ်း ရေး
Chunk #3
ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န က အေး ဂျင့် တွေ ဟာ စစ် ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ် ထိပ် ပိုင်း အ ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ စေ " အဲ ဒီ သူ တွေ ကို တိုက် ခိုက် နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ မှာ ရှိ တဲ့ ဘီ ဘီ စီ
Chunk #4
ယူ က ရိန်း ရဲ့ သ တင်း ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။ အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။
Chunk #5
စ ကူ တာ လေး ထဲ မှာ
Chunk #6
ထည့် ထား ပုံ ရ တဲ့ ဗုံး
Chunk #7
နဲ့ ရု ရှား ဒု တိ ယ ဗိုလ် ချုပ် ကြီး အစ် ဂေါ ကီ လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း မှာ မော့ ဆက် အ ဖွဲ့ က ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို လာ တို့ ကို တိုက် ခိုက် ပုံ
Chunk #8
နဲ့ နှိုင်း ယှ ဥ် နိုင် တယ်
Chunk #9
လို့ ယူ က ရိန်း လုံ ခြုံ
Chunk #10
ရေး ဌာ န ( Security Service
Chunk #11
of Ukraine - SBU ) က အ ရာ ရှိ ဟောင်း အိုင် ဗင်
Chunk #12
စ တု ပက်ခ် က ပြော ပါ
Chunk #13
တယ် ။
Chunk #14
" သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက် မ လား ၊ အ ဆိပ် ပေး မ လား ဆို တာ ကို ယူ က ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
Chunk #15
ရေး ဌာ န က ဆုံး ဖြတ် တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး ရ အာ ဏာ ပိုင် တွေ က
Chunk #16
တ ရား ဝင် မှတ် ချက် ချ
Chunk #17
တာ မျိုး မ ရှိ ပါ ဘူး ။
တာ မျိုး မ ရှိ ပါ ဘူး ။
Chunks saved to chunk1.txt

real    0m1.970s
user    0m4.331s
sys     0m3.691s

```

Test file ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ cat ./test1.syl
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး - မော် စ ကို အ ထိ ရောက် နေ တဲ့ ယူ က ရိန်း ထောက် လှမ်း ရေး
ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န က အေး ဂျင့် တွေ ဟာ စစ် ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ် ထိပ် ပိုင်း အ ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ စေ " အဲ ဒီ သူ တွေ ကို တိုက် ခိုက် နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ မှာ ရှိ တဲ့ ဘီ ဘီ စီ ယူ က ရိန်း ရဲ့ သ တင်း ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။
အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။
စ ကူ တာ လေး ထဲ မှာ ထည့် ထား ပုံ ရ တဲ့ ဗုံး နဲ့ ရု ရှား ဒု တိ ယ ဗိုလ် ချုပ် ကြီး အစ် ဂေါ ကီ လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း မှာ မော့ ဆက် အ ဖွဲ့ က ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို လာ တို့ ကို တိုက် ခိုက် ပုံ နဲ့ နှိုင်း ယှ ဥ် နိုင် တယ် လို့ ယူ က ရိန်း လုံ ခြုံ ရေး ဌာ န ( Security Service of Ukraine - SBU ) က အ ရာ ရှိ ဟောင်း အိုင် ဗင် စ တု ပက်ခ် က ပြော ပါ တယ် ။
" သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက် မ လား ၊ အ ဆိပ် ပေး မ လား ဆို တာ ကို ယူ က ရိန်း လျှို့ ဝှက် ထောက် လှမ်း ရေး ဌာ န က ဆုံး ဖြတ် တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။
ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး ရ အာ ဏာ ပိုင် တွေ က တ ရား ဝင် မှတ် ချက် ချ တာ မျိုး မ ရှိ ပါ ဘူး ။
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$
```

Chunked output file():  

```
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး - မော် စ ကို အ ထိ ရောက် နေ တဲ့ ယူ က ရိန်း
ထောက် လှမ်း ရေး
ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န က အေး ဂျင့် တွေ ဟာ စစ် ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ် ထိပ် ပိုင်း အ ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ စေ " အဲ ဒီ သူ တွေ ကို တိုက် ခိုက် နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ မှာ ရှိ တဲ့ ဘီ ဘီ စီ
ယူ က ရိန်း ရဲ့ သ တင်း ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။ အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။
စ ကူ တာ လေး ထဲ မှာ
ထည့် ထား ပုံ ရ တဲ့ ဗုံး
နဲ့ ရု ရှား ဒု တိ ယ ဗိုလ် ချုပ် ကြီး အစ် ဂေါ ကီ လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း မှာ မော့ ဆက် အ ဖွဲ့ က ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို လာ တို့ ကို တိုက် ခိုက် ပုံ
နဲ့ နှိုင်း ယှ ဥ် နိုင် တယ်
လို့ ယူ က ရိန်း လုံ ခြုံ
ရေး ဌာ န ( Security Service
of Ukraine - SBU ) က အ ရာ ရှိ ဟောင်း အိုင် ဗင်
စ တု ပက်ခ် က ပြော ပါ
တယ် ။
" သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက် မ လား ၊ အ ဆိပ် ပေး မ လား ဆို တာ ကို ယူ က ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
ရေး ဌာ န က ဆုံး ဖြတ် တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး ရ အာ ဏာ ပိုင် တွေ က
တ ရား ဝင် မှတ် ချက် ချ
တာ မျိုး မ ရှိ ပါ ဘူး ။

```


## Parameter Changing

ဒီတခါတော့ --percentile_threshold ရဲ့ တန်ဖိုးကို 40 ထားကြည့်ခဲ့တယ်။  

```
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances --chunk_filename chunk2.txt --percentile_threshold 40
```

Running log:  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
> --graph_filename distances --chunk_filename chunk2.txt --percentile_threshold 40
No. of chunks:  34
Chunk #0

Chunk #1
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး - မော် စ ကို အ ထိ ရောက် နေ တဲ့ ယူ က ရိန်း
Chunk #2
ထောက် လှမ်း ရေး
Chunk #3
ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န
Chunk #4
က အေး ဂျင့် တွေ ဟာ စစ်
Chunk #5
ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ် ထိပ် ပိုင်း အ ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ စေ " အဲ ဒီ
Chunk #6
သူ တွေ ကို တိုက် ခိုက် နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ
Chunk #7
မှာ ရှိ တဲ့ ဘီ ဘီ စီ
Chunk #8
ယူ က ရိန်း ရဲ့ သ တင်း
Chunk #9
ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။
Chunk #10
အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။
Chunk #11
စ ကူ တာ လေး ထဲ မှာ
Chunk #12
ထည့် ထား ပုံ ရ တဲ့ ဗုံး
Chunk #13
နဲ့ ရု ရှား ဒု တိ ယ
Chunk #14
ဗိုလ် ချုပ် ကြီး အစ် ဂေါ ကီ
Chunk #15
လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း
Chunk #16
မှာ မော့ ဆက် အ ဖွဲ့ က
Chunk #17
ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို
Chunk #18
လာ တို့ ကို တိုက် ခိုက် ပုံ
Chunk #19
နဲ့ နှိုင်း ယှ ဥ် နိုင် တယ်
Chunk #20
လို့ ယူ က ရိန်း လုံ ခြုံ
Chunk #21
ရေး ဌာ န ( Security Service
Chunk #22
of Ukraine - SBU ) က
Chunk #23
အ ရာ ရှိ ဟောင်း အိုင် ဗင်
Chunk #24
စ တု ပက်ခ် က ပြော ပါ
Chunk #25
တယ် ။
Chunk #26
" သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက်
Chunk #27
မ လား ၊ အ ဆိပ် ပေး
Chunk #28
မ လား ဆို တာ ကို ယူ
Chunk #29
က ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
Chunk #30
ရေး ဌာ န က ဆုံး ဖြတ် တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး
Chunk #31
ရ အာ ဏာ ပိုင် တွေ က
Chunk #32
တ ရား ဝင် မှတ် ချက် ချ
Chunk #33
တာ မျိုး မ ရှိ ပါ ဘူး ။
တာ မျိုး မ ရှိ ပါ ဘူး ။
Chunks saved to chunk2.txt

real    0m1.891s
user    0m4.069s
sys     0m3.858s

```

Chunked Output File (chunk2.txt):  

```
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး - မော် စ ကို အ ထိ ရောက် နေ တဲ့ ယူ က ရိန်း
ထောက် လှမ်း ရေး
ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န
က အေး ဂျင့် တွေ ဟာ စစ်
ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ် ထိပ် ပိုင်း အ ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ စေ " အဲ ဒီ
သူ တွေ ကို တိုက် ခိုက် နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ
မှာ ရှိ တဲ့ ဘီ ဘီ စီ
ယူ က ရိန်း ရဲ့ သ တင်း
ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။
အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။
စ ကူ တာ လေး ထဲ မှာ
ထည့် ထား ပုံ ရ တဲ့ ဗုံး
နဲ့ ရု ရှား ဒု တိ ယ
ဗိုလ် ချုပ် ကြီး အစ် ဂေါ ကီ
လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း
မှာ မော့ ဆက် အ ဖွဲ့ က
ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို
လာ တို့ ကို တိုက် ခိုက် ပုံ
နဲ့ နှိုင်း ယှ ဥ် နိုင် တယ်
လို့ ယူ က ရိန်း လုံ ခြုံ
ရေး ဌာ န ( Security Service
of Ukraine - SBU ) က
အ ရာ ရှိ ဟောင်း အိုင် ဗင်
စ တု ပက်ခ် က ပြော ပါ
တယ် ။
" သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက်
မ လား ၊ အ ဆိပ် ပေး
မ လား ဆို တာ ကို ယူ
က ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
ရေး ဌာ န က ဆုံး ဖြတ် တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး
ရ အာ ဏာ ပိုင် တွေ က
တ ရား ဝင် မှတ် ချက် ချ
တာ မျိုး မ ရှိ ပါ ဘူး ။

```

## Updating Code  

No. of chunk ကိုပါ ဂရဖ်မှာ ထည့် ...  

```python
"""
Written by Ye Kyaw Thu, LU Lab., Myanmar
Last updated: 24 Dec 2024

How to run, Example 1:  
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances --chunk_filename chunk1.txt

Example 2:
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances --chunk_filename chunk2.txt --percentile_threshold 40
"""

import argparse
import fasttext
import numpy as np
from sklearn.metrics.pairwise import cosine_similarity
import matplotlib.pyplot as plt

def combine_sentences(sentences, buffer_size=1):
    for i in range(len(sentences)):
        combined_sentence = ''
        for j in range(i - buffer_size, i):
            if j >= 0:
                combined_sentence += sentences[j]['sentence'] + ' '
        for j in range(i + 1, i + 1 + buffer_size):
            if j < len(sentences):
                combined_sentence += ' ' + sentences[j]['sentence']

        sentences[i]['combined_sentence'] = combined_sentence
    return sentences

def process_file(file_path, group_length=2):
    result = []
    with open(file_path, 'r', encoding='utf-8') as f:
        for line in f:
            words = line.split()  # Split the line into words
            # Create variable-length word groups
            word_groups = [' '.join(words[i:i+group_length]) for i in range(0, len(words), group_length)]
            result.extend(word_groups)  # Add to the result list
    return result

def embed_documents(sentences, model):
    embeddings = [np.mean([model.get_word_vector(word) for word in sentence.split()], axis=0)
                  if sentence.strip() else np.zeros(model.get_dimension())
                  for sentence in sentences]
    return embeddings

def calculate_cosine_distances(sentences):
    distances = []
    for i in range(len(sentences) - 1):
        embedding_current = sentences[i]['combined_sentence_embedding']
        embedding_next = sentences[i + 1]['combined_sentence_embedding']

        similarity = cosine_similarity([embedding_current], [embedding_next])[0][0]
        distance = 1 - similarity
        distances.append(distance)
        sentences[i]['distance_to_next'] = distance

    return distances, sentences

def main():
    parser = argparse.ArgumentParser(description="Process text and visualize embeddings.")
    parser.add_argument('--model', required=True, help="Path to the FastText model file.")
    parser.add_argument('--input', required=True, help="Path to the input text file.")
    parser.add_argument('--buffer', type=int, default=3000, help="Buffer size for printing chunks. Default: 3000")
    parser.add_argument('--percentile_threshold', type=int, default=70, help="Breakpoint percentile threshold. Default: 70")
    parser.add_argument('--y_upper_bound', type=float, default=1.0, help="Upper bound for the Y-axis in the plot. Default: 1.0")
    parser.add_argument('--graph_filename', required=True, help="Filename for saving the graph (without extension). Default: 1.0")
    parser.add_argument('--chunk_filename', help="Filename to save the segmented chunks.")

    args = parser.parse_args()

    # Load FastText model
    model = fasttext.load_model(args.model)

    # Process input file
    group_length = 6  # Default group length for splitting words
    word_groups = process_file(args.input, group_length)

    # Prepare sentences
    sentences2 = [{'sentence': x, 'index': i} for i, x in enumerate(word_groups)]
    sentences = combine_sentences(sentences2)

    # Embed documents
    embeddings = embed_documents([x['combined_sentence'] for x in sentences], model)
    for i, sentence in enumerate(sentences):
        sentence['combined_sentence_embedding'] = embeddings[i]

    # Calculate cosine distances
    distances, sentences = calculate_cosine_distances(sentences)

    # Plot distances
    plt.plot(distances)
    plt.ylim(0, args.y_upper_bound)
    plt.xlim(0, len(distances))
    breakpoint_distance_threshold = np.percentile(distances, args.percentile_threshold)
    plt.axhline(y=breakpoint_distance_threshold, color='r', linestyle='-')

    # Add text annotation for the number of chunks
    num_distances_above_threshold = len([d for d in distances if d > breakpoint_distance_threshold])-1
    plt.text(x=(len(distances) * 0.01), 
             y=args.y_upper_bound / 50, 
             s=f"{num_distances_above_threshold + 1} Chunks", 
             color='black', fontsize=10)

    # Add breakpoints and regions
    indices_above_thresh = [i for i, x in enumerate(distances) if x > breakpoint_distance_threshold]
    colors = ['b', 'g', 'r', 'c', 'm', 'y', 'k']
    for i, breakpoint_index in enumerate(indices_above_thresh):
        start_index = 0 if i == 0 else indices_above_thresh[i - 1]
        end_index = breakpoint_index if i < len(indices_above_thresh) - 1 else len(distances)
        plt.axvspan(start_index, end_index, facecolor=colors[i % len(colors)], alpha=0.25)

    if indices_above_thresh:
        last_breakpoint = indices_above_thresh[-1]
        if last_breakpoint < len(distances):
            plt.axvspan(last_breakpoint, len(distances), facecolor=colors[len(indices_above_thresh) % len(colors)], alpha=0.25)

    plt.title("Chunks Based On FastText Embedding Breakpoints")
    plt.xlabel("Index of sentences (Sentence Position)")
    plt.ylabel("Cosine distance between sequential sentences")
    plt.savefig(f"{args.graph_filename}.png")
    plt.savefig(f"{args.graph_filename}.pdf")

    # Segment into chunks
    start_index = 0
    chunks = []
    for index in indices_above_thresh:
        end_index = index - 1
        group = sentences[start_index:end_index + 1]
        combined_text = ' '.join([d['sentence'] for d in group])
        chunks.append(combined_text)
        start_index = index

    if start_index < len(sentences):
        combined_text = ' '.join([d['sentence'] for d in sentences[start_index:]])
        chunks.append(combined_text)

    print("No. of chunks: ", len(chunks))
    for i, chunk in enumerate(chunks):
        print(f"Chunk #{i}")
        print(chunk[:args.buffer].strip())

    print(chunk[-args.buffer:].strip())

    # Save chunks to file if specified
    if args.chunk_filename:
        with open(args.chunk_filename, 'w', encoding='utf-8') as f:
            for chunk in chunks:
                if chunk.strip():  # Only write non-empty chunks
                    f.write(chunk.strip() + '\n')  # Strip any trailing/leading whitespace
        print(f"Chunks saved to {args.chunk_filename}")


if __name__ == "__main__":
    main()


```

--help  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ python ./semantic_chunk.py --help
usage: semantic_chunk.py [-h] --model MODEL --input INPUT [--buffer BUFFER]
                         [--percentile_threshold PERCENTILE_THRESHOLD] [--y_upper_bound Y_UPPER_BOUND]
                         --graph_filename GRAPH_FILENAME [--chunk_filename CHUNK_FILENAME]

Process text and visualize embeddings.

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL         Path to the FastText model file.
  --input INPUT         Path to the input text file.
  --buffer BUFFER       Buffer size for printing chunks. Default: 3000
  --percentile_threshold PERCENTILE_THRESHOLD
                        Breakpoint percentile threshold. Default: 70
  --y_upper_bound Y_UPPER_BOUND
                        Upper bound for the Y-axis in the plot. Default: 1.0
  --graph_filename GRAPH_FILENAME
                        Filename for saving the graph (without extension). Default: 1.0
  --chunk_filename CHUNK_FILENAME
                        Filename to save the segmented chunks.
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$
```

## Test Again  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl --graph_filename distances-eg3 --chunk_filename chunk3.txt --percentile_threshold 30 --y_upper_bound 0.5
No. of chunks:  40
Chunk #0

Chunk #1
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး
Chunk #2
- မော် စ ကို အ ထိ
Chunk #3
ရောက် နေ တဲ့ ယူ က ရိန်း
Chunk #4
ထောက် လှမ်း ရေး
Chunk #5
ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န
Chunk #6
က အေး ဂျင့် တွေ ဟာ စစ်
Chunk #7
ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ် ထိပ် ပိုင်း အ
Chunk #8
ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ
Chunk #9
နေ ပါ စေ " အဲ ဒီ
Chunk #10
သူ တွေ ကို တိုက် ခိုက် နေ
Chunk #11
ကြောင်း အဲ ဒီ ဌာ န ထဲ
Chunk #12
မှာ ရှိ တဲ့ ဘီ ဘီ စီ
Chunk #13
ယူ က ရိန်း ရဲ့ သ တင်း
Chunk #14
ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။
Chunk #15
အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။
Chunk #16
စ ကူ တာ လေး ထဲ မှာ
Chunk #17
ထည့် ထား ပုံ ရ တဲ့ ဗုံး
Chunk #18
နဲ့ ရု ရှား ဒု တိ ယ
Chunk #19
ဗိုလ် ချုပ် ကြီး အစ် ဂေါ ကီ
Chunk #20
လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း
Chunk #21
မှာ မော့ ဆက် အ ဖွဲ့ က
Chunk #22
ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို
Chunk #23
လာ တို့ ကို တိုက် ခိုက် ပုံ
Chunk #24
နဲ့ နှိုင်း ယှ ဥ် နိုင် တယ်
Chunk #25
လို့ ယူ က ရိန်း လုံ ခြုံ
Chunk #26
ရေး ဌာ န ( Security Service
Chunk #27
of Ukraine - SBU ) က
Chunk #28
အ ရာ ရှိ ဟောင်း အိုင် ဗင်
Chunk #29
စ တု ပက်ခ် က ပြော ပါ
Chunk #30
တယ် ။
Chunk #31
" သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက်
Chunk #32
မ လား ၊ အ ဆိပ် ပေး
Chunk #33
မ လား ဆို တာ ကို ယူ
Chunk #34
က ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
Chunk #35
ရေး ဌာ န က ဆုံး ဖြတ်
Chunk #36
တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး
Chunk #37
ရ အာ ဏာ ပိုင် တွေ က
Chunk #38
တ ရား ဝင် မှတ် ချက် ချ
Chunk #39
တာ မျိုး မ ရှိ ပါ ဘူး ။
တာ မျိုး မ ရှိ ပါ ဘူး ။
Chunks saved to chunk3.txt

real    0m1.921s
user    0m4.259s
sys     0m3.711s

```

Check the chunked file (chunk3.txt):  

```
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး
- မော် စ ကို အ ထိ
ရောက် နေ တဲ့ ယူ က ရိန်း
ထောက် လှမ်း ရေး
ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န
က အေး ဂျင့် တွေ ဟာ စစ်
ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ် ထိပ် ပိုင်း အ
ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ
နေ ပါ စေ " အဲ ဒီ
သူ တွေ ကို တိုက် ခိုက် နေ
ကြောင်း အဲ ဒီ ဌာ န ထဲ
မှာ ရှိ တဲ့ ဘီ ဘီ စီ
ယူ က ရိန်း ရဲ့ သ တင်း
ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။
အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။
စ ကူ တာ လေး ထဲ မှာ
ထည့် ထား ပုံ ရ တဲ့ ဗုံး
နဲ့ ရု ရှား ဒု တိ ယ
ဗိုလ် ချုပ် ကြီး အစ် ဂေါ ကီ
လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း
မှာ မော့ ဆက် အ ဖွဲ့ က
ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို
လာ တို့ ကို တိုက် ခိုက် ပုံ
နဲ့ နှိုင်း ယှ ဥ် နိုင် တယ်
လို့ ယူ က ရိန်း လုံ ခြုံ
ရေး ဌာ န ( Security Service
of Ukraine - SBU ) က
အ ရာ ရှိ ဟောင်း အိုင် ဗင်
စ တု ပက်ခ် က ပြော ပါ
တယ် ။
" သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက်
မ လား ၊ အ ဆိပ် ပေး
မ လား ဆို တာ ကို ယူ
က ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
ရေး ဌာ န က ဆုံး ဖြတ်
တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး
ရ အာ ဏာ ပိုင် တွေ က
တ ရား ဝင် မှတ် ချက် ချ
တာ မျိုး မ ရှိ ပါ ဘူး ။

```

## Updating Code

--syllable_group_length ထပ်ဖြည့်တယ်။ ဒီကောင်းကလည်း အရေးကြီးလို့ ...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ python ./semantic_chunk.py --help
usage: semantic_chunk.py [-h] --model MODEL --input INPUT [--buffer BUFFER]
                         [--percentile_threshold PERCENTILE_THRESHOLD] [--y_upper_bound Y_UPPER_BOUND]
                         --graph_filename GRAPH_FILENAME [--chunk_filename CHUNK_FILENAME]
                         [--syllable_group_length SYLLABLE_GROUP_LENGTH]

Process text and visualize embeddings.

optional arguments:
  -h, --help            show this help message and exit
  --model MODEL         Path to the FastText model file.
  --input INPUT         Path to the input text file.
  --buffer BUFFER       Buffer size for printing chunks. Default: 3000
  --percentile_threshold PERCENTILE_THRESHOLD
                        Breakpoint percentile threshold. Default: 70
  --y_upper_bound Y_UPPER_BOUND
                        Upper bound for the Y-axis in the plot. Default: 1.0
  --graph_filename GRAPH_FILENAME
                        Filename for saving the graph (without extension). Default: 1.0
  --chunk_filename CHUNK_FILENAME
                        Filename to save the segmented chunks.
  --syllable_group_length SYLLABLE_GROUP_LENGTH
                        Initial syllable group length. Default: 2
```

## Test 

--syllable_group_length ကို 5 ထားပြီး ကစားကြည့်ခဲ့...  
  
```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl --graph_filename distances-eg4 --chunk_filename chunk4.txt --percentile_threshold 70 --y_upper_bound 0.5 --syllable_group_length 5
No. of chunks:  21
Chunk #0

Chunk #1
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး - မော် စ
Chunk #2
ကို အ ထိ ရောက် နေ
Chunk #3
တဲ့ ယူ က ရိန်း ထောက် လှမ်း ရေး ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န က အေး ဂျင့် တွေ ဟာ စစ် ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား
Chunk #4
စစ် တပ် ထိပ် ပိုင်း အ
Chunk #5
ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ
Chunk #6
စေ " အဲ ဒီ သူ တွေ ကို တိုက် ခိုက် နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ မှာ ရှိ တဲ့ ဘီ ဘီ စီ ယူ က ရိန်း ရဲ့ သ တင်း ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။ အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။ စ ကူ တာ လေး ထဲ
Chunk #7
မှာ ထည့် ထား ပုံ ရ
Chunk #8
တဲ့ ဗုံး နဲ့ ရု ရှား
Chunk #9
ဒု တိ ယ ဗိုလ် ချုပ်
Chunk #10
ကြီး အစ် ဂေါ ကီ လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း မှာ မော့ ဆက် အ ဖွဲ့ က ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို လာ တို့ ကို တိုက် ခိုက် ပုံ
Chunk #11
နဲ့ နှိုင်း ယှ ဥ် နိုင်
Chunk #12
တယ် လို့ ယူ က ရိန်း
Chunk #13
လုံ ခြုံ ရေး ဌာ န
Chunk #14
( Security Service of Ukraine
Chunk #15
- SBU ) က အ ရာ ရှိ ဟောင်း အိုင် ဗင် စ တု ပက်ခ် က ပြော
Chunk #16
ပါ တယ် ။ " သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက် မ လား ၊ အ ဆိပ် ပေး မ လား
Chunk #17
ဆို တာ ကို ယူ က
Chunk #18
ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
Chunk #19
ရေး ဌာ န က ဆုံး ဖြတ် တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး ရ အာ ဏာ ပိုင် တွေ က တ ရား ဝင် မှတ် ချက် ချ တာ
Chunk #20
မျိုး မ ရှိ ပါ ဘူး ။
မျိုး မ ရှိ ပါ ဘူး ။
Chunks saved to chunk3.txt

real    0m1.892s
user    0m4.388s
sys     0m3.525s

```

check the chunked output file (chunk4.txt):  

```
' တိုက် ပွဲ ဝင် ခြင် တွေ ' နဲ့ စ ကူ တာ ဗုံး - မော် စ
ကို အ ထိ ရောက် နေ
တဲ့ ယူ က ရိန်း ထောက် လှမ်း ရေး ယူ က ရိန်း လုံ ခြုံ ရေး နဲ့ ထောက် လှမ်း ရေး ဌာ န က အေး ဂျင့် တွေ ဟာ စစ် ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား
စစ် တပ် ထိပ် ပိုင်း အ
ရာ ရှိ တွေ နဲ့ တ ခြား ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ
စေ " အဲ ဒီ သူ တွေ ကို တိုက် ခိုက် နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ မှာ ရှိ တဲ့ ဘီ ဘီ စီ ယူ က ရိန်း ရဲ့ သ တင်း ရင်း မြစ် တွေ က အ တည် ပြု ပြော ပါ တယ် ။ အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ က ရိန်း နယ် မြေ တွေ ၊ ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ် ။ စ ကူ တာ လေး ထဲ
မှာ ထည့် ထား ပုံ ရ
တဲ့ ဗုံး နဲ့ ရု ရှား
ဒု တိ ယ ဗိုလ် ချုပ်
ကြီး အစ် ဂေါ ကီ လီ လော့ဗ် ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ တွင်း မှာ မော့ ဆက် အ ဖွဲ့ က ပေ ဂျာ တွေ နဲ့ ဟစ်ဇ် ဘို လာ တို့ ကို တိုက် ခိုက် ပုံ
နဲ့ နှိုင်း ယှ ဥ် နိုင်
တယ် လို့ ယူ က ရိန်း
လုံ ခြုံ ရေး ဌာ န
( Security Service of Ukraine
- SBU ) က အ ရာ ရှိ ဟောင်း အိုင် ဗင် စ တု ပက်ခ် က ပြော
ပါ တယ် ။ " သူ့ ကို ပစ် သတ် မ လား ၊ ဗုံး နဲ့ တိုက် ခိုက် မ လား ၊ အ ဆိပ် ပေး မ လား
ဆို တာ ကို ယူ က
ရိန်း လျှို့ ဝှက် ထောက် လှမ်း
ရေး ဌာ န က ဆုံး ဖြတ် တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ က ရိန်း အ စိုး ရ အာ ဏာ ပိုင် တွေ က တ ရား ဝင် မှတ် ချက် ချ တာ
မျိုး မ ရှိ ပါ ဘူး ။

```

## Test with Syllable Level Input  

--syllable_group_length 1 ထားပြီး စမ်းခဲ့...  

```
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$ time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl --graph_filename distances-eg5 --chunk_filename chunk5.txt --percentile_threshold 70 --y_upper_bound 0.5 --syllable_group_length 1
No. of chunks:  98
Chunk #0

Chunk #1
' တိုက်
Chunk #2
ပွဲ
Chunk #3
ဝင်
Chunk #4
ခြင်
Chunk #5
တွေ
Chunk #6
'
Chunk #7
နဲ့
Chunk #8
စ
Chunk #9
ကူ
Chunk #10
တာ
Chunk #11
ဗုံး
Chunk #12
-
Chunk #13
မော် စ ကို အ ထိ ရောက် နေ တဲ့
Chunk #14
ယူ
Chunk #15
က ရိန်း
Chunk #16
ထောက် လှမ်း
Chunk #17
ရေး
Chunk #18
ယူ
Chunk #19
က ရိန်း လုံ ခြုံ ရေး
Chunk #20
နဲ့
Chunk #21
ထောက် လှမ်း ရေး ဌာ န
Chunk #22
က အေး ဂျင့် တွေ ဟာ စစ် ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ်
Chunk #23
ထိပ် ပိုင်း အ ရာ ရှိ တွေ နဲ့ တ
Chunk #24
ခြား
Chunk #25
ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ စေ " အဲ ဒီ သူ တွေ ကို တိုက် ခိုက်
Chunk #26
နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ မှာ ရှိ တဲ့ ဘီ ဘီ စီ
Chunk #27
ယူ
Chunk #28
က ရိန်း ရဲ့ သ
Chunk #29
တင်း
Chunk #30
ရင်း မြစ်
Chunk #31
တွေ က အ တည် ပြု ပြော ပါ တယ် ။ အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ
Chunk #32
က
Chunk #33
ရိန်း နယ်
Chunk #34
မြေ
Chunk #35
တွေ
Chunk #36
၊
Chunk #37
ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ်
Chunk #38
။
Chunk #39
စ
Chunk #40
ကူ တာ လေး ထဲ မှာ ထည့် ထား ပုံ
Chunk #41
ရ
Chunk #42
တဲ့
Chunk #43
ဗုံး
Chunk #44
နဲ့
Chunk #45
ရု ရှား ဒု တိ ယ ဗိုလ် ချုပ်
Chunk #46
ကြီး
Chunk #47
အစ်
Chunk #48
ဂေါ
Chunk #49
ကီ လီ လော့ဗ်
Chunk #50
ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ
Chunk #51
တွင်း
Chunk #52
မှာ
Chunk #53
မော့
Chunk #54
ဆက် အ ဖွဲ့
Chunk #55
က
Chunk #56
ပေ
Chunk #57
ဂျာ တွေ
Chunk #58
နဲ့
Chunk #59
ဟစ်ဇ်
Chunk #60
ဘို
Chunk #61
လာ တို့ ကို တိုက် ခိုက်
Chunk #62
ပုံ
Chunk #63
နဲ့
Chunk #64
နှိုင်း
Chunk #65
ယှ
Chunk #66
ဥ် နိုင် တယ် လို့
Chunk #67
ယူ
Chunk #68
က ရိန်း လုံ ခြုံ ရေး ဌာ န
Chunk #69
(
Chunk #70
Security
Chunk #71
Service
Chunk #72
of
Chunk #73
Ukraine
Chunk #74
-
Chunk #75
SBU ) က အ ရာ
Chunk #76
ရှိ
Chunk #77
ဟောင်း
Chunk #78
အိုင်
Chunk #79
ဗင်
Chunk #80
စ
Chunk #81
တု
Chunk #82
ပက်ခ် က ပြော ပါ တယ်
Chunk #83
။ " သူ့ ကို ပစ် သတ် မ
Chunk #84
လား
Chunk #85
၊
Chunk #86
ဗုံး နဲ့ တိုက် ခိုက် မ လား
Chunk #87
၊
Chunk #88
အ
Chunk #89
ဆိပ်
Chunk #90
ပေး မ လား ဆို တာ ကို
Chunk #91
ယူ
Chunk #92
က ရိန်း လျှို့ ဝှက်
Chunk #93
ထောက် လှမ်း ရေး ဌာ န က ဆုံး ဖြတ်
Chunk #94
တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ
Chunk #95
က
Chunk #96
ရိန်း
Chunk #97
အ စိုး ရ အာ ဏာ ပိုင် တွေ က တ ရား ဝင် မှတ် ချက် ချ တာ မျိုး မ ရှိ ပါ ဘူး ။
အ စိုး ရ အာ ဏာ ပိုင် တွေ က တ ရား ဝင် မှတ် ချက် ချ တာ မျိုး မ ရှိ ပါ ဘူး ။
Chunks saved to chunk5.txt

real    0m2.071s
user    0m4.497s
sys     0m3.596s
(base) ye@lst-gpu-server-197:~/ye/exp/sem-chunk$
```

check chunked output file (chunk5.txt):  

```
' တိုက်
ပွဲ
ဝင်
ခြင်
တွေ
'
နဲ့
စ
ကူ
တာ
ဗုံး
-
မော် စ ကို အ ထိ ရောက် နေ တဲ့
ယူ
က ရိန်း
ထောက် လှမ်း
ရေး
ယူ
က ရိန်း လုံ ခြုံ ရေး
နဲ့
ထောက် လှမ်း ရေး ဌာ န
က အေး ဂျင့် တွေ ဟာ စစ် ပွဲ မှာ ပါ ဝင် တဲ့ ရု ရှား စစ် တပ်
ထိပ် ပိုင်း အ ရာ ရှိ တွေ နဲ့ တ
ခြား
ထိပ် ပိုင်း အ ရာ ရှိ တွေ " ဘယ် နေ ရာ မှာ ရှိ နေ ပါ စေ " အဲ ဒီ သူ တွေ ကို တိုက် ခိုက်
နေ ကြောင်း အဲ ဒီ ဌာ န ထဲ မှာ ရှိ တဲ့ ဘီ ဘီ စီ
ယူ
က ရိန်း ရဲ့ သ
တင်း
ရင်း မြစ်
တွေ က အ တည် ပြု ပြော ပါ တယ် ။ အဲ ဒီ နေ ရာ တွေ ထဲ မှာ သိမ်း ပိုက် ခံ ယူ
က
ရိန်း နယ်
မြေ
တွေ
၊
ရု ရှား နဲ့ တ ခြား နိုင် ငံ ရပ် ခြား တွေ ပါ ဝင် ပါ တယ်
။
စ
ကူ တာ လေး ထဲ မှာ ထည့် ထား ပုံ
ရ
တဲ့
ဗုံး
နဲ့
ရု ရှား ဒု တိ ယ ဗိုလ် ချုပ်
ကြီး
အစ်
ဂေါ
ကီ လီ လော့ဗ်
ကို တိုက် ခိုက် သတ် ဖြတ် လိုက် တာ ဟာ ပြီး ခဲ့ တဲ့ လ ပိုင်း တွေ အ
တွင်း
မှာ
မော့
ဆက် အ ဖွဲ့
က
ပေ
ဂျာ တွေ
နဲ့
ဟစ်ဇ်
ဘို
လာ တို့ ကို တိုက် ခိုက်
ပုံ
နဲ့
နှိုင်း
ယှ
ဥ် နိုင် တယ် လို့
ယူ
က ရိန်း လုံ ခြုံ ရေး ဌာ န
(
Security
Service
of
Ukraine
-
SBU ) က အ ရာ
ရှိ
ဟောင်း
အိုင်
ဗင်
စ
တု
ပက်ခ် က ပြော ပါ တယ်
။ " သူ့ ကို ပစ် သတ် မ
လား
၊
ဗုံး နဲ့ တိုက် ခိုက် မ လား
၊
အ
ဆိပ်
ပေး မ လား ဆို တာ ကို
ယူ
က ရိန်း လျှို့ ဝှက်
ထောက် လှမ်း ရေး ဌာ န က ဆုံး ဖြတ်
တာ ပါ " လို့ သူ က ပြော ပါ တယ် ။ ဒီ အ ဖြစ် နဲ့ ပတ် သက် ပြီး ယူ
က
ရိန်း
အ စိုး ရ အာ ဏာ ပိုင် တွေ က တ ရား ဝင် မှတ် ချက် ချ တာ မျိုး မ ရှိ ပါ ဘူး ။

```

## Test Commands  

Test လုပ်ခဲ့တဲ့ command တွေကို reference ပြန်လုပ်ခဲ့...  

```bash
#!/bin/bash

## Test commands run by Ye, LU Lab., Myanmar
## Date: 24 Dec 2024

## Test-1
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances-eg1 --chunk_filename chunk1.txt

## Test-2
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances-eg2 --chunk_filename chunk2.txt --percentile_threshold 40

## Test-3
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances-eg3 --chunk_filename chunk3.txt --percentile_threshold 30 --y_upper_bound 0.5

## Test-4
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances-eg4 --chunk_filename chunk4.txt --percentile_threshold 70 --y_upper_bound 0.5 --syllable_group_length 5

## Test-5
time python ./semantic_chunk.py --model ./model/myfasttext_v1.bin --input ./test1.syl \
--graph_filename distances-eg5 --chunk_filename chunk5.txt --percentile_threshold 70 --y_upper_bound 0.5 --syllable_group_length 1

```

## Conclusion  

Experiment အောင်မြင်တယ်။  
Syllable ဖြတ်ထားတာတွေကို ပြန်ပူးပေးချင်ရင်လည်း ပေးလို့ ရတယ်။  
percentile အစား တခြား approach တွေလည်း သုံးလို့ ရလိမ့်မယ်။    

## Reference

The 5 Levels Of Text Splitting For Retrieval by Greg Kamradt, (Accessed date: 23 Dec 2024):  
https://www.youtube.com/watch?v=8OJC21T2SL4&t=2112s    

Test Data that I used, article: 'တိုက်ပွဲဝင် ခြင်တွေ'နဲ့ စကူတာဗုံး - မော်စကိုအထိရောက်နေတဲ့ ယူကရိန်းထောက်လှမ်းရေး,  
https://www.bbc.com/burmese/articles/crl35en7nz3o    
