# sequence to Sequence Modeling for Myanmar Sentence Segmentation

## Prepare a Training Script

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, Affiliated Professor, CADT, Cambodia
## for NMT Experiments between Burmese dialects
## used Marian NMT Framework for seq2seq training
## Last updated: 30 May 2022

## Reference: https://marian-nmt.github.io/examples/mtm2017/complex/

model_folder="model.seq2seq.sent1";
mkdir ${model_folder};
data_path="/home/ye/exp/mysent/data-sent";
src="my"; tgt="tg";


marian \
  --type s2s \
  --train-sets ${data_path}/train.${src} ${data_path}/train.${tgt} \
  --max-length 200 \
  --valid-sets ${data_path}/dev.${src} ${data_path}/dev.${tgt} \
  --vocabs  ${data_path}/vocab/vocab.${src}.yml  ${data_path}/vocab/vocab.${tgt}.yml \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --model ${model_folder}/model.npz \
  --workspace 4500 \
  --enc-depth 3 --enc-type alternating --enc-cell lstm --enc-cell-depth 4 \
  --dec-depth 3 --dec-cell lstm --dec-cell-base-depth 4 --dec-cell-high-depth 2 \
  --tied-embeddings --layer-normalization --skip \
  --mini-batch-fit \
  --valid-mini-batch 32 \
  --valid-metrics cross-entropy perplexity bleu\
  --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
  --dropout-rnn 0.3 --dropout-src 0.3 --exponential-smoothing \
  --early-stopping 10 \
  --log ${model_folder}/train.log --valid-log ${model_folder}/valid.log \
  --devices 0 --sync-sgd --seed 1111  \
  --dump-config > ${model_folder}/config.yml

time marian -c ${model_folder}/config.yml  2>&1 | tee ${model_folder}/s2s.${src}-${tgt}.log1
```

## Training and Got Error as Usual

```
[CALL STACK]
[0x55efa8ee47d7]    marian::io::InputFileStream::  InputFileStream  (std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>> const&) + 0xaf7
[0x55efa8f3a45f]    marian::data::CorpusBase::  CorpusBase  (std::vector<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>,std::allocator<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>>> const&,  std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>> const&,  std::shared_ptr<marian::Options>,  unsigned long) + 0xb9f
[0x55efa8f4f198]    marian::data::Corpus::  Corpus  (std::vector<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>,std::allocator<std::__cxx11::basic_string<char,std::char_traits<char>,std::allocator<char>>>>,  std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>>,  std::shared_ptr<marian::Options>,  unsigned long) + 0x78
[0x55efa9313395]    marian::CrossEntropyValidator::  CrossEntropyValidator  (std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>>,  std::shared_ptr<marian::Options>) + 0x185
[0x55efa9316785]    marian::  Validators  (std::vector<std::shared_ptr<marian::Vocab>,std::allocator<std::shared_ptr<marian::Vocab>>>,  std::shared_ptr<marian::Options>) + 0x845
[0x55efa8e2845f]    marian::Train<marian::SyncGraphGroup>::  run  ()   + 0x17df
[0x55efa8d56347]    mainTrainer  (int,  char**)                        + 0x147
[0x7f8b0b0eed90]                                                       + 0x29d90
[0x7f8b0b0eee40]    __libc_start_main                                  + 0x80
[0x55efa8d4f995]    _start                                             + 0x25


real    0m53.890s
user    0m51.347s
sys     0m1.942s
root@2328f1decde9:/home/ye/exp/mysent# ./seq2seq.sent1.sh
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
