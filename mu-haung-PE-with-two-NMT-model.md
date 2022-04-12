# MuHaung Post Editing with Two NMT Models

## Preparation

Post-Editing အတွက် training data တစ်ခုလုံးကို translation လုပ်ပြီး machine-translation output training data ကို ဖန်တီးမယ်။  

for my-br testing, tran-eval-traindata-mybr.sh:  

```bash
#!/bin/bash

## Preparation for Post-Editing with two NMT Models
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with TRAINING-DATA, Marian, Transformer Model, for my-br
## 12 April 2022

marian-decoder -m ./model0-mybr.iter95000.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter95000-trainingdata.br < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my
echo "Evaluation with hyp.iter95000-trainingdata.br, Best Transformer Model:" >> test-train0-mybr-results.txt
perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br < ./hyp.iter95000-trainingdata.br  >> test-train0-mybr-results.txt

```

for br-my testing:  

```bash

```

## Translating Myanmar Training Data

Translating the whole training-set:  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer$ time ./tran-eval-traindata-mybr.sh
...
...
...
[2022-04-12 21:02:47] Best translation 16386 : ⠼⠙ ⠲ ⠹⠣⠃⠔ ⠰⠶ ⠣⠎⠥⠂⠣⠺⠱⠆ ⠲
[2022-04-12 21:02:47] Best translation 16387 : ⠏⠋⠆ ⠇⠑⠈⠶ ⠲
[2022-04-12 21:02:47] Best translation 16388 : ⠎⠣⠅⠁⠆⠿⠱ ⠣⠗⠱⠆⠣⠹⠁⠆ ⠩⠱⠂⠈⠶ ⠇⠋⠆⠿⠣⠾ ⠲
[2022-04-12 21:02:47] Best translation 16389 : ⠣⠸⠣⠥⠩⠔ ⠗ ⠗⠺⠁⠹⠥⠗⠺⠁⠹⠁⠆ ⠚ ⠇⠆ ⠁⠆⠗⠣⠏⠁⠆⠗⠣ ⠗⠮⠍⠻⠆ ⠟⠣ ⠃ ⠹⠞ ⠲
[2022-04-12 21:02:48] Best translation 16390 : ⠼⠂ ⠝⠴ ⠰⠣⠣ ⠾⠋⠍⠁ ⠚ ⠈⠑⠨⠋⠯ ⠅⠣⠿⠣ ⠇⠁ ⠨⠮⠂ ⠟⠣ ⠡ ⠿⠓ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠣⠅⠣ ⠹⠏⠔ ⠾⠋⠍⠁ ⠇⠥⠾⠕⠆ ⠚ ⠊ ⠣⠾⠔⠂⠈⠉⠆ ⠹⠻⠆ ⠣⠈⠔⠂⠣⠞⠋⠆ ⠺⠔ ⠣⠝⠥⠂⠏⠔⠷⠁ ⠚ ⠏⠩ ⠹⠻⠆ ⠣⠅⠣ ⠏⠔⠷⠁⠗⠣⠞ ⠓ ⠹⠣⠞⠰⠣⠣⠞ ⠨⠮⠂ ⠟ ⠃ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16391 : ⠍⠋⠞⠣⠇⠱⠆ ⠙⠖⠽⠁⠍⠪⠅⠔⠃⠽⠭ ⠎⠑⠗⠉ ⠹ ⠩⠱⠆ ⠅⠣ ⠱⠝⠩⠱⠂⠅⠕⠞⠻⠟⠪⠆ ⠊ ⠇⠑⠝⠑ ⠗⠉ ⠭ ⠨⠮⠂ ⠊ ⠲
[2022-04-12 21:02:48] Best translation 16392 : ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠲
[2022-04-12 21:02:48] Best translation 16393 : ⠟⠋⠎⠪ ⠲
[2022-04-12 21:02:48] Best translation 16394 : ⠱⠆⠎⠢⠂ ⠝⠱ ⠹⠻⠆ ⠝⠋⠝⠑ ⠹⠣⠃⠁⠺⠣ ⠗ ⠞⠱⠅⠈⠱⠅ ⠷⠢⠹⠑ ⠡ ⠚ ⠅⠣ ⠨⠣⠗⠪⠆⠁⠺⠑ ⠡ ⠅ ⠣⠗⠣⠹⠁ ⠞⠭⠾⠕⠆ ⠭⠎ ⠏ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16395 : ⠥⠆⠃⠣⠷⠋ ⠅⠁⠆ ⠺⠁⠹⠣⠝⠁ ⠣⠗⠔⠆⠨⠋ ⠵ ⠏⠋⠆⠡⠪ ⠏⠔⠷⠁ ⠞⠺ ⠟⠻⠟⠁⠆ ⠨⠮⠂ ⠹⠥ ⠭ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16396 : ⠞⠣⠍⠁⠏⠔ ⠲
[2022-04-12 21:02:48] Best translation 16397 : ⠟⠴⠹⠔⠏⠉⠆ ⠞⠦⠅⠴ ⠾⠴ ⠌⠁⠆ ⠡⠴ ⠲
[2022-04-12 21:02:48] Best translation 16398 : ⠼ ⠣⠇⠔⠅⠁⠾ ⠹ ⠹⠑⠈⠖⠗⠁ ⠎⠣⠅⠁⠆⠿⠱ ⠅ ⠍⠙ ⠍⠏⠉ ⠣⠁⠴⠣⠅⠥ ⠿⠥⠂ ⠝⠱ ⠟⠶⠆ ⠈⠑⠎⠣⠞ ⠇⠱⠂⠇⠁ ⠞⠣⠞ ⠶ ⠁⠆⠁⠦ ⠹⠔⠂ ⠏ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16399 : ⠅⠉⠆ ⠏⠋ ⠇⠕⠂ ⠡⠁⠆⠡⠁⠆ ⠲
[2022-04-12 21:02:48] Best translation 16400 : ⠇⠱⠂⠟⠔⠂⠨⠋⠆ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠲
[2022-04-12 21:02:48] Best translation 16401 : ⠶ ⠛⠣ ⠶ ⠍⠶⠾⠔⠂ ⠅ ⠣⠃⠮⠳ ⠹⠥⠌⠮⠡⠔⠆⠅⠶⠆ ⠏⠪⠹⠣ ⠹⠓ ⠨⠻⠈⠕ ⠼⠬ ⠹⠝ ⠲
[2022-04-12 21:02:48] Best translation 16402 : ⠛⠣⠲
[2022-04-12 21:02:48] Best translation 16403 : ⠼⠉ ⠲ ⠍⠣⠓⠻⠹⠣⠙⠁ ⠝⠺⠁⠆ ⠞⠽ ⠎⠪ ⠗⠔⠏⠉ ⠿⠣⠵⠣⠞ ⠅ ⠟⠪⠂ ⠿⠪⠆ ⠍⠙ ⠨⠋⠎⠁⠆ ⠗⠣ ⠹⠝ ⠲
[2022-04-12 21:02:48] Best translation 16404 : ⠼⠁ ⠲ ⠴⠏⠁ ⠣⠡⠑⠾ ⠏⠻ ⠍⠥⠞⠮ ⠿⠪⠆ ⠵⠣⠽⠁⠆ ⠞⠺ ⠿⠓⠱⠂ ⠏ ⠲
[2022-04-12 21:02:48] Best translation 16405 : ⠞⠭⠝⠱⠂ ⠞⠺ ⠍⠔⠆⠟⠪⠆ ⠅⠣ ⠣⠍⠶ ⠇⠥⠂⠇⠔ ⠒ ⠪ ⠣⠞⠣⠞⠏⠔⠷⠁ ⠅ ⠣⠃⠮ ⠈⠣⠗⠁⠂ ⠁⠋ ⠞⠺ ⠇⠱⠂⠇⠁ ⠈⠪⠆⠏⠥⠆ ⠨⠮⠂ ⠹⠝ ⠲
[2022-04-12 21:02:48] Best translation 16406 : ⠥⠆⠘⠕⠆⠟⠁⠆ ⠹ ⠙⠥⠂⠞⠊⠽⠣ ⠅⠋⠃⠁⠎⠭ ⠣⠞⠺⠔⠆ ⠎⠭⠿⠱⠆ ⠗⠔⠆ ⠾⠋⠍⠁ ⠠⠣⠭ ⠼⠁ ⠉ ⠚ ⠉ ⠨⠥⠂ ⠶ ⠅⠗ ⠠⠣⠭ ⠼⠁ ⠊ ⠙ ⠃ ⠶ ⠞⠺ ⠁⠋⠆⠞⠣⠏⠔ ⠾⠕⠂ ⠫ ⠅⠺⠮⠇⠥⠝ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16407 : ⠹⠥ ⠺⠁⠹⠣⠝⠁ ⠏⠁ ⠗⠁ ⠒ ⠾⠣⠞⠝⠕⠆ ⠗⠁ ⠏⠋⠆⠡⠪ ⠣⠇⠦ ⠅ ⠇⠦ ⠱ ⠗⠣ ⠸ ⠣⠇⠥⠝ ⠟⠱⠝⠣⠞ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16408 : ⠞⠣⠞⠊⠽⠣ ⠠⠣⠭ ⠟⠣⠞⠻⠂ ⠇⠆ ⠓⠕⠓⠕⠙⠪⠙⠪ ⠈⠕⠯ ⠏⠱⠆ ⠇⠬ ⠗⠣⠞⠁ ⠅⠣ ⠌⠺⠱ ⠡⠴ ⠁⠶ ⠲
[2022-04-12 21:02:48] Best translation 16409 : ⠱⠅⠗⠁ ⠰⠣⠣ ⠁⠣⠯ ⠍⠣⠟⠁⠍⠪ ⠰⠣⠁ ⠏⠔ ⠣⠝⠪⠆⠣⠝⠁⠆ ⠩ ⠃⠉⠆⠟⠪⠆⠟⠶⠆ ⠰⠣⠣ ⠅⠣⠇⠣⠞⠑⠹⠋ ⠅ ⠟⠁⠆ ⠗⠣ ⠃ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16410 : ⠣⠍⠮⠆⠹⠁⠆ ⠌⠁⠆⠾ ⠋ ⠏⠦ ⠋ ⠹⠕⠆ ⠃⠮⠆ ⠞⠁⠩⠱⠨⠋ ⠶ ⠎⠓⠁⠆ ⠿⠓ ⠿⠥⠂⠿⠔ ⠞⠓⠁⠆ ⠝ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16411 : ⠏⠁⠝⠪ ⠇⠆ ⠇⠁ ⠞⠮ ⠩ ⠞⠮ ⠲
[2022-04-12 21:02:48] Best translation 16412 : ⠼⠃ ⠲ ⠈⠑⠎⠣⠞ ⠰⠶ ⠞⠭ ⠨⠥⠂ ⠗ ⠞⠭ ⠨⠥⠂ ⠏⠥⠆⠏⠶⠆ ⠹ ⠲ ⠈⠑⠝⠺⠮ ⠹ ⠲
[2022-04-12 21:02:48] Best translation 16413 : ⠚⠔ ⠏⠮⠂ ⠡⠔⠆ ⠏⠴ ⠟⠣⠎⠕⠂ ⠲
[2022-04-12 21:02:48] Best translation 16414 : ⠶ ⠗⠥⠞⠈⠕⠗⠋ ⠶ ⠲
[2022-04-12 21:02:48] Total time: 451.43179s wall

real	7m36.136s
user	14m46.195s
sys	0m16.659s
```
