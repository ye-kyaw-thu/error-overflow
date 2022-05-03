# XNMT Medical Domain Experiment with SwitchOut

## Check the Example Config

```yaml
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ cat ./examples/22_switchout.yaml 
# Implements SwitchOut, a data augmentation strategy for NMT
# RAML corrupts target side only, while SwitchOut corrupts both source and target
# https://arxiv.org/pdf/1808.07512.pdf 
switchout: !Experiment 
  # global parameters shared throughout the experiment
  exp_global: !ExpGlobal
    # {EXP_DIR} is a placeholder for the directory in which the config file lies.
    # {EXP} is a placeholder for the experiment name (here: 'standard')
    model_file: '{EXP_DIR}/models/{EXP}.mod'
    log_file: '{EXP_DIR}/logs/{EXP}.log'
    default_layer_dim: 512
    dropout: 0.3
  # model architecture
  model: !DefaultTranslator
    src_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: examples/data/head.ja.vocab}
      tau: 0.8
    trg_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: examples/data/head.en.vocab}
      tau: 0.8
    src_embedder: !SimpleWordEmbedder
      emb_dim: 512
    encoder: !BiLSTMSeqTransducer
      layers: 1
    attender: !MlpAttender
      hidden_dim: 512
      state_dim: 512
      input_dim: 512
    decoder: !AutoRegressiveDecoder
      embedder: !SimpleWordEmbedder
        emb_dim: 512
      rnn: !UniLSTMSeqTransducer
        layers: 1
      transform: !AuxNonLinear
        output_dim: 512
        activation: 'tanh'
      bridge: !CopyBridge {}
      scorer: !Softmax {}
  # training parameters
  train: !SimpleTrainingRegimen
    batcher: !SrcBatcher
      batch_size: 32
    trainer: !AdamTrainer
      alpha: 0.001
    run_for_epochs: 2
    src_file: examples/data/head.ja
    trg_file: examples/data/head.en
    dev_tasks:
      - !LossEvalTask
        src_file: examples/data/head.ja
        ref_file: examples/data/head.en
  # final evaluation
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu
      src_file: examples/data/head.ja
      ref_file: examples/data/head.en
      hyp_file: examples/output/{EXP}.test_hyp
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$
```

## Test Run with Example Config

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ time xnmt --backend torch --gpu ./examples/22_switchout.yaml | tee switchout-tst.log
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 14:02:43
=> Running switchout
> use randomly initialized neural network parameters for all components
  neural network param count: 5884997
> Training
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/xnmt-0.0.1-py3.6.egg/xnmt/batchers.py:184: UserWarning: The given NumPy array is not writeable, and PyTorch does not support non-writeable tensors. This means you can write to the underlying (supposedly non-writeable) NumPy array using the tensor. You may want to copy the array to protect its data or make it writeable before converting it to a tensor. This type of warning will be suppressed for the rest of this program. (Triggered internally at  /opt/conda/conda-bld/pytorch_1639180593867/work/torch/csrc/utils/tensor_numpy.cpp:189.)
ERROR:   mask_exp = torch.as_tensor(self.np_arr[:, timestep:timestep + 1], dtype=expr.dtype, device=xnmt.device)
ERROR: /home/ye/anaconda3/envs/xnmt-py3.6/lib/python3.6/site-packages/torch/optim/lr_scheduler.py:134: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
ERROR:   "https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate", UserWarning)
[switchout] Epoch 1.0000: train_loss/word=4.700846 (steps=1, words/sec=219.63, time=0-00:00:00)
> Checkpoint [switchout]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[switchout] Epoch 1.0000 dev Loss: 4.603 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[switchout] Epoch 2.0000: train_loss/word=4.627975 (steps=2, words/sec=2247.22, time=0-00:00:00)
> Checkpoint [switchout]
Starting to read examples/data/head.ja and examples/data/head.en
Done reading examples/data/head.ja and examples/data/head.en. Packing into batches.
Done packing batches.
[switchout] Epoch 2.0000 dev Loss: 4.493 (ref_len=91) (time=0-00:00:00)
             checkpoint took 0-00:00:00
  best dev score, writing out model
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on examples/data/head.ja and examples/data/head.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout                     | BLEU4: 0.0, 0.555556/0.000000/0.000000/0.000000 (BP = 0.000110, ratio=0.10, hyp_len=9, ref_len=91)

real	0m4.480s
user	0m3.851s
sys	0m1.513s
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt$ 

```

## Data Preparation

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ mkdir syl_switchout
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ mkdir word_switchout
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ cp ./syl/data/ ./syl_switchout/ -r
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1$ cp ./word/data/ ./word_switchout/ -r
```

## Updating Config File for Word Unit (en-my)

```yaml
# standard settings
switchout.en-my: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.en'
      - '{EXP_DIR}/data/train.my'
      out_files:
      - '{EXP_DIR}/vocab.en'
      - '{EXP_DIR}/vocab.my'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
      tau: 0.8      
    trg_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.my'}
      tau: 0.8      
    src_embedder: !SimpleWordEmbedder   # Embed source words as 256 dimensional vectors
      emb_dim: 512
    encoder: !ResidualSeqTransducer
      child: !BiLSTMSeqTransducer
        layers: 2
    attender: !MlpAttender {}
    decoder: !AutoRegressiveDecoder
      embedder: !DenseWordEmbedder      # Represent target words as a 40000x256 matrix
        emb_dim: 512
      bridge: !LinearBridge {}          # Initialize the first state of the decoder with an affine transform of the last state of the encoder
      rnn: !UniLSTMSeqTransducer        # Just your standard LSTM decoder
        layers: 2                       # With 2 layers
      transform: !AuxNonLinear
        output_dim: !Ref
          path: model.decoder.embedder.emb_dim
        activation: 'relu'
      scorer: !Softmax
        output_projector: !Ref
          path: model.decoder.embedder      # Tie the softmax output to the target word embeddings
        label_smoothing: 0.1              # Smooth the output labels with the uniform distribution
    inference: !AutoRegressiveInference
      search_strategy: !BeamSearch
        beam_size: 5
        len_norm: !PolynomialNormalization
          apply_during_search: true
          m: 0.8
  train: !SimpleTrainingRegimen
    run_for_epochs: 30  # Run for at most 20 epochs
    initial_patience: 2 # Run for at least 2 epochs without decreasing the learning rate
    patience: 1         # After there is no improvement for 1 epoch, decrease the learning rate
    lr_decay: 0.5       # Decay the learning rate by half whenever there is no improvement
    lr_decay_times: 2   # If there is still no improvement after decreasing the learning rate 2 times in a row, stop training
    trainer: !AdamTrainer
      alpha: 0.001
    batcher: !WordSrcBatcher
      avg_batch_size: 64
    src_file: '{EXP_DIR}/data/train.en'
    trg_file: '{EXP_DIR}/data/train.my'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.en'
        ref_file: &dev_trg '{EXP_DIR}/data/dev.my'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.my'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.my'
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: &test_src '{EXP_DIR}/data/test.en'
      ref_file: &test_trg '{EXP_DIR}/data/test.my'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.my'
```

## Training for Word-SwitchOut (en-my)

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$ time xnmt --backend torch --gpu ./config.switchout.en-my-word.yaml | tee switchout.en-my.log1
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 14:45:35
=> Running switchout.en-my
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 22454378
> Training
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 0.0739: train_loss/word=8.723841 (steps=21, words/sec=7448.40, time=0-00:00:07)
[switchout.en-my] Epoch 0.1496: train_loss/word=7.516871 (steps=43, words/sec=9582.27, time=0-00:00:09)
[switchout.en-my] Epoch 0.2252: train_loss/word=7.404384 (steps=64, words/sec=9171.66, time=0-00:00:11)
[switchout.en-my] Epoch 0.3009: train_loss/word=7.242526 (steps=86, words/sec=10442.14, time=0-00:00:13)
[switchout.en-my] Epoch 0.3746: train_loss/word=7.188582 (steps=110, words/sec=9375.36, time=0-00:00:15)
[switchout.en-my] Epoch 0.4519: train_loss/word=7.178165 (steps=130, words/sec=10687.95, time=0-00:00:17)
[switchout.en-my] Epoch 0.5277: train_loss/word=7.030050 (steps=150, words/sec=10637.92, time=0-00:00:18)
[switchout.en-my] Epoch 0.6033: train_loss/word=6.967326 (steps=173, words/sec=9985.06, time=0-00:00:20)
[switchout.en-my] Epoch 0.6771: train_loss/word=6.841437 (steps=191, words/sec=12116.21, time=0-00:00:22)
[switchout.en-my] Epoch 0.7540: train_loss/word=6.737395 (steps=217, words/sec=9026.74, time=0-00:00:24)
[switchout.en-my] Epoch 0.8312: train_loss/word=6.639657 (steps=239, words/sec=10239.66, time=0-00:00:26)
[switchout.en-my] Epoch 0.9069: train_loss/word=6.625069 (steps=261, words/sec=9391.02, time=0-00:00:28)
[switchout.en-my] Epoch 0.9843: train_loss/word=6.510635 (steps=283, words/sec=10499.54, time=0-00:00:30)
[switchout.en-my] Epoch 1.0000: train_loss/word=6.473059 (steps=288, words/sec=8538.13, time=0-00:00:30)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 1.0000 dev BLEU4: 0.0022576921258563734, 0.028986/0.005336/0.001011/0.000166 (BP = 1.000000, ratio=4.86, hyp_len=37605, ref_len=7744) (time=0-00:02:32)
[switchout.en-my]              dev auxiliary GLEU: 0.008898
[switchout.en-my]              dev auxiliary Loss: 6.175 (ref_len=7744)
             checkpoint took 0-00:02:02
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 1.0039: train_loss/word=6.404499 (steps=289, words/sec=10643.77, time=0-00:02:58)
[switchout.en-my] Epoch 1.0811: train_loss/word=6.420670 (steps=313, words/sec=9120.92, time=0-00:03:00)
[switchout.en-my] Epoch 1.1595: train_loss/word=6.333354 (steps=336, words/sec=9790.04, time=0-00:03:02)
[switchout.en-my] Epoch 1.2335: train_loss/word=6.321980 (steps=357, words/sec=9310.16, time=0-00:03:04)
[switchout.en-my] Epoch 1.3072: train_loss/word=6.384337 (steps=377, words/sec=10424.26, time=0-00:03:05)
[switchout.en-my] Epoch 1.3843: train_loss/word=6.204682 (steps=398, words/sec=10750.06, time=0-00:03:07)
[switchout.en-my] Epoch 1.4582: train_loss/word=6.244721 (steps=421, words/sec=9729.09, time=0-00:03:09)
[switchout.en-my] Epoch 1.5350: train_loss/word=6.151536 (steps=442, words/sec=11625.42, time=0-00:03:11)
[switchout.en-my] Epoch 1.6134: train_loss/word=6.210247 (steps=462, words/sec=10714.34, time=0-00:03:12)
[switchout.en-my] Epoch 1.6875: train_loss/word=6.153826 (steps=484, words/sec=10167.56, time=0-00:03:14)
[switchout.en-my] Epoch 1.7613: train_loss/word=6.175680 (steps=507, words/sec=8499.89, time=0-00:03:16)
[switchout.en-my] Epoch 1.8378: train_loss/word=6.125551 (steps=531, words/sec=9716.72, time=0-00:03:18)
[switchout.en-my] Epoch 1.9132: train_loss/word=6.102367 (steps=553, words/sec=9188.99, time=0-00:03:20)
[switchout.en-my] Epoch 1.9868: train_loss/word=6.003304 (steps=574, words/sec=10226.91, time=0-00:03:22)
[switchout.en-my] Epoch 2.0000: train_loss/word=6.153741 (steps=577, words/sec=10941.58, time=0-00:03:22)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 2.0000 dev BLEU4: 0.011049108042477862, 0.085244/0.022346/0.005419/0.001444 (BP = 1.000000, ratio=2.61, hyp_len=20189, ref_len=7744) (time=0-00:04:34)
[switchout.en-my]              dev auxiliary GLEU: 0.027948
[switchout.en-my]              dev auxiliary Loss: 5.754 (ref_len=7744)
             checkpoint took 0-00:01:11
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 2.0032: train_loss/word=5.850168 (steps=578, words/sec=10403.66, time=0-00:04:43)
[switchout.en-my] Epoch 2.0791: train_loss/word=5.847983 (steps=600, words/sec=10675.36, time=0-00:04:45)
[switchout.en-my] Epoch 2.1549: train_loss/word=5.864891 (steps=619, words/sec=12681.08, time=0-00:04:46)
[switchout.en-my] Epoch 2.2315: train_loss/word=5.902731 (steps=640, words/sec=11754.98, time=0-00:04:48)
[switchout.en-my] Epoch 2.3079: train_loss/word=5.917770 (steps=666, words/sec=9018.38, time=0-00:04:50)
[switchout.en-my] Epoch 2.3835: train_loss/word=5.858398 (steps=686, words/sec=10730.76, time=0-00:04:52)
[switchout.en-my] Epoch 2.4595: train_loss/word=5.827458 (steps=708, words/sec=10308.56, time=0-00:04:54)
[switchout.en-my] Epoch 2.5355: train_loss/word=5.850230 (steps=729, words/sec=10900.60, time=0-00:04:55)
[switchout.en-my] Epoch 2.6112: train_loss/word=5.856258 (steps=749, words/sec=11602.47, time=0-00:04:57)
[switchout.en-my] Epoch 2.6867: train_loss/word=5.861828 (steps=772, words/sec=9621.24, time=0-00:04:59)
[switchout.en-my] Epoch 2.7603: train_loss/word=5.825612 (steps=793, words/sec=10259.15, time=0-00:05:01)
[switchout.en-my] Epoch 2.8360: train_loss/word=5.791001 (steps=815, words/sec=9838.09, time=0-00:05:03)
[switchout.en-my] Epoch 2.9098: train_loss/word=5.765051 (steps=837, words/sec=9471.93, time=0-00:05:05)
[switchout.en-my] Epoch 2.9847: train_loss/word=5.748295 (steps=858, words/sec=9875.08, time=0-00:05:06)
[switchout.en-my] Epoch 3.0000: train_loss/word=5.790373 (steps=863, words/sec=7863.34, time=0-00:05:07)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 3.0000 dev BLEU4: 0.04358847815831242, 0.260418/0.080281/0.024087/0.007168 (BP = 1.000000, ratio=1.09, hyp_len=8471, ref_len=7744) (time=0-00:05:41)
[switchout.en-my]              dev auxiliary GLEU: 0.088452
[switchout.en-my]              dev auxiliary Loss: 5.500 (ref_len=7744)
             checkpoint took 0-00:00:34
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 3.0057: train_loss/word=5.746877 (steps=864, words/sec=15623.90, time=0-00:05:50)
[switchout.en-my] Epoch 3.0825: train_loss/word=5.599231 (steps=884, words/sec=10664.99, time=0-00:05:52)
[switchout.en-my] Epoch 3.1581: train_loss/word=5.565133 (steps=905, words/sec=10551.19, time=0-00:05:54)
[switchout.en-my] Epoch 3.2347: train_loss/word=5.666036 (steps=923, words/sec=11211.35, time=0-00:05:55)
[switchout.en-my] Epoch 3.3083: train_loss/word=5.598091 (steps=945, words/sec=10433.69, time=0-00:05:57)
[switchout.en-my] Epoch 3.3852: train_loss/word=5.535604 (steps=966, words/sec=10562.67, time=0-00:05:58)
[switchout.en-my] Epoch 3.4595: train_loss/word=5.549147 (steps=989, words/sec=9102.36, time=0-00:06:01)
[switchout.en-my] Epoch 3.5361: train_loss/word=5.566792 (steps=1010, words/sec=10462.80, time=0-00:06:02)
[switchout.en-my] Epoch 3.6123: train_loss/word=5.578711 (steps=1034, words/sec=10009.51, time=0-00:06:04)
[switchout.en-my] Epoch 3.6861: train_loss/word=5.495679 (steps=1056, words/sec=10507.96, time=0-00:06:06)
[switchout.en-my] Epoch 3.7604: train_loss/word=5.638004 (steps=1079, words/sec=8717.00, time=0-00:06:08)
[switchout.en-my] Epoch 3.8356: train_loss/word=5.514635 (steps=1101, words/sec=9682.78, time=0-00:06:10)
[switchout.en-my] Epoch 3.9094: train_loss/word=5.571534 (steps=1123, words/sec=10150.22, time=0-00:06:12)
[switchout.en-my] Epoch 3.9865: train_loss/word=5.485918 (steps=1146, words/sec=10019.21, time=0-00:06:14)
[switchout.en-my] Epoch 4.0000: train_loss/word=5.493431 (steps=1151, words/sec=9836.90, time=0-00:06:15)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 4.0000 dev BLEU4: 0.0496754094102786, 0.280698/0.089469/0.028439/0.008526 (BP = 1.000000, ratio=1.13, hyp_len=8771, ref_len=7744) (time=0-00:06:50)
[switchout.en-my]              dev auxiliary GLEU: 0.099515
[switchout.en-my]              dev auxiliary Loss: 5.318 (ref_len=7744)
             checkpoint took 0-00:00:35
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 4.0035: train_loss/word=5.183984 (steps=1152, words/sec=12006.30, time=0-00:07:00)
[switchout.en-my] Epoch 4.0803: train_loss/word=5.375508 (steps=1172, words/sec=10474.44, time=0-00:07:01)
[switchout.en-my] Epoch 4.1561: train_loss/word=5.306403 (steps=1195, words/sec=10366.35, time=0-00:07:03)
[switchout.en-my] Epoch 4.2298: train_loss/word=5.327725 (steps=1215, words/sec=10434.52, time=0-00:07:05)
[switchout.en-my] Epoch 4.3036: train_loss/word=5.317661 (steps=1239, words/sec=9226.17, time=0-00:07:07)
[switchout.en-my] Epoch 4.3780: train_loss/word=5.279517 (steps=1264, words/sec=8553.08, time=0-00:07:09)
[switchout.en-my] Epoch 4.4541: train_loss/word=5.309467 (steps=1283, words/sec=11780.72, time=0-00:07:11)
[switchout.en-my] Epoch 4.5297: train_loss/word=5.364242 (steps=1307, words/sec=9314.20, time=0-00:07:13)
[switchout.en-my] Epoch 4.6059: train_loss/word=5.335232 (steps=1329, words/sec=10067.47, time=0-00:07:15)
[switchout.en-my] Epoch 4.6824: train_loss/word=5.373047 (steps=1351, words/sec=10442.04, time=0-00:07:17)
[switchout.en-my] Epoch 4.7574: train_loss/word=5.266347 (steps=1373, words/sec=9952.41, time=0-00:07:19)
[switchout.en-my] Epoch 4.8334: train_loss/word=5.245546 (steps=1395, words/sec=10072.86, time=0-00:07:20)
[switchout.en-my] Epoch 4.9115: train_loss/word=5.348156 (steps=1417, words/sec=9568.37, time=0-00:07:22)
[switchout.en-my] Epoch 4.9854: train_loss/word=5.267146 (steps=1435, words/sec=11984.48, time=0-00:07:24)
[switchout.en-my] Epoch 5.0000: train_loss/word=5.233847 (steps=1439, words/sec=10326.66, time=0-00:07:24)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 5.0000 dev BLEU4: 0.06678684394088219, 0.348726/0.123650/0.040392/0.012757 (BP = 0.972777, ratio=0.97, hyp_len=7536, ref_len=7744) (time=0-00:07:56)
[switchout.en-my]              dev auxiliary GLEU: 0.122856
[switchout.en-my]              dev auxiliary Loss: 5.154 (ref_len=7744)
             checkpoint took 0-00:00:32
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 5.0055: train_loss/word=5.622667 (steps=1440, words/sec=11151.81, time=0-00:08:06)
[switchout.en-my] Epoch 5.0801: train_loss/word=5.108628 (steps=1459, words/sec=11411.63, time=0-00:08:07)
[switchout.en-my] Epoch 5.1560: train_loss/word=5.052308 (steps=1481, words/sec=9465.28, time=0-00:08:09)
[switchout.en-my] Epoch 5.2304: train_loss/word=5.098566 (steps=1502, words/sec=9941.88, time=0-00:08:11)
[switchout.en-my] Epoch 5.3049: train_loss/word=5.111122 (steps=1526, words/sec=9018.06, time=0-00:08:13)
[switchout.en-my] Epoch 5.3807: train_loss/word=5.111317 (steps=1547, words/sec=9449.41, time=0-00:08:15)
[switchout.en-my] Epoch 5.4557: train_loss/word=5.134463 (steps=1568, words/sec=10667.77, time=0-00:08:17)
[switchout.en-my] Epoch 5.5303: train_loss/word=5.096799 (steps=1591, words/sec=9710.12, time=0-00:08:19)
[switchout.en-my] Epoch 5.6048: train_loss/word=5.091357 (steps=1613, words/sec=10281.35, time=0-00:08:21)
[switchout.en-my] Epoch 5.6795: train_loss/word=5.097136 (steps=1633, words/sec=11604.05, time=0-00:08:22)
[switchout.en-my] Epoch 5.7543: train_loss/word=5.121377 (steps=1651, words/sec=11444.05, time=0-00:08:24)
[switchout.en-my] Epoch 5.8283: train_loss/word=5.086330 (steps=1676, words/sec=9031.14, time=0-00:08:26)
[switchout.en-my] Epoch 5.9060: train_loss/word=5.074510 (steps=1697, words/sec=11181.47, time=0-00:08:27)
[switchout.en-my] Epoch 5.9808: train_loss/word=5.067679 (steps=1720, words/sec=10276.01, time=0-00:08:29)
[switchout.en-my] Epoch 6.0000: train_loss/word=5.076757 (steps=1727, words/sec=7521.12, time=0-00:08:30)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 6.0000 dev BLEU4: 0.08487246734045625, 0.358628/0.137857/0.050816/0.020654 (BP = 1.000000, ratio=1.03, hyp_len=7986, ref_len=7744) (time=0-00:09:04)
[switchout.en-my]              dev auxiliary GLEU: 0.136958
[switchout.en-my]              dev auxiliary Loss: 5.042 (ref_len=7744)
             checkpoint took 0-00:00:33
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 6.0027: train_loss/word=4.807608 (steps=1728, words/sec=9919.31, time=0-00:09:13)
[switchout.en-my] Epoch 6.0795: train_loss/word=4.875355 (steps=1749, words/sec=11281.18, time=0-00:09:14)
[switchout.en-my] Epoch 6.1546: train_loss/word=5.015319 (steps=1768, words/sec=9139.61, time=0-00:09:16)
[switchout.en-my] Epoch 6.2298: train_loss/word=4.920124 (steps=1792, words/sec=9633.70, time=0-00:09:18)
[switchout.en-my] Epoch 6.3057: train_loss/word=4.945467 (steps=1814, words/sec=10527.93, time=0-00:09:20)
[switchout.en-my] Epoch 6.3815: train_loss/word=4.964402 (steps=1835, words/sec=9305.19, time=0-00:09:22)
[switchout.en-my] Epoch 6.4590: train_loss/word=4.870002 (steps=1856, words/sec=11363.54, time=0-00:09:24)
[switchout.en-my] Epoch 6.5349: train_loss/word=4.973717 (steps=1880, words/sec=8993.56, time=0-00:09:26)
[switchout.en-my] Epoch 6.6103: train_loss/word=4.874707 (steps=1902, words/sec=10292.22, time=0-00:09:28)
[switchout.en-my] Epoch 6.6876: train_loss/word=4.903983 (steps=1924, words/sec=10719.76, time=0-00:09:29)
[switchout.en-my] Epoch 6.7618: train_loss/word=4.880374 (steps=1945, words/sec=11038.74, time=0-00:09:31)
[switchout.en-my] Epoch 6.8381: train_loss/word=4.909216 (steps=1969, words/sec=9639.28, time=0-00:09:33)
[switchout.en-my] Epoch 6.9118: train_loss/word=4.871389 (steps=1988, words/sec=11940.61, time=0-00:09:35)
[switchout.en-my] Epoch 6.9861: train_loss/word=4.861709 (steps=2011, words/sec=10294.11, time=0-00:09:36)
[switchout.en-my] Epoch 7.0000: train_loss/word=4.828157 (steps=2015, words/sec=11123.16, time=0-00:09:37)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 7.0000 dev BLEU4: 0.0908703205828449, 0.370375/0.149084/0.056956/0.021681 (BP = 1.000000, ratio=1.02, hyp_len=7865, ref_len=7744) (time=0-00:10:09)
[switchout.en-my]              dev auxiliary GLEU: 0.140801
[switchout.en-my]              dev auxiliary Loss: 4.947 (ref_len=7744)
             checkpoint took 0-00:00:32
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 7.0004: train_loss/word=5.152378 (steps=2016, words/sec=1469.40, time=0-00:10:19)
[switchout.en-my] Epoch 7.0765: train_loss/word=4.696512 (steps=2036, words/sec=10322.10, time=0-00:10:20)
[switchout.en-my] Epoch 7.1513: train_loss/word=4.727471 (steps=2061, words/sec=9373.87, time=0-00:10:23)
[switchout.en-my] Epoch 7.2256: train_loss/word=4.695670 (steps=2085, words/sec=9600.08, time=0-00:10:25)
[switchout.en-my] Epoch 7.3011: train_loss/word=4.728114 (steps=2106, words/sec=10748.08, time=0-00:10:26)
[switchout.en-my] Epoch 7.3764: train_loss/word=4.664113 (steps=2125, words/sec=12022.59, time=0-00:10:28)
[switchout.en-my] Epoch 7.4528: train_loss/word=4.668269 (steps=2147, words/sec=10979.74, time=0-00:10:30)
[switchout.en-my] Epoch 7.5296: train_loss/word=4.700451 (steps=2169, words/sec=10680.12, time=0-00:10:31)
[switchout.en-my] Epoch 7.6045: train_loss/word=4.674800 (steps=2192, words/sec=10169.12, time=0-00:10:33)
[switchout.en-my] Epoch 7.6801: train_loss/word=4.792773 (steps=2214, words/sec=9186.30, time=0-00:10:35)
[switchout.en-my] Epoch 7.7541: train_loss/word=4.774558 (steps=2237, words/sec=9779.55, time=0-00:10:37)
[switchout.en-my] Epoch 7.8288: train_loss/word=4.696695 (steps=2258, words/sec=10476.40, time=0-00:10:39)
[switchout.en-my] Epoch 7.9067: train_loss/word=4.776629 (steps=2279, words/sec=10896.70, time=0-00:10:41)
[switchout.en-my] Epoch 7.9803: train_loss/word=4.748352 (steps=2299, words/sec=11202.09, time=0-00:10:42)
[switchout.en-my] Epoch 8.0000: train_loss/word=4.770230 (steps=2304, words/sec=11484.70, time=0-00:10:42)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 8.0000 dev BLEU4: 0.10192249940623452, 0.395823/0.162162/0.063333/0.026546 (BP = 1.000000, ratio=1.02, hyp_len=7900, ref_len=7744) (time=0-00:11:14)
[switchout.en-my]              dev auxiliary GLEU: 0.156550
[switchout.en-my]              dev auxiliary Loss: 4.861 (ref_len=7744)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 8.0042: train_loss/word=4.465875 (steps=2305, words/sec=13921.55, time=0-00:11:23)
[switchout.en-my] Epoch 8.0789: train_loss/word=4.497093 (steps=2327, words/sec=9860.21, time=0-00:11:25)
[switchout.en-my] Epoch 8.1541: train_loss/word=4.505645 (steps=2349, words/sec=10224.56, time=0-00:11:27)
[switchout.en-my] Epoch 8.2307: train_loss/word=4.498507 (steps=2370, words/sec=11523.61, time=0-00:11:28)
[switchout.en-my] Epoch 8.3043: train_loss/word=4.541856 (steps=2392, words/sec=10565.10, time=0-00:11:30)
[switchout.en-my] Epoch 8.3797: train_loss/word=4.621101 (steps=2417, words/sec=8948.40, time=0-00:11:33)
[switchout.en-my] Epoch 8.4549: train_loss/word=4.602690 (steps=2438, words/sec=11004.54, time=0-00:11:34)
[switchout.en-my] Epoch 8.5312: train_loss/word=4.559091 (steps=2459, words/sec=11231.53, time=0-00:11:36)
[switchout.en-my] Epoch 8.6054: train_loss/word=4.556694 (steps=2481, words/sec=9832.24, time=0-00:11:38)
[switchout.en-my] Epoch 8.6797: train_loss/word=4.631004 (steps=2504, words/sec=9435.80, time=0-00:11:40)
[switchout.en-my] Epoch 8.7551: train_loss/word=4.567896 (steps=2527, words/sec=10290.80, time=0-00:11:42)
[switchout.en-my] Epoch 8.8297: train_loss/word=4.535808 (steps=2548, words/sec=9350.21, time=0-00:11:44)
[switchout.en-my] Epoch 8.9035: train_loss/word=4.646318 (steps=2566, words/sec=10039.30, time=0-00:11:45)
[switchout.en-my] Epoch 8.9780: train_loss/word=4.562201 (steps=2585, words/sec=11080.20, time=0-00:11:46)
[switchout.en-my] Epoch 9.0000: train_loss/word=4.713431 (steps=2592, words/sec=9114.94, time=0-00:11:47)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 9.0000 dev BLEU4: 0.11023970609093395, 0.408179/0.169780/0.068678/0.031305 (BP = 0.997802, ratio=1.00, hyp_len=7727, ref_len=7744) (time=0-00:12:20)
[switchout.en-my]              dev auxiliary GLEU: 0.161905
[switchout.en-my]              dev auxiliary Loss: 4.822 (ref_len=7744)
             checkpoint took 0-00:00:32
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 9.0024: train_loss/word=4.391270 (steps=2593, words/sec=8739.86, time=0-00:12:30)
[switchout.en-my] Epoch 9.0767: train_loss/word=4.368182 (steps=2613, words/sec=11139.44, time=0-00:12:31)
[switchout.en-my] Epoch 9.1529: train_loss/word=4.395972 (steps=2637, words/sec=8980.55, time=0-00:12:33)
[switchout.en-my] Epoch 9.2265: train_loss/word=4.447427 (steps=2656, words/sec=10158.24, time=0-00:12:35)
[switchout.en-my] Epoch 9.3024: train_loss/word=4.308621 (steps=2679, words/sec=9714.83, time=0-00:12:37)
[switchout.en-my] Epoch 9.3760: train_loss/word=4.420477 (steps=2702, words/sec=9280.73, time=0-00:12:39)
[switchout.en-my] Epoch 9.4499: train_loss/word=4.319258 (steps=2723, words/sec=10187.05, time=0-00:12:41)
[switchout.en-my] Epoch 9.5264: train_loss/word=4.430128 (steps=2746, words/sec=10398.09, time=0-00:12:43)
[switchout.en-my] Epoch 9.6017: train_loss/word=4.517244 (steps=2765, words/sec=10285.29, time=0-00:12:44)
[switchout.en-my] Epoch 9.6766: train_loss/word=4.365933 (steps=2786, words/sec=10773.91, time=0-00:12:46)
[switchout.en-my] Epoch 9.7508: train_loss/word=4.485935 (steps=2808, words/sec=9723.43, time=0-00:12:48)
[switchout.en-my] Epoch 9.8251: train_loss/word=4.451509 (steps=2828, words/sec=11220.14, time=0-00:12:49)
[switchout.en-my] Epoch 9.9001: train_loss/word=4.489584 (steps=2849, words/sec=10186.46, time=0-00:12:51)
[switchout.en-my] Epoch 9.9745: train_loss/word=4.503153 (steps=2870, words/sec=10744.40, time=0-00:12:53)
[switchout.en-my] Epoch 10.0000: train_loss/word=4.454952 (steps=2880, words/sec=6019.83, time=0-00:12:54)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 10.0000 dev BLEU4: 0.11949076595398474, 0.423248/0.181729/0.078971/0.035290 (BP = 0.987526, ratio=0.99, hyp_len=7648, ref_len=7744) (time=0-00:13:25)
[switchout.en-my]              dev auxiliary GLEU: 0.169167
[switchout.en-my]              dev auxiliary Loss: 4.768 (ref_len=7744)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 10.0020: train_loss/word=4.382329 (steps=2881, words/sec=7647.96, time=0-00:13:35)
[switchout.en-my] Epoch 10.0778: train_loss/word=4.236202 (steps=2900, words/sec=11613.80, time=0-00:13:36)
[switchout.en-my] Epoch 10.1537: train_loss/word=4.192036 (steps=2922, words/sec=10499.67, time=0-00:13:38)
[switchout.en-my] Epoch 10.2296: train_loss/word=4.163970 (steps=2942, words/sec=11649.09, time=0-00:13:40)
[switchout.en-my] Epoch 10.3055: train_loss/word=4.193455 (steps=2964, words/sec=10768.03, time=0-00:13:41)
[switchout.en-my] Epoch 10.3807: train_loss/word=4.244906 (steps=2988, words/sec=9174.36, time=0-00:13:43)
[switchout.en-my] Epoch 10.4575: train_loss/word=4.264775 (steps=3012, words/sec=8743.00, time=0-00:13:46)
[switchout.en-my] Epoch 10.5322: train_loss/word=4.324776 (steps=3033, words/sec=11198.28, time=0-00:13:47)
[switchout.en-my] Epoch 10.6068: train_loss/word=4.329542 (steps=3056, words/sec=9295.62, time=0-00:13:49)
[switchout.en-my] Epoch 10.6818: train_loss/word=4.289787 (steps=3078, words/sec=10084.73, time=0-00:13:51)
[switchout.en-my] Epoch 10.7557: train_loss/word=4.382642 (steps=3099, words/sec=8617.07, time=0-00:13:53)
[switchout.en-my] Epoch 10.8304: train_loss/word=4.364098 (steps=3118, words/sec=11029.85, time=0-00:13:55)
[switchout.en-my] Epoch 10.9055: train_loss/word=4.326004 (steps=3142, words/sec=9889.65, time=0-00:13:57)
[switchout.en-my] Epoch 10.9791: train_loss/word=4.287561 (steps=3162, words/sec=11249.09, time=0-00:13:58)
[switchout.en-my] Epoch 11.0000: train_loss/word=4.263645 (steps=3169, words/sec=7309.85, time=0-00:13:59)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 11.0000 dev BLEU4: 0.11938318537082238, 0.434662/0.187632/0.077413/0.034726 (BP = 0.981099, ratio=0.98, hyp_len=7599, ref_len=7744) (time=0-00:14:29)
[switchout.en-my]              dev auxiliary GLEU: 0.173079
[switchout.en-my]              dev auxiliary Loss: 4.744 (ref_len=7744)
             checkpoint took 0-00:00:30
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 11.0021: train_loss/word=3.815920 (steps=3170, words/sec=4927.97, time=0-00:14:32)
[switchout.en-my] Epoch 11.0775: train_loss/word=4.130092 (steps=3189, words/sec=12097.75, time=0-00:14:34)
[switchout.en-my] Epoch 11.1519: train_loss/word=4.064284 (steps=3213, words/sec=10253.52, time=0-00:14:36)
[switchout.en-my] Epoch 11.2287: train_loss/word=4.130590 (steps=3236, words/sec=9622.34, time=0-00:14:38)
[switchout.en-my] Epoch 11.3053: train_loss/word=4.172516 (steps=3256, words/sec=11033.90, time=0-00:14:39)
[switchout.en-my] Epoch 11.3790: train_loss/word=4.223263 (steps=3276, words/sec=10715.17, time=0-00:14:41)
[switchout.en-my] Epoch 11.4603: train_loss/word=4.160185 (steps=3301, words/sec=9635.69, time=0-00:14:43)
[switchout.en-my] Epoch 11.5340: train_loss/word=4.177310 (steps=3322, words/sec=9717.21, time=0-00:14:45)
[switchout.en-my] Epoch 11.6124: train_loss/word=4.294764 (steps=3343, words/sec=10091.79, time=0-00:14:47)
[switchout.en-my] Epoch 11.6881: train_loss/word=4.120710 (steps=3367, words/sec=9729.76, time=0-00:14:49)
[switchout.en-my] Epoch 11.7677: train_loss/word=4.154037 (steps=3388, words/sec=11088.46, time=0-00:14:50)
[switchout.en-my] Epoch 11.8416: train_loss/word=4.158277 (steps=3408, words/sec=11005.82, time=0-00:14:52)
[switchout.en-my] Epoch 11.9199: train_loss/word=4.218624 (steps=3431, words/sec=9262.80, time=0-00:14:54)
[switchout.en-my] Epoch 11.9955: train_loss/word=4.151725 (steps=3455, words/sec=10224.99, time=0-00:14:56)
[switchout.en-my] Epoch 12.0000: train_loss/word=4.370084 (steps=3456, words/sec=11056.67, time=0-00:14:56)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 12.0000 dev BLEU4: 0.13049397485255798, 0.453689/0.204244/0.089764/0.041329 (BP = 0.958350, ratio=0.96, hyp_len=7428, ref_len=7744) (time=0-00:15:26)
[switchout.en-my]              dev auxiliary GLEU: 0.183692
[switchout.en-my]              dev auxiliary Loss: 4.714 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 12.0024: train_loss/word=3.816751 (steps=3457, words/sec=7504.23, time=0-00:15:36)
[switchout.en-my] Epoch 12.0782: train_loss/word=3.937602 (steps=3480, words/sec=10116.01, time=0-00:15:38)
[switchout.en-my] Epoch 12.1533: train_loss/word=4.029599 (steps=3505, words/sec=8670.21, time=0-00:15:40)
[switchout.en-my] Epoch 12.2284: train_loss/word=4.026449 (steps=3524, words/sec=11672.54, time=0-00:15:42)
[switchout.en-my] Epoch 12.3066: train_loss/word=4.144141 (steps=3547, words/sec=8807.20, time=0-00:15:44)
[switchout.en-my] Epoch 12.3832: train_loss/word=4.044709 (steps=3570, words/sec=9682.80, time=0-00:15:46)
[switchout.en-my] Epoch 12.4593: train_loss/word=4.069976 (steps=3591, words/sec=9599.57, time=0-00:15:47)
[switchout.en-my] Epoch 12.5335: train_loss/word=4.089151 (steps=3610, words/sec=10668.67, time=0-00:15:49)
[switchout.en-my] Epoch 12.6073: train_loss/word=4.009033 (steps=3634, words/sec=9442.06, time=0-00:15:51)
[switchout.en-my] Epoch 12.6831: train_loss/word=3.991932 (steps=3658, words/sec=10133.37, time=0-00:15:53)
[switchout.en-my] Epoch 12.7572: train_loss/word=4.075236 (steps=3680, words/sec=10429.08, time=0-00:15:55)
[switchout.en-my] Epoch 12.8320: train_loss/word=4.022799 (steps=3701, words/sec=10873.66, time=0-00:15:57)
[switchout.en-my] Epoch 12.9119: train_loss/word=4.147108 (steps=3723, words/sec=8833.33, time=0-00:15:59)
[switchout.en-my] Epoch 12.9856: train_loss/word=4.078264 (steps=3742, words/sec=11767.51, time=0-00:16:00)
[switchout.en-my] Epoch 13.0000: train_loss/word=4.269014 (steps=3745, words/sec=14545.16, time=0-00:16:00)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 13.0000 dev BLEU4: 0.12864969327292133, 0.451504/0.200347/0.087451/0.041399 (BP = 0.956331, ratio=0.96, hyp_len=7413, ref_len=7744) (time=0-00:16:31)
[switchout.en-my]              dev auxiliary GLEU: 0.183183
[switchout.en-my]              dev auxiliary Loss: 4.695 (ref_len=7744)
             checkpoint took 0-00:00:30
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 13.0030: train_loss/word=4.073249 (steps=3746, words/sec=10187.00, time=0-00:16:34)
[switchout.en-my] Epoch 13.0814: train_loss/word=3.882440 (steps=3768, words/sec=9821.73, time=0-00:16:36)
[switchout.en-my] Epoch 13.1555: train_loss/word=4.004488 (steps=3790, words/sec=8055.79, time=0-00:16:38)
[switchout.en-my] Epoch 13.2295: train_loss/word=3.882409 (steps=3812, words/sec=10734.92, time=0-00:16:40)
[switchout.en-my] Epoch 13.3064: train_loss/word=3.922308 (steps=3834, words/sec=9677.81, time=0-00:16:42)
[switchout.en-my] Epoch 13.3846: train_loss/word=3.936277 (steps=3858, words/sec=9684.34, time=0-00:16:44)
[switchout.en-my] Epoch 13.4598: train_loss/word=3.943840 (steps=3879, words/sec=10136.61, time=0-00:16:46)
[switchout.en-my] Epoch 13.5345: train_loss/word=3.969772 (steps=3900, words/sec=10209.34, time=0-00:16:47)
[switchout.en-my] Epoch 13.6090: train_loss/word=3.931135 (steps=3922, words/sec=9451.21, time=0-00:16:49)
[switchout.en-my] Epoch 13.6863: train_loss/word=3.995887 (steps=3941, words/sec=10878.98, time=0-00:16:51)
[switchout.en-my] Epoch 13.7610: train_loss/word=3.914497 (steps=3962, words/sec=10612.74, time=0-00:16:53)
[switchout.en-my] Epoch 13.8358: train_loss/word=3.922197 (steps=3985, words/sec=9576.17, time=0-00:16:55)
[switchout.en-my] Epoch 13.9113: train_loss/word=3.933303 (steps=4007, words/sec=10817.91, time=0-00:16:56)
[switchout.en-my] Epoch 13.9854: train_loss/word=3.924254 (steps=4028, words/sec=10320.86, time=0-00:16:58)
[switchout.en-my] Epoch 14.0000: train_loss/word=3.873443 (steps=4033, words/sec=9812.80, time=0-00:16:58)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 14.0000 dev BLEU4: 0.14107144988712927, 0.455377/0.210122/0.094394/0.045986 (BP = 0.988180, ratio=0.99, hyp_len=7653, ref_len=7744) (time=0-00:17:29)
[switchout.en-my]              dev auxiliary GLEU: 0.190758
[switchout.en-my]              dev auxiliary Loss: 4.700 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 14.0026: train_loss/word=3.567610 (steps=4034, words/sec=8518.26, time=0-00:17:38)
[switchout.en-my] Epoch 14.0804: train_loss/word=3.708180 (steps=4059, words/sec=9717.19, time=0-00:17:41)
[switchout.en-my] Epoch 14.1552: train_loss/word=3.819925 (steps=4082, words/sec=9132.36, time=0-00:17:43)
[switchout.en-my] Epoch 14.2318: train_loss/word=3.854884 (steps=4103, words/sec=10538.96, time=0-00:17:44)
[switchout.en-my] Epoch 14.3064: train_loss/word=3.843349 (steps=4124, words/sec=10914.35, time=0-00:17:46)
[switchout.en-my] Epoch 14.3832: train_loss/word=3.920217 (steps=4144, words/sec=11476.26, time=0-00:17:48)
[switchout.en-my] Epoch 14.4597: train_loss/word=3.905197 (steps=4164, words/sec=10998.21, time=0-00:17:49)
[switchout.en-my] Epoch 14.5351: train_loss/word=3.745763 (steps=4187, words/sec=10541.65, time=0-00:17:51)
[switchout.en-my] Epoch 14.6123: train_loss/word=3.847813 (steps=4211, words/sec=9822.72, time=0-00:17:53)
[switchout.en-my] Epoch 14.6887: train_loss/word=3.905219 (steps=4231, words/sec=11815.37, time=0-00:17:55)
[switchout.en-my] Epoch 14.7651: train_loss/word=3.911287 (steps=4251, words/sec=10887.10, time=0-00:17:56)
[switchout.en-my] Epoch 14.8401: train_loss/word=3.843314 (steps=4276, words/sec=9297.03, time=0-00:17:58)
[switchout.en-my] Epoch 14.9172: train_loss/word=3.863339 (steps=4295, words/sec=11873.02, time=0-00:18:00)
[switchout.en-my] Epoch 14.9947: train_loss/word=3.910983 (steps=4319, words/sec=8551.96, time=0-00:18:02)
[switchout.en-my] Epoch 15.0000: train_loss/word=3.804570 (steps=4321, words/sec=9775.31, time=0-00:18:02)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 15.0000 dev BLEU4: 0.14261434941782153, 0.466649/0.215695/0.097752/0.047992 (BP = 0.967457, ratio=0.97, hyp_len=7496, ref_len=7744) (time=0-00:18:33)
[switchout.en-my]              dev auxiliary GLEU: 0.194675
[switchout.en-my]              dev auxiliary Loss: 4.659 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 15.0026: train_loss/word=3.370950 (steps=4322, words/sec=8957.77, time=0-00:18:42)
[switchout.en-my] Epoch 15.0778: train_loss/word=3.731929 (steps=4341, words/sec=12107.33, time=0-00:18:44)
[switchout.en-my] Epoch 15.1541: train_loss/word=3.774535 (steps=4359, words/sec=12043.68, time=0-00:18:45)
[switchout.en-my] Epoch 15.2281: train_loss/word=3.634742 (steps=4381, words/sec=10636.23, time=0-00:18:47)
[switchout.en-my] Epoch 15.3033: train_loss/word=3.753076 (steps=4403, words/sec=9845.98, time=0-00:18:49)
[switchout.en-my] Epoch 15.3776: train_loss/word=3.758496 (steps=4423, words/sec=10366.19, time=0-00:18:50)
[switchout.en-my] Epoch 15.4531: train_loss/word=3.640586 (steps=4445, words/sec=10368.31, time=0-00:18:52)
[switchout.en-my] Epoch 15.5292: train_loss/word=3.715120 (steps=4466, words/sec=11369.03, time=0-00:18:54)
[switchout.en-my] Epoch 15.6054: train_loss/word=3.781652 (steps=4489, words/sec=10088.51, time=0-00:18:55)
[switchout.en-my] Epoch 15.6806: train_loss/word=3.725854 (steps=4511, words/sec=10699.15, time=0-00:18:57)
[switchout.en-my] Epoch 15.7576: train_loss/word=3.803048 (steps=4534, words/sec=8339.77, time=0-00:19:00)
[switchout.en-my] Epoch 15.8333: train_loss/word=3.679063 (steps=4559, words/sec=8716.80, time=0-00:19:02)
[switchout.en-my] Epoch 15.9085: train_loss/word=3.801664 (steps=4582, words/sec=9761.83, time=0-00:19:04)
[switchout.en-my] Epoch 15.9836: train_loss/word=3.772482 (steps=4602, words/sec=10725.60, time=0-00:19:06)
[switchout.en-my] Epoch 16.0000: train_loss/word=3.852766 (steps=4608, words/sec=9404.03, time=0-00:19:06)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 16.0000 dev BLEU4: 0.14998532808687806, 0.467783/0.219155/0.104336/0.053094 (BP = 0.971582, ratio=0.97, hyp_len=7527, ref_len=7744) (time=0-00:19:37)
[switchout.en-my]              dev auxiliary GLEU: 0.198572
[switchout.en-my]              dev auxiliary Loss: 4.665 (ref_len=7744)
             checkpoint took 0-00:00:31
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 16.0036: train_loss/word=3.540973 (steps=4609, words/sec=11555.75, time=0-00:19:47)
[switchout.en-my] Epoch 16.0775: train_loss/word=3.532564 (steps=4632, words/sec=9838.92, time=0-00:19:49)
[switchout.en-my] Epoch 16.1521: train_loss/word=3.616771 (steps=4652, words/sec=11555.76, time=0-00:19:50)
[switchout.en-my] Epoch 16.2281: train_loss/word=3.632885 (steps=4675, words/sec=9775.86, time=0-00:19:52)
[switchout.en-my] Epoch 16.3026: train_loss/word=3.714642 (steps=4697, words/sec=9284.59, time=0-00:19:54)
[switchout.en-my] Epoch 16.3771: train_loss/word=3.562027 (steps=4722, words/sec=9540.61, time=0-00:19:56)
[switchout.en-my] Epoch 16.4510: train_loss/word=3.765015 (steps=4742, words/sec=9084.73, time=0-00:19:58)
[switchout.en-my] Epoch 16.5261: train_loss/word=3.713307 (steps=4764, words/sec=9838.58, time=0-00:20:00)
[switchout.en-my] Epoch 16.6023: train_loss/word=3.766737 (steps=4784, words/sec=10535.80, time=0-00:20:02)
[switchout.en-my] Epoch 16.6788: train_loss/word=3.754105 (steps=4804, words/sec=9934.59, time=0-00:20:03)
[switchout.en-my] Epoch 16.7535: train_loss/word=3.688935 (steps=4825, words/sec=10629.60, time=0-00:20:05)
[switchout.en-my] Epoch 16.8275: train_loss/word=3.777019 (steps=4844, words/sec=11760.81, time=0-00:20:06)
[switchout.en-my] Epoch 16.9044: train_loss/word=3.696245 (steps=4867, words/sec=9782.15, time=0-00:20:08)
[switchout.en-my] Epoch 16.9803: train_loss/word=3.658188 (steps=4889, words/sec=9512.46, time=0-00:20:10)
[switchout.en-my] Epoch 17.0000: train_loss/word=3.730179 (steps=4896, words/sec=9379.45, time=0-00:20:11)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 17.0000 dev BLEU4: 0.1573533240683473, 0.484763/0.228954/0.110801/0.058409 (BP = 0.961171, ratio=0.96, hyp_len=7449, ref_len=7744) (time=0-00:20:42)
[switchout.en-my]              dev auxiliary GLEU: 0.206827
[switchout.en-my]              dev auxiliary Loss: 4.640 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 17.0040: train_loss/word=3.036984 (steps=4897, words/sec=13001.39, time=0-00:20:51)
[switchout.en-my] Epoch 17.0796: train_loss/word=3.439942 (steps=4919, words/sec=10619.78, time=0-00:20:53)
[switchout.en-my] Epoch 17.1556: train_loss/word=3.470851 (steps=4943, words/sec=9660.37, time=0-00:20:55)
[switchout.en-my] Epoch 17.2343: train_loss/word=3.610843 (steps=4964, words/sec=10646.50, time=0-00:20:57)
[switchout.en-my] Epoch 17.3082: train_loss/word=3.574363 (steps=4987, words/sec=9171.76, time=0-00:20:59)
[switchout.en-my] Epoch 17.3827: train_loss/word=3.540632 (steps=5009, words/sec=9971.55, time=0-00:21:01)
[switchout.en-my] Epoch 17.4564: train_loss/word=3.639619 (steps=5030, words/sec=9591.33, time=0-00:21:03)
[switchout.en-my] Epoch 17.5314: train_loss/word=3.570467 (steps=5054, words/sec=9671.05, time=0-00:21:05)
[switchout.en-my] Epoch 17.6071: train_loss/word=3.534456 (steps=5079, words/sec=10015.27, time=0-00:21:07)
[switchout.en-my] Epoch 17.6808: train_loss/word=3.620846 (steps=5100, words/sec=10173.06, time=0-00:21:09)
[switchout.en-my] Epoch 17.7548: train_loss/word=3.661767 (steps=5120, words/sec=10064.06, time=0-00:21:10)
[switchout.en-my] Epoch 17.8301: train_loss/word=3.651583 (steps=5139, words/sec=10908.41, time=0-00:21:12)
[switchout.en-my] Epoch 17.9108: train_loss/word=3.669237 (steps=5160, words/sec=11638.32, time=0-00:21:13)
[switchout.en-my] Epoch 17.9871: train_loss/word=3.672612 (steps=5178, words/sec=12498.58, time=0-00:21:15)
[switchout.en-my] Epoch 18.0000: train_loss/word=3.727277 (steps=5182, words/sec=8568.67, time=0-00:21:15)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 18.0000 dev BLEU4: 0.15327430226345928, 0.480600/0.224694/0.104347/0.052752 (BP = 0.981626, ratio=0.98, hyp_len=7603, ref_len=7744) (time=0-00:21:46)
[switchout.en-my]              dev auxiliary GLEU: 0.205359
[switchout.en-my]              dev auxiliary Loss: 4.644 (ref_len=7744)
             checkpoint took 0-00:00:30
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 18.0020: train_loss/word=3.516460 (steps=5183, words/sec=7394.67, time=0-00:21:49)
[switchout.en-my] Epoch 18.0765: train_loss/word=3.510207 (steps=5202, words/sec=11808.45, time=0-00:21:50)
[switchout.en-my] Epoch 18.1528: train_loss/word=3.385494 (steps=5227, words/sec=9279.53, time=0-00:21:52)
[switchout.en-my] Epoch 18.2298: train_loss/word=3.506224 (steps=5250, words/sec=10077.83, time=0-00:21:54)
[switchout.en-my] Epoch 18.3042: train_loss/word=3.453983 (steps=5273, words/sec=9145.24, time=0-00:21:56)
[switchout.en-my] Epoch 18.3805: train_loss/word=3.484658 (steps=5294, words/sec=11068.15, time=0-00:21:58)
[switchout.en-my] Epoch 18.4555: train_loss/word=3.513768 (steps=5317, words/sec=10202.75, time=0-00:22:00)
[switchout.en-my] Epoch 18.5293: train_loss/word=3.493069 (steps=5340, words/sec=8907.82, time=0-00:22:02)
[switchout.en-my] Epoch 18.6037: train_loss/word=3.599472 (steps=5361, words/sec=9731.11, time=0-00:22:04)
[switchout.en-my] Epoch 18.6820: train_loss/word=3.644027 (steps=5382, words/sec=10152.21, time=0-00:22:05)
[switchout.en-my] Epoch 18.7593: train_loss/word=3.573293 (steps=5403, words/sec=10804.95, time=0-00:22:07)
[switchout.en-my] Epoch 18.8342: train_loss/word=3.647625 (steps=5423, words/sec=11820.10, time=0-00:22:09)
[switchout.en-my] Epoch 18.9101: train_loss/word=3.547931 (steps=5446, words/sec=10148.71, time=0-00:22:11)
[switchout.en-my] Epoch 18.9865: train_loss/word=3.695134 (steps=5467, words/sec=10038.10, time=0-00:22:12)
[switchout.en-my] Epoch 19.0000: train_loss/word=3.755264 (steps=5470, words/sec=9570.12, time=0-00:22:13)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 19.0000 dev BLEU4: 0.16008021496414626, 0.486422/0.228180/0.111486/0.060047 (BP = 0.969588, ratio=0.97, hyp_len=7512, ref_len=7744) (time=0-00:22:43)
[switchout.en-my]              dev auxiliary GLEU: 0.209883
[switchout.en-my]              dev auxiliary Loss: 4.633 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 19.0074: train_loss/word=3.903908 (steps=5471, words/sec=20187.74, time=0-00:22:53)
[switchout.en-my] Epoch 19.0816: train_loss/word=3.484886 (steps=5490, words/sec=10543.35, time=0-00:22:54)
[switchout.en-my] Epoch 19.1562: train_loss/word=3.339288 (steps=5512, words/sec=11276.27, time=0-00:22:56)
[switchout.en-my] Epoch 19.2328: train_loss/word=3.459531 (steps=5533, words/sec=10697.15, time=0-00:22:57)
[switchout.en-my] Epoch 19.3069: train_loss/word=3.465413 (steps=5554, words/sec=9985.55, time=0-00:22:59)
[switchout.en-my] Epoch 19.3817: train_loss/word=3.402857 (steps=5578, words/sec=8703.10, time=0-00:23:01)
[switchout.en-my] Epoch 19.4567: train_loss/word=3.412644 (steps=5602, words/sec=9477.95, time=0-00:23:04)
[switchout.en-my] Epoch 19.5346: train_loss/word=3.443381 (steps=5623, words/sec=10682.92, time=0-00:23:05)
[switchout.en-my] Epoch 19.6099: train_loss/word=3.466453 (steps=5643, words/sec=10819.83, time=0-00:23:07)
[switchout.en-my] Epoch 19.6844: train_loss/word=3.504651 (steps=5665, words/sec=9822.88, time=0-00:23:09)
[switchout.en-my] Epoch 19.7598: train_loss/word=3.520607 (steps=5687, words/sec=10193.58, time=0-00:23:10)
[switchout.en-my] Epoch 19.8348: train_loss/word=3.458331 (steps=5709, words/sec=10267.01, time=0-00:23:12)
[switchout.en-my] Epoch 19.9084: train_loss/word=3.483084 (steps=5734, words/sec=8787.07, time=0-00:23:15)
[switchout.en-my] Epoch 19.9836: train_loss/word=3.537320 (steps=5755, words/sec=10100.89, time=0-00:23:17)
[switchout.en-my] Epoch 20.0000: train_loss/word=3.854678 (steps=5758, words/sec=14022.35, time=0-00:23:17)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 20.0000 dev BLEU4: 0.16397001359445085, 0.491921/0.239662/0.115699/0.060727 (BP = 0.966523, ratio=0.97, hyp_len=7489, ref_len=7744) (time=0-00:23:47)
[switchout.en-my]              dev auxiliary GLEU: 0.214655
[switchout.en-my]              dev auxiliary Loss: 4.624 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 20.0029: train_loss/word=3.039767 (steps=5759, words/sec=6858.85, time=0-00:23:57)
[switchout.en-my] Epoch 20.0778: train_loss/word=3.240548 (steps=5782, words/sec=10414.41, time=0-00:23:59)
[switchout.en-my] Epoch 20.1528: train_loss/word=3.391403 (steps=5803, words/sec=10333.03, time=0-00:24:01)
[switchout.en-my] Epoch 20.2269: train_loss/word=3.337775 (steps=5824, words/sec=11174.39, time=0-00:24:02)
[switchout.en-my] Epoch 20.3005: train_loss/word=3.345031 (steps=5846, words/sec=10182.71, time=0-00:24:04)
[switchout.en-my] Epoch 20.3802: train_loss/word=3.404630 (steps=5868, words/sec=9267.68, time=0-00:24:06)
[switchout.en-my] Epoch 20.4551: train_loss/word=3.398341 (steps=5892, words/sec=9165.14, time=0-00:24:08)
[switchout.en-my] Epoch 20.5294: train_loss/word=3.472333 (steps=5912, words/sec=11421.99, time=0-00:24:10)
[switchout.en-my] Epoch 20.6043: train_loss/word=3.398115 (steps=5933, words/sec=10647.28, time=0-00:24:11)
[switchout.en-my] Epoch 20.6789: train_loss/word=3.390718 (steps=5955, words/sec=10538.35, time=0-00:24:13)
[switchout.en-my] Epoch 20.7550: train_loss/word=3.380072 (steps=5977, words/sec=11193.98, time=0-00:24:15)
[switchout.en-my] Epoch 20.8308: train_loss/word=3.417681 (steps=5998, words/sec=11267.46, time=0-00:24:17)
[switchout.en-my] Epoch 20.9059: train_loss/word=3.481989 (steps=6020, words/sec=9168.11, time=0-00:24:19)
[switchout.en-my] Epoch 20.9810: train_loss/word=3.487898 (steps=6041, words/sec=9889.73, time=0-00:24:20)
[switchout.en-my] Epoch 21.0000: train_loss/word=3.343139 (steps=6046, words/sec=11640.21, time=0-00:24:21)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 21.0000 dev BLEU4: 0.16432812546713377, 0.490464/0.237589/0.114656/0.060486 (BP = 0.974632, ratio=0.97, hyp_len=7550, ref_len=7744) (time=0-00:24:51)
[switchout.en-my]              dev auxiliary GLEU: 0.214300
[switchout.en-my]              dev auxiliary Loss: 4.624 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 21.0028: train_loss/word=2.960055 (steps=6047, words/sec=9397.14, time=0-00:25:01)
[switchout.en-my] Epoch 21.0834: train_loss/word=3.222053 (steps=6070, words/sec=9466.16, time=0-00:25:03)
[switchout.en-my] Epoch 21.1588: train_loss/word=3.246716 (steps=6093, words/sec=9639.50, time=0-00:25:05)
[switchout.en-my] Epoch 21.2335: train_loss/word=3.422874 (steps=6114, words/sec=10603.98, time=0-00:25:07)
[switchout.en-my] Epoch 21.3098: train_loss/word=3.318850 (steps=6135, words/sec=10371.34, time=0-00:25:08)
[switchout.en-my] Epoch 21.3865: train_loss/word=3.368418 (steps=6158, words/sec=9581.87, time=0-00:25:10)
[switchout.en-my] Epoch 21.4603: train_loss/word=3.371118 (steps=6180, words/sec=9635.01, time=0-00:25:12)
[switchout.en-my] Epoch 21.5344: train_loss/word=3.322761 (steps=6202, words/sec=10113.61, time=0-00:25:14)
[switchout.en-my] Epoch 21.6099: train_loss/word=3.343046 (steps=6224, words/sec=8971.93, time=0-00:25:16)
[switchout.en-my] Epoch 21.6906: train_loss/word=3.433726 (steps=6247, words/sec=10649.50, time=0-00:25:18)
[switchout.en-my] Epoch 21.7671: train_loss/word=3.302000 (steps=6269, words/sec=10573.77, time=0-00:25:20)
[switchout.en-my] Epoch 21.8417: train_loss/word=3.360155 (steps=6290, words/sec=10948.69, time=0-00:25:21)
[switchout.en-my] Epoch 21.9197: train_loss/word=3.436183 (steps=6312, words/sec=10321.89, time=0-00:25:23)
[switchout.en-my] Epoch 21.9954: train_loss/word=3.398992 (steps=6334, words/sec=10107.31, time=0-00:25:25)
[switchout.en-my] Epoch 22.0000: train_loss/word=3.349503 (steps=6335, words/sec=16839.25, time=0-00:25:25)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 22.0000 dev BLEU4: 0.17072102128526617, 0.490284/0.243395/0.120731/0.063062 (BP = 0.983334, ratio=0.98, hyp_len=7616, ref_len=7744) (time=0-00:25:55)
[switchout.en-my]              dev auxiliary GLEU: 0.219476
[switchout.en-my]              dev auxiliary Loss: 4.610 (ref_len=7744)
             checkpoint took 0-00:00:29
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 22.0026: train_loss/word=2.937181 (steps=6336, words/sec=8726.88, time=0-00:26:04)
[switchout.en-my] Epoch 22.0778: train_loss/word=3.330393 (steps=6357, words/sec=9188.22, time=0-00:26:06)
[switchout.en-my] Epoch 22.1526: train_loss/word=3.251108 (steps=6377, words/sec=11554.99, time=0-00:26:08)
[switchout.en-my] Epoch 22.2315: train_loss/word=3.279556 (steps=6399, words/sec=10610.03, time=0-00:26:10)
[switchout.en-my] Epoch 22.3070: train_loss/word=3.227939 (steps=6423, words/sec=10442.97, time=0-00:26:12)
[switchout.en-my] Epoch 22.3818: train_loss/word=3.389420 (steps=6441, words/sec=11389.20, time=0-00:26:13)
[switchout.en-my] Epoch 22.4555: train_loss/word=3.358982 (steps=6462, words/sec=9507.55, time=0-00:26:15)
[switchout.en-my] Epoch 22.5321: train_loss/word=3.219060 (steps=6486, words/sec=9898.45, time=0-00:26:17)
[switchout.en-my] Epoch 22.6090: train_loss/word=3.203045 (steps=6509, words/sec=11250.50, time=0-00:26:19)
[switchout.en-my] Epoch 22.6840: train_loss/word=3.380140 (steps=6532, words/sec=10049.45, time=0-00:26:21)
[switchout.en-my] Epoch 22.7603: train_loss/word=3.431927 (steps=6550, words/sec=12197.09, time=0-00:26:22)
[switchout.en-my] Epoch 22.8363: train_loss/word=3.294057 (steps=6573, words/sec=9822.29, time=0-00:26:24)
[switchout.en-my] Epoch 22.9106: train_loss/word=3.325391 (steps=6594, words/sec=10764.30, time=0-00:26:26)
[switchout.en-my] Epoch 22.9882: train_loss/word=3.335883 (steps=6617, words/sec=10388.23, time=0-00:26:27)
[switchout.en-my] Epoch 23.0000: train_loss/word=3.284319 (steps=6622, words/sec=8109.35, time=0-00:26:28)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 23.0000 dev BLEU4: 0.16992784367514555, 0.485804/0.236695/0.116202/0.064584 (BP = 0.991441, ratio=0.99, hyp_len=7678, ref_len=7744) (time=0-00:26:57)
[switchout.en-my]              dev auxiliary GLEU: 0.215704
[switchout.en-my]              dev auxiliary Loss: 4.629 (ref_len=7744)
             checkpoint took 0-00:00:29
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 23.0024: train_loss/word=2.875284 (steps=6623, words/sec=7717.88, time=0-00:27:00)
[switchout.en-my] Epoch 23.0782: train_loss/word=3.146151 (steps=6647, words/sec=9170.78, time=0-00:27:03)
[switchout.en-my] Epoch 23.1537: train_loss/word=3.229592 (steps=6668, words/sec=10176.41, time=0-00:27:04)
[switchout.en-my] Epoch 23.2281: train_loss/word=3.168921 (steps=6689, words/sec=10651.37, time=0-00:27:06)
[switchout.en-my] Epoch 23.3030: train_loss/word=3.273488 (steps=6711, words/sec=10169.48, time=0-00:27:08)
[switchout.en-my] Epoch 23.3786: train_loss/word=3.278738 (steps=6732, words/sec=10144.71, time=0-00:27:10)
[switchout.en-my] Epoch 23.4522: train_loss/word=3.315202 (steps=6750, words/sec=11641.49, time=0-00:27:11)
[switchout.en-my] Epoch 23.5289: train_loss/word=3.242898 (steps=6773, words/sec=9557.33, time=0-00:27:13)
[switchout.en-my] Epoch 23.6037: train_loss/word=3.193210 (steps=6795, words/sec=10216.31, time=0-00:27:15)
[switchout.en-my] Epoch 23.6787: train_loss/word=3.330138 (steps=6815, words/sec=10312.20, time=0-00:27:16)
[switchout.en-my] Epoch 23.7543: train_loss/word=3.332418 (steps=6836, words/sec=9943.54, time=0-00:27:18)
[switchout.en-my] Epoch 23.8282: train_loss/word=3.319152 (steps=6857, words/sec=10205.35, time=0-00:27:20)
[switchout.en-my] Epoch 23.9043: train_loss/word=3.216568 (steps=6882, words/sec=10438.29, time=0-00:27:22)
[switchout.en-my] Epoch 23.9804: train_loss/word=3.360289 (steps=6904, words/sec=10082.87, time=0-00:27:24)
[switchout.en-my] Epoch 24.0000: train_loss/word=3.282339 (steps=6910, words/sec=8749.15, time=0-00:27:24)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 24.0000 dev BLEU4: 0.16641619388075793, 0.478737/0.230441/0.113132/0.061453 (BP = 1.000000, ratio=1.00, hyp_len=7760, ref_len=7744) (time=0-00:27:55)
[switchout.en-my]              dev auxiliary GLEU: 0.212466
[switchout.en-my]              dev auxiliary Loss: 4.636 (ref_len=7744)
             checkpoint took 0-00:00:30
  new learning rate: 0.5
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 24.0026: train_loss/word=2.849275 (steps=6911, words/sec=9271.89, time=0-00:27:58)
[switchout.en-my] Epoch 24.0775: train_loss/word=3.204617 (steps=6930, words/sec=11419.21, time=0-00:27:59)
[switchout.en-my] Epoch 24.1524: train_loss/word=3.045089 (steps=6952, words/sec=9395.85, time=0-00:28:01)
[switchout.en-my] Epoch 24.2261: train_loss/word=3.323322 (steps=6970, words/sec=10782.93, time=0-00:28:03)
[switchout.en-my] Epoch 24.3018: train_loss/word=3.054576 (steps=6994, words/sec=10736.20, time=0-00:28:05)
[switchout.en-my] Epoch 24.3759: train_loss/word=3.038061 (steps=7018, words/sec=9827.04, time=0-00:28:07)
[switchout.en-my] Epoch 24.4509: train_loss/word=3.141195 (steps=7040, words/sec=9255.58, time=0-00:28:09)
[switchout.en-my] Epoch 24.5274: train_loss/word=3.263823 (steps=7060, words/sec=10780.47, time=0-00:28:10)
[switchout.en-my] Epoch 24.6035: train_loss/word=3.084906 (steps=7082, words/sec=10630.99, time=0-00:28:12)
[switchout.en-my] Epoch 24.6788: train_loss/word=3.043823 (steps=7106, words/sec=9671.51, time=0-00:28:14)
[switchout.en-my] Epoch 24.7575: train_loss/word=3.119861 (steps=7129, words/sec=9162.06, time=0-00:28:16)
[switchout.en-my] Epoch 24.8316: train_loss/word=3.146807 (steps=7151, words/sec=10180.14, time=0-00:28:18)
[switchout.en-my] Epoch 24.9052: train_loss/word=3.148676 (steps=7172, words/sec=9922.43, time=0-00:28:20)
[switchout.en-my] Epoch 24.9815: train_loss/word=3.187888 (steps=7193, words/sec=10032.68, time=0-00:28:22)
[switchout.en-my] Epoch 25.0000: train_loss/word=3.107126 (steps=7198, words/sec=11487.76, time=0-00:28:22)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 25.0000 dev BLEU4: 0.1720498841729279, 0.494854/0.241594/0.120401/0.066447 (BP = 0.978333, ratio=0.98, hyp_len=7578, ref_len=7744) (time=0-00:28:52)
[switchout.en-my]              dev auxiliary GLEU: 0.219757
[switchout.en-my]              dev auxiliary Loss: 4.597 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 25.0026: train_loss/word=2.928240 (steps=7199, words/sec=7498.41, time=0-00:29:01)
[switchout.en-my] Epoch 25.0771: train_loss/word=3.018447 (steps=7220, words/sec=10441.69, time=0-00:29:03)
[switchout.en-my] Epoch 25.1535: train_loss/word=3.135101 (steps=7240, words/sec=9964.47, time=0-00:29:05)
[switchout.en-my] Epoch 25.2272: train_loss/word=3.017401 (steps=7262, words/sec=10271.52, time=0-00:29:07)
[switchout.en-my] Epoch 25.3028: train_loss/word=3.014649 (steps=7287, words/sec=9743.72, time=0-00:29:09)
[switchout.en-my] Epoch 25.3766: train_loss/word=3.006907 (steps=7311, words/sec=9288.97, time=0-00:29:11)
[switchout.en-my] Epoch 25.4541: train_loss/word=3.046785 (steps=7332, words/sec=10393.84, time=0-00:29:13)
[switchout.en-my] Epoch 25.5291: train_loss/word=3.023226 (steps=7356, words/sec=9414.49, time=0-00:29:15)
[switchout.en-my] Epoch 25.6047: train_loss/word=3.158076 (steps=7378, words/sec=10162.82, time=0-00:29:17)
[switchout.en-my] Epoch 25.6791: train_loss/word=3.235102 (steps=7397, words/sec=11648.25, time=0-00:29:18)
[switchout.en-my] Epoch 25.7528: train_loss/word=3.165953 (steps=7416, words/sec=11799.90, time=0-00:29:20)
[switchout.en-my] Epoch 25.8288: train_loss/word=3.003315 (steps=7438, words/sec=10626.78, time=0-00:29:21)
[switchout.en-my] Epoch 25.9080: train_loss/word=3.202006 (steps=7457, words/sec=11684.75, time=0-00:29:23)
[switchout.en-my] Epoch 25.9856: train_loss/word=3.061179 (steps=7482, words/sec=8373.19, time=0-00:29:25)
[switchout.en-my] Epoch 26.0000: train_loss/word=3.121965 (steps=7486, words/sec=11113.22, time=0-00:29:25)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 26.0000 dev BLEU4: 0.17572891376540606, 0.493754/0.242120/0.122247/0.065252 (BP = 1.000000, ratio=1.00, hyp_len=7765, ref_len=7744) (time=0-00:29:56)
[switchout.en-my]              dev auxiliary GLEU: 0.222995
[switchout.en-my]              dev auxiliary Loss: 4.583 (ref_len=7744)
             checkpoint took 0-00:00:30
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 26.0036: train_loss/word=2.841434 (steps=7487, words/sec=12088.72, time=0-00:30:05)
[switchout.en-my] Epoch 26.0798: train_loss/word=3.030800 (steps=7509, words/sec=10715.61, time=0-00:30:07)
[switchout.en-my] Epoch 26.1583: train_loss/word=2.987661 (steps=7532, words/sec=10758.05, time=0-00:30:09)
[switchout.en-my] Epoch 26.2326: train_loss/word=3.029060 (steps=7554, words/sec=9450.35, time=0-00:30:11)
[switchout.en-my] Epoch 26.3078: train_loss/word=3.013530 (steps=7576, words/sec=10569.75, time=0-00:30:13)
[switchout.en-my] Epoch 26.3826: train_loss/word=3.189450 (steps=7597, words/sec=10031.98, time=0-00:30:14)
[switchout.en-my] Epoch 26.4563: train_loss/word=3.034268 (steps=7619, words/sec=9276.89, time=0-00:30:16)
[switchout.en-my] Epoch 26.5299: train_loss/word=2.992233 (steps=7640, words/sec=10467.60, time=0-00:30:18)
[switchout.en-my] Epoch 26.6045: train_loss/word=2.988595 (steps=7663, words/sec=10032.66, time=0-00:30:20)
[switchout.en-my] Epoch 26.6810: train_loss/word=3.106316 (steps=7685, words/sec=10685.57, time=0-00:30:22)
[switchout.en-my] Epoch 26.7559: train_loss/word=3.061474 (steps=7707, words/sec=9891.74, time=0-00:30:24)
[switchout.en-my] Epoch 26.8311: train_loss/word=3.090678 (steps=7728, words/sec=10542.38, time=0-00:30:25)
[switchout.en-my] Epoch 26.9074: train_loss/word=3.262252 (steps=7745, words/sec=11710.66, time=0-00:30:27)
[switchout.en-my] Epoch 26.9826: train_loss/word=2.992563 (steps=7769, words/sec=9758.92, time=0-00:30:29)
[switchout.en-my] Epoch 27.0000: train_loss/word=3.193270 (steps=7773, words/sec=13993.51, time=0-00:30:29)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 27.0000 dev BLEU4: 0.1765910715396283, 0.504297/0.246354/0.126276/0.068216 (BP = 0.976352, ratio=0.98, hyp_len=7563, ref_len=7744) (time=0-00:30:59)
[switchout.en-my]              dev auxiliary GLEU: 0.225126
[switchout.en-my]              dev auxiliary Loss: 4.590 (ref_len=7744)
             checkpoint took 0-00:00:29
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 27.0029: train_loss/word=2.775882 (steps=7774, words/sec=7624.20, time=0-00:31:08)
[switchout.en-my] Epoch 27.0803: train_loss/word=2.998033 (steps=7794, words/sec=11583.37, time=0-00:31:10)
[switchout.en-my] Epoch 27.1563: train_loss/word=2.977715 (steps=7814, words/sec=10660.71, time=0-00:31:11)
[switchout.en-my] Epoch 27.2341: train_loss/word=2.931384 (steps=7840, words/sec=9645.33, time=0-00:31:14)
[switchout.en-my] Epoch 27.3097: train_loss/word=2.988869 (steps=7863, words/sec=9714.90, time=0-00:31:16)
[switchout.en-my] Epoch 27.3838: train_loss/word=2.973855 (steps=7884, words/sec=10407.62, time=0-00:31:17)
[switchout.en-my] Epoch 27.4603: train_loss/word=2.974900 (steps=7906, words/sec=9932.27, time=0-00:31:19)
[switchout.en-my] Epoch 27.5349: train_loss/word=3.000790 (steps=7927, words/sec=10620.70, time=0-00:31:21)
[switchout.en-my] Epoch 27.6107: train_loss/word=2.960387 (steps=7950, words/sec=9748.32, time=0-00:31:23)
[switchout.en-my] Epoch 27.6848: train_loss/word=3.076382 (steps=7972, words/sec=9900.76, time=0-00:31:25)
[switchout.en-my] Epoch 27.7593: train_loss/word=2.956166 (steps=7996, words/sec=9203.12, time=0-00:31:27)
[switchout.en-my] Epoch 27.8356: train_loss/word=3.028405 (steps=8018, words/sec=10496.75, time=0-00:31:29)
[switchout.en-my] Epoch 27.9117: train_loss/word=3.051025 (steps=8039, words/sec=11498.69, time=0-00:31:30)
[switchout.en-my] Epoch 27.9862: train_loss/word=3.085826 (steps=8057, words/sec=11155.00, time=0-00:31:32)
[switchout.en-my] Epoch 28.0000: train_loss/word=3.229425 (steps=8061, words/sec=8699.62, time=0-00:31:32)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 28.0000 dev BLEU4: 0.17380462209212255, 0.494656/0.244004/0.122752/0.063947 (BP = 0.990659, ratio=0.99, hyp_len=7672, ref_len=7744) (time=0-00:32:02)
[switchout.en-my]              dev auxiliary GLEU: 0.220904
[switchout.en-my]              dev auxiliary Loss: 4.606 (ref_len=7744)
             checkpoint took 0-00:00:30
  new learning rate: 0.25
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 28.0026: train_loss/word=2.825023 (steps=8062, words/sec=7968.25, time=0-00:32:05)
[switchout.en-my] Epoch 28.0768: train_loss/word=3.006702 (steps=8082, words/sec=10849.02, time=0-00:32:07)
[switchout.en-my] Epoch 28.1543: train_loss/word=2.906401 (steps=8104, words/sec=11599.77, time=0-00:32:08)
[switchout.en-my] Epoch 28.2301: train_loss/word=3.061300 (steps=8124, words/sec=11178.58, time=0-00:32:10)
[switchout.en-my] Epoch 28.3067: train_loss/word=2.991438 (steps=8146, words/sec=9001.71, time=0-00:32:12)
[switchout.en-my] Epoch 28.3808: train_loss/word=2.985212 (steps=8165, words/sec=11124.89, time=0-00:32:13)
[switchout.en-my] Epoch 28.4572: train_loss/word=2.932787 (steps=8189, words/sec=9645.11, time=0-00:32:15)
[switchout.en-my] Epoch 28.5322: train_loss/word=2.920636 (steps=8212, words/sec=10090.99, time=0-00:32:17)
[switchout.en-my] Epoch 28.6107: train_loss/word=2.932378 (steps=8235, words/sec=10757.02, time=0-00:32:19)
[switchout.en-my] Epoch 28.6892: train_loss/word=2.963573 (steps=8258, words/sec=9965.94, time=0-00:32:21)
[switchout.en-my] Epoch 28.7651: train_loss/word=3.002701 (steps=8279, words/sec=10193.35, time=0-00:32:23)
[switchout.en-my] Epoch 28.8390: train_loss/word=2.949210 (steps=8301, words/sec=9368.00, time=0-00:32:25)
[switchout.en-my] Epoch 28.9144: train_loss/word=3.005114 (steps=8323, words/sec=10693.05, time=0-00:32:27)
[switchout.en-my] Epoch 28.9882: train_loss/word=2.956705 (steps=8346, words/sec=9004.82, time=0-00:32:29)
[switchout.en-my] Epoch 29.0000: train_loss/word=2.846880 (steps=8350, words/sec=10140.49, time=0-00:32:29)
> Checkpoint [switchout.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.en-my] Epoch 29.0000 dev BLEU4: 0.17538504470081667, 0.502360/0.245932/0.122661/0.066351 (BP = 0.984908, ratio=0.99, hyp_len=7628, ref_len=7744) (time=0-00:32:59)
[switchout.en-my]              dev auxiliary GLEU: 0.223430
[switchout.en-my]              dev auxiliary Loss: 4.569 (ref_len=7744)
             checkpoint took 0-00:00:29
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.en-my               | BLEU4: 0.1765910715396283, 0.504297/0.246354/0.126276/0.068216 (BP = 0.976352, ratio=0.98, hyp_len=7563, ref_len=7744)
                              | GLEU: 0.225126
                              | WER: 69.21% ( C/S/I/D: 3323/3301/939/1120; hyp_len=7563, ref_len=7744 )
                              | CER: 56.68% ( C/S/I/D: 19849/9880/3759/7411; hyp_len=33488, ref_len=37140 )
                              | BLEU4: 0.1815215905704093, 0.511365/0.256621/0.130396/0.071406 (BP = 0.970896, ratio=0.97, hyp_len=7787, ref_len=8017)
                              | GLEU: 0.229314
                              | WER: 67.94% ( C/S/I/D: 3471/3415/901/1131; hyp_len=7787, ref_len=8017 )
                              | CER: 56.27% ( C/S/I/D: 20483/10066/3743/7731; hyp_len=34292, ref_len=38280 )
```

အရင် run ခဲ့တဲ့ (no-data argumentation, word unit, en-my) ရလဒ်က အောက်ပါအတိုင်း...  

```
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.en-my                 | BLEU4: 0.1654160488338149, 0.484379/0.230994/0.113738/0.060763 (BP = 0.991962, ratio=0.99, hyp_len=7682, ref_len=7744)
                              | GLEU: 0.212490
                              | WER: 71.44% ( C/S/I/D: 3194/3506/982/1044; hyp_len=7682, ref_len=7744 )
                              | CER: 58.03% ( C/S/I/D: 19664/10508/4077/6968; hyp_len=34249, ref_len=37140 )
                              | BLEU4: 0.17699824231899827, 0.486881/0.240633/0.121469/0.068966 (BP = 1.000000, ratio=1.01, hyp_len=8080, ref_len=8017)
                              | GLEU: 0.220710
                              | WER: 71.00% ( C/S/I/D: 3394/3617/1069/1006; hyp_len=8080, ref_len=8017 )
                              | CER: 58.23% ( C/S/I/D: 20641/11172/4651/6467; hyp_len=36464, ref_len=38280 )
```

အထက်ပါ ရလဒ်နှစ်ခုကို နှိုင်းယှဉ်ကြည့်ရင် ...  

***switchout ရလဒ်က အကုန်သာတယ်***  

## Updating Config File for Word Unit (my-en)

```yaml
# standard settings
switchout.my-en: !Experiment
  exp_global: !ExpGlobal
    default_layer_dim: 512 # Hidden layer size 512 by default
    dropout: 0.3           # Dropout 0.3 by default
  preproc: !PreprocRunner
    overwrite: False       # Don't redo preprocessing if it's been done once before
    tasks:
    - !PreprocVocab        # Create vocabulary files from the training data
      in_files:
      - '{EXP_DIR}/data/train.my'
      - '{EXP_DIR}/data/train.en'
      out_files:
      - '{EXP_DIR}/vocab.my'
      - '{EXP_DIR}/vocab.en'
      specs:
      - filenum: all
        filters:
        - !VocabFiltererRank
          max_rank: 30000 # Limit the vocabulary size to the 40k most frequent words
  model: !DefaultTranslator
    src_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.my'}
      tau: 0.8      
    trg_reader: !RamlTextReader
      vocab: !Vocab {vocab_file: '{EXP_DIR}/vocab.en'}
      tau: 0.8      
    src_embedder: !SimpleWordEmbedder   # Embed source words as 256 dimensional vectors
      emb_dim: 512
    encoder: !ResidualSeqTransducer
      child: !BiLSTMSeqTransducer
        layers: 2
    attender: !MlpAttender {}
    decoder: !AutoRegressiveDecoder
      embedder: !DenseWordEmbedder      # Represent target words as a 40000x256 matrix
        emb_dim: 512
      bridge: !LinearBridge {}          # Initialize the first state of the decoder with an affine transform of the last state of the encoder
      rnn: !UniLSTMSeqTransducer        # Just your standard LSTM decoder
        layers: 2                       # With 2 layers
      transform: !AuxNonLinear
        output_dim: !Ref
          path: model.decoder.embedder.emb_dim
        activation: 'relu'
      scorer: !Softmax
        output_projector: !Ref
          path: model.decoder.embedder      # Tie the softmax output to the target word embeddings
        label_smoothing: 0.1              # Smooth the output labels with the uniform distribution
    inference: !AutoRegressiveInference
      search_strategy: !BeamSearch
        beam_size: 5
        len_norm: !PolynomialNormalization
          apply_during_search: true
          m: 0.8
  train: !SimpleTrainingRegimen
    run_for_epochs: 30  # Run for at most 20 epochs
    initial_patience: 2 # Run for at least 2 epochs without decreasing the learning rate
    patience: 1         # After there is no improvement for 1 epoch, decrease the learning rate
    lr_decay: 0.5       # Decay the learning rate by half whenever there is no improvement
    lr_decay_times: 2   # If there is still no improvement after decreasing the learning rate 2 times in a row, stop training
    trainer: !AdamTrainer
      alpha: 0.001
    batcher: !WordSrcBatcher
      avg_batch_size: 64
    src_file: '{EXP_DIR}/data/train.my'
    trg_file: '{EXP_DIR}/data/train.en'
    dev_tasks:
      - !AccuracyEvalTask
        eval_metrics: bleu,gleu
        src_file: &dev_src '{EXP_DIR}/data/dev.my'
        ref_file: &dev_trg '{EXP_DIR}/data/dev.en'
        hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.en'
      - !LossEvalTask
        src_file: *dev_src
        ref_file: *dev_trg
  evaluate:
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: *dev_src
      ref_file: *dev_trg
      hyp_file: '{EXP_DIR}/hyp/{EXP}.dev.en'
    - !AccuracyEvalTask
      eval_metrics: bleu,gleu,wer,cer
      src_file: &test_src '{EXP_DIR}/data/test.my'
      ref_file: &test_trg '{EXP_DIR}/data/test.en'
      hyp_file: '{EXP_DIR}/hyp/{EXP}.test.en'
```

## Training for Word-SwitchOut (my-en)

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/word_switchout$ time xnmt --backend torch --gpu ./config.switchout.my-en-word.yaml | tee switchout.my-en.log1
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 15:58:31
=> Running switchout.my-en
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 22449317
> Training
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 0.0753: train_loss/word=9.602448 (steps=23, words/sec=7231.28, time=0-00:00:08)
[switchout.my-en] Epoch 0.1492: train_loss/word=7.607947 (steps=43, words/sec=10180.92, time=0-00:00:09)
[switchout.my-en] Epoch 0.2246: train_loss/word=7.381298 (steps=64, words/sec=9879.40, time=0-00:00:11)
[switchout.my-en] Epoch 0.3019: train_loss/word=7.361799 (steps=84, words/sec=10399.07, time=0-00:00:12)
[switchout.my-en] Epoch 0.3756: train_loss/word=7.269590 (steps=105, words/sec=9520.01, time=0-00:00:14)
[switchout.my-en] Epoch 0.4546: train_loss/word=7.296032 (steps=125, words/sec=10804.59, time=0-00:00:15)
[switchout.my-en] Epoch 0.5300: train_loss/word=7.249267 (steps=148, words/sec=9426.46, time=0-00:00:17)
[switchout.my-en] Epoch 0.6036: train_loss/word=7.259353 (steps=166, words/sec=10564.47, time=0-00:00:19)
[switchout.my-en] Epoch 0.6819: train_loss/word=7.239325 (steps=187, words/sec=9387.06, time=0-00:00:20)
[switchout.my-en] Epoch 0.7592: train_loss/word=7.104398 (steps=210, words/sec=9716.62, time=0-00:00:22)
[switchout.my-en] Epoch 0.8334: train_loss/word=7.139365 (steps=227, words/sec=11245.34, time=0-00:00:23)
[switchout.my-en] Epoch 0.9098: train_loss/word=7.005535 (steps=247, words/sec=9408.61, time=0-00:00:25)
[switchout.my-en] Epoch 0.9847: train_loss/word=6.896281 (steps=266, words/sec=11248.93, time=0-00:00:26)
[switchout.my-en] Epoch 1.0000: train_loss/word=6.919019 (steps=271, words/sec=8573.58, time=0-00:00:26)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 1.0000 dev BLEU4: 0.0, 0.177482/0.003899/0.000000/0.000000 (BP = 0.739776, ratio=0.77, hyp_len=5116, ref_len=6658) (time=0-00:00:48)
[switchout.my-en]              dev auxiliary GLEU: 0.038458
[switchout.my-en]              dev auxiliary Loss: 6.598 (ref_len=6658)
             checkpoint took 0-00:00:21
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 1.0029: train_loss/word=6.860208 (steps=272, words/sec=8833.28, time=0-00:01:12)
[switchout.my-en] Epoch 1.0768: train_loss/word=6.793001 (steps=295, words/sec=8935.08, time=0-00:01:14)
[switchout.my-en] Epoch 1.1521: train_loss/word=6.744456 (steps=312, words/sec=11145.60, time=0-00:01:16)
[switchout.my-en] Epoch 1.2276: train_loss/word=6.688260 (steps=333, words/sec=10222.70, time=0-00:01:17)
[switchout.my-en] Epoch 1.3028: train_loss/word=6.625168 (steps=353, words/sec=10391.34, time=0-00:01:19)
[switchout.my-en] Epoch 1.3764: train_loss/word=6.595685 (steps=376, words/sec=8374.72, time=0-00:01:21)
[switchout.my-en] Epoch 1.4511: train_loss/word=6.535812 (steps=397, words/sec=9274.38, time=0-00:01:22)
[switchout.my-en] Epoch 1.5271: train_loss/word=6.492137 (steps=418, words/sec=8869.70, time=0-00:01:24)
[switchout.my-en] Epoch 1.6035: train_loss/word=6.418563 (steps=438, words/sec=10322.60, time=0-00:01:26)
[switchout.my-en] Epoch 1.6779: train_loss/word=6.370263 (steps=455, words/sec=12182.45, time=0-00:01:27)
[switchout.my-en] Epoch 1.7535: train_loss/word=6.386616 (steps=475, words/sec=10419.72, time=0-00:01:28)
[switchout.my-en] Epoch 1.8273: train_loss/word=6.340819 (steps=497, words/sec=8830.58, time=0-00:01:30)
[switchout.my-en] Epoch 1.9017: train_loss/word=6.327882 (steps=519, words/sec=9201.48, time=0-00:01:32)
[switchout.my-en] Epoch 1.9795: train_loss/word=6.283105 (steps=536, words/sec=11111.07, time=0-00:01:33)
[switchout.my-en] Epoch 2.0000: train_loss/word=6.262261 (steps=542, words/sec=10113.75, time=0-00:01:33)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 2.0000 dev BLEU4: 0.011777749262601427, 0.201453/0.018831/0.004457/0.001174 (BP = 0.992311, ratio=0.99, hyp_len=6607, ref_len=6658) (time=0-00:02:01)
[switchout.my-en]              dev auxiliary GLEU: 0.053760
[switchout.my-en]              dev auxiliary Loss: 5.878 (ref_len=6658)
             checkpoint took 0-00:00:28
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 2.0040: train_loss/word=6.142390 (steps=543, words/sec=12367.89, time=0-00:02:11)
[switchout.my-en] Epoch 2.0798: train_loss/word=6.142543 (steps=562, words/sec=11409.91, time=0-00:02:12)
[switchout.my-en] Epoch 2.1546: train_loss/word=6.108929 (steps=582, words/sec=9987.21, time=0-00:02:13)
[switchout.my-en] Epoch 2.2318: train_loss/word=6.085267 (steps=603, words/sec=10770.24, time=0-00:02:15)
[switchout.my-en] Epoch 2.3071: train_loss/word=6.070254 (steps=623, words/sec=10763.29, time=0-00:02:16)
[switchout.my-en] Epoch 2.3830: train_loss/word=6.075199 (steps=640, words/sec=11510.53, time=0-00:02:17)
[switchout.my-en] Epoch 2.4578: train_loss/word=6.024356 (steps=662, words/sec=10694.98, time=0-00:02:19)
[switchout.my-en] Epoch 2.5327: train_loss/word=6.027215 (steps=682, words/sec=10002.42, time=0-00:02:20)
[switchout.my-en] Epoch 2.6063: train_loss/word=5.945091 (steps=702, words/sec=11235.32, time=0-00:02:22)
[switchout.my-en] Epoch 2.6799: train_loss/word=6.002858 (steps=719, words/sec=11646.22, time=0-00:02:23)
[switchout.my-en] Epoch 2.7541: train_loss/word=5.987095 (steps=739, words/sec=10355.19, time=0-00:02:24)
[switchout.my-en] Epoch 2.8298: train_loss/word=5.988612 (steps=765, words/sec=8700.94, time=0-00:02:27)
[switchout.my-en] Epoch 2.9069: train_loss/word=5.916124 (steps=787, words/sec=10089.41, time=0-00:02:28)
[switchout.my-en] Epoch 2.9820: train_loss/word=5.891487 (steps=807, words/sec=10158.64, time=0-00:02:30)
[switchout.my-en] Epoch 3.0000: train_loss/word=6.028076 (steps=813, words/sec=7300.00, time=0-00:02:31)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 3.0000 dev BLEU4: 0.031240152013284044, 0.252704/0.043715/0.016171/0.006351 (BP = 0.957205, ratio=0.96, hyp_len=6379, ref_len=6658) (time=0-00:02:57)
[switchout.my-en]              dev auxiliary GLEU: 0.076706
[switchout.my-en]              dev auxiliary Loss: 5.524 (ref_len=6658)
             checkpoint took 0-00:00:26
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 3.0013: train_loss/word=5.986424 (steps=814, words/sec=3713.57, time=0-00:03:06)
[switchout.my-en] Epoch 3.0785: train_loss/word=5.707024 (steps=835, words/sec=11108.31, time=0-00:03:08)
[switchout.my-en] Epoch 3.1530: train_loss/word=5.738042 (steps=859, words/sec=8562.31, time=0-00:03:10)
[switchout.my-en] Epoch 3.2318: train_loss/word=5.742953 (steps=879, words/sec=11031.54, time=0-00:03:11)
[switchout.my-en] Epoch 3.3055: train_loss/word=5.690430 (steps=897, words/sec=12300.99, time=0-00:03:12)
[switchout.my-en] Epoch 3.3805: train_loss/word=5.736816 (steps=916, words/sec=11437.66, time=0-00:03:13)
[switchout.my-en] Epoch 3.4566: train_loss/word=5.703463 (steps=936, words/sec=11108.69, time=0-00:03:15)
[switchout.my-en] Epoch 3.5325: train_loss/word=5.778186 (steps=958, words/sec=9203.19, time=0-00:03:17)
[switchout.my-en] Epoch 3.6114: train_loss/word=5.734117 (steps=976, words/sec=11425.89, time=0-00:03:18)
[switchout.my-en] Epoch 3.6866: train_loss/word=5.665794 (steps=996, words/sec=10675.74, time=0-00:03:19)
[switchout.my-en] Epoch 3.7602: train_loss/word=5.682942 (steps=1019, words/sec=8734.10, time=0-00:03:21)
[switchout.my-en] Epoch 3.8343: train_loss/word=5.630496 (steps=1041, words/sec=10782.14, time=0-00:03:23)
[switchout.my-en] Epoch 3.9079: train_loss/word=5.621506 (steps=1061, words/sec=11147.65, time=0-00:03:24)
[switchout.my-en] Epoch 3.9853: train_loss/word=5.652243 (steps=1080, words/sec=10391.82, time=0-00:03:26)
[switchout.my-en] Epoch 4.0000: train_loss/word=5.640589 (steps=1084, words/sec=9642.60, time=0-00:03:26)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 4.0000 dev BLEU4: 0.04245759555990993, 0.290465/0.058213/0.025337/0.012739 (BP = 0.878426, ratio=0.89, hyp_len=5894, ref_len=6658) (time=0-00:03:49)
[switchout.my-en]              dev auxiliary GLEU: 0.089031
[switchout.my-en]              dev auxiliary Loss: 5.275 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 4.0045: train_loss/word=5.348275 (steps=1085, words/sec=10714.21, time=0-00:03:58)
[switchout.my-en] Epoch 4.0815: train_loss/word=5.522058 (steps=1103, words/sec=12375.36, time=0-00:03:59)
[switchout.my-en] Epoch 4.1562: train_loss/word=5.490745 (steps=1123, words/sec=10521.87, time=0-00:04:01)
[switchout.my-en] Epoch 4.2302: train_loss/word=5.493831 (steps=1143, words/sec=9782.49, time=0-00:04:02)
[switchout.my-en] Epoch 4.3061: train_loss/word=5.537450 (steps=1166, words/sec=7962.45, time=0-00:04:05)
[switchout.my-en] Epoch 4.3797: train_loss/word=5.421516 (steps=1185, words/sec=11234.88, time=0-00:04:06)
[switchout.my-en] Epoch 4.4545: train_loss/word=5.456902 (steps=1207, words/sec=10453.11, time=0-00:04:07)
[switchout.my-en] Epoch 4.5300: train_loss/word=5.478014 (steps=1227, words/sec=10356.26, time=0-00:04:09)
[switchout.my-en] Epoch 4.6057: train_loss/word=5.358328 (steps=1246, words/sec=11710.94, time=0-00:04:10)
[switchout.my-en] Epoch 4.6802: train_loss/word=5.440078 (steps=1268, words/sec=10116.00, time=0-00:04:12)
[switchout.my-en] Epoch 4.7575: train_loss/word=5.441076 (steps=1290, words/sec=10385.32, time=0-00:04:13)
[switchout.my-en] Epoch 4.8333: train_loss/word=5.459005 (steps=1309, words/sec=10543.69, time=0-00:04:15)
[switchout.my-en] Epoch 4.9076: train_loss/word=5.363194 (steps=1329, words/sec=11167.58, time=0-00:04:16)
[switchout.my-en] Epoch 4.9819: train_loss/word=5.419429 (steps=1349, words/sec=10526.77, time=0-00:04:18)
[switchout.my-en] Epoch 5.0000: train_loss/word=5.476481 (steps=1354, words/sec=11582.23, time=0-00:04:18)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 5.0000 dev BLEU4: 0.05692124247718581, 0.293205/0.071069/0.034063/0.019138 (BP = 0.937603, ratio=0.94, hyp_len=6255, ref_len=6658) (time=0-00:04:43)
[switchout.my-en]              dev auxiliary GLEU: 0.099109
[switchout.my-en]              dev auxiliary Loss: 5.129 (ref_len=6658)
             checkpoint took 0-00:00:24
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 5.0039: train_loss/word=5.350380 (steps=1355, words/sec=12866.07, time=0-00:04:52)
[switchout.my-en] Epoch 5.0800: train_loss/word=5.197561 (steps=1379, words/sec=10037.02, time=0-00:04:54)
[switchout.my-en] Epoch 5.1539: train_loss/word=5.296089 (steps=1397, words/sec=10786.68, time=0-00:04:55)
[switchout.my-en] Epoch 5.2301: train_loss/word=5.260787 (steps=1418, words/sec=10142.66, time=0-00:04:56)
[switchout.my-en] Epoch 5.3065: train_loss/word=5.268197 (steps=1435, words/sec=11942.42, time=0-00:04:57)
[switchout.my-en] Epoch 5.3806: train_loss/word=5.179915 (steps=1455, words/sec=11523.21, time=0-00:04:59)
[switchout.my-en] Epoch 5.4609: train_loss/word=5.287821 (steps=1476, words/sec=10202.24, time=0-00:05:00)
[switchout.my-en] Epoch 5.5365: train_loss/word=5.346175 (steps=1500, words/sec=9045.87, time=0-00:05:02)
[switchout.my-en] Epoch 5.6132: train_loss/word=5.266361 (steps=1520, words/sec=10569.56, time=0-00:05:04)
[switchout.my-en] Epoch 5.6917: train_loss/word=5.335898 (steps=1540, words/sec=9724.95, time=0-00:05:05)
[switchout.my-en] Epoch 5.7670: train_loss/word=5.263652 (steps=1561, words/sec=9656.75, time=0-00:05:07)
[switchout.my-en] Epoch 5.8414: train_loss/word=5.168498 (steps=1581, words/sec=11682.27, time=0-00:05:08)
[switchout.my-en] Epoch 5.9200: train_loss/word=5.300434 (steps=1603, words/sec=9601.61, time=0-00:05:10)
[switchout.my-en] Epoch 5.9954: train_loss/word=5.204600 (steps=1624, words/sec=10666.69, time=0-00:05:12)
[switchout.my-en] Epoch 6.0000: train_loss/word=5.020150 (steps=1625, words/sec=15310.55, time=0-00:05:12)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 6.0000 dev BLEU4: 0.062112503238781945, 0.322704/0.085311/0.040199/0.020534 (BP = 0.899608, ratio=0.90, hyp_len=6021, ref_len=6658) (time=0-00:05:36)
[switchout.my-en]              dev auxiliary GLEU: 0.108516
[switchout.my-en]              dev auxiliary Loss: 4.986 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 6.0030: train_loss/word=4.953006 (steps=1626, words/sec=11007.83, time=0-00:05:45)
[switchout.my-en] Epoch 6.0772: train_loss/word=5.096200 (steps=1647, words/sec=10002.08, time=0-00:05:46)
[switchout.my-en] Epoch 6.1527: train_loss/word=5.006128 (steps=1669, words/sec=10388.27, time=0-00:05:48)
[switchout.my-en] Epoch 6.2300: train_loss/word=5.188885 (steps=1690, words/sec=9658.08, time=0-00:05:49)
[switchout.my-en] Epoch 6.3047: train_loss/word=5.131610 (steps=1713, words/sec=8847.45, time=0-00:05:51)
[switchout.my-en] Epoch 6.3790: train_loss/word=5.150179 (steps=1733, words/sec=9961.86, time=0-00:05:53)
[switchout.my-en] Epoch 6.4538: train_loss/word=5.077112 (steps=1754, words/sec=9926.53, time=0-00:05:55)
[switchout.my-en] Epoch 6.5276: train_loss/word=5.038482 (steps=1775, words/sec=10804.88, time=0-00:05:56)
[switchout.my-en] Epoch 6.6044: train_loss/word=5.114046 (steps=1795, words/sec=11124.39, time=0-00:05:57)
[switchout.my-en] Epoch 6.6780: train_loss/word=5.108348 (steps=1813, words/sec=11227.01, time=0-00:05:59)
[switchout.my-en] Epoch 6.7517: train_loss/word=5.085814 (steps=1831, words/sec=12219.11, time=0-00:06:00)
[switchout.my-en] Epoch 6.8271: train_loss/word=5.093983 (steps=1852, words/sec=9714.44, time=0-00:06:01)
[switchout.my-en] Epoch 6.9023: train_loss/word=5.077186 (steps=1872, words/sec=10768.95, time=0-00:06:03)
[switchout.my-en] Epoch 6.9771: train_loss/word=5.149653 (steps=1892, words/sec=10026.44, time=0-00:06:04)
[switchout.my-en] Epoch 7.0000: train_loss/word=5.181107 (steps=1896, words/sec=17021.90, time=0-00:06:04)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 7.0000 dev BLEU4: 0.07897810793250712, 0.324996/0.097786/0.052099/0.030782 (BP = 0.934727, ratio=0.94, hyp_len=6237, ref_len=6658) (time=0-00:06:29)
[switchout.my-en]              dev auxiliary GLEU: 0.119094
[switchout.my-en]              dev auxiliary Loss: 4.898 (ref_len=6658)
             checkpoint took 0-00:00:24
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 7.0019: train_loss/word=4.972392 (steps=1897, words/sec=6900.49, time=0-00:06:38)
[switchout.my-en] Epoch 7.0767: train_loss/word=4.979226 (steps=1917, words/sec=9660.49, time=0-00:06:40)
[switchout.my-en] Epoch 7.1522: train_loss/word=4.839233 (steps=1941, words/sec=9144.20, time=0-00:06:42)
[switchout.my-en] Epoch 7.2278: train_loss/word=4.870557 (steps=1964, words/sec=10208.68, time=0-00:06:44)
[switchout.my-en] Epoch 7.3039: train_loss/word=4.920254 (steps=1984, words/sec=10183.89, time=0-00:06:45)
[switchout.my-en] Epoch 7.3776: train_loss/word=4.935116 (steps=2005, words/sec=10051.80, time=0-00:06:47)
[switchout.my-en] Epoch 7.4517: train_loss/word=4.980019 (steps=2024, words/sec=11888.61, time=0-00:06:48)
[switchout.my-en] Epoch 7.5324: train_loss/word=4.927564 (steps=2042, words/sec=12132.90, time=0-00:06:49)
[switchout.my-en] Epoch 7.6091: train_loss/word=4.898182 (steps=2064, words/sec=9644.48, time=0-00:06:51)
[switchout.my-en] Epoch 7.6830: train_loss/word=4.970691 (steps=2085, words/sec=10321.63, time=0-00:06:52)
[switchout.my-en] Epoch 7.7577: train_loss/word=4.857357 (steps=2102, words/sec=12361.46, time=0-00:06:53)
[switchout.my-en] Epoch 7.8361: train_loss/word=4.957514 (steps=2120, words/sec=12692.94, time=0-00:06:54)
[switchout.my-en] Epoch 7.9118: train_loss/word=4.987412 (steps=2142, words/sec=9869.37, time=0-00:06:56)
[switchout.my-en] Epoch 7.9877: train_loss/word=4.868769 (steps=2162, words/sec=11332.42, time=0-00:06:57)
[switchout.my-en] Epoch 8.0000: train_loss/word=5.047447 (steps=2167, words/sec=5475.44, time=0-00:06:58)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 8.0000 dev BLEU4: 0.08360765857899624, 0.327002/0.101957/0.052820/0.029077 (BP = 0.988368, ratio=0.99, hyp_len=6581, ref_len=6658) (time=0-00:07:24)
[switchout.my-en]              dev auxiliary GLEU: 0.124299
[switchout.my-en]              dev auxiliary Loss: 4.827 (ref_len=6658)
             checkpoint took 0-00:00:25
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 8.0024: train_loss/word=4.813824 (steps=2168, words/sec=8941.51, time=0-00:07:33)
[switchout.my-en] Epoch 8.0778: train_loss/word=4.647702 (steps=2190, words/sec=10787.32, time=0-00:07:35)
[switchout.my-en] Epoch 8.1537: train_loss/word=4.781069 (steps=2211, words/sec=10367.00, time=0-00:07:36)
[switchout.my-en] Epoch 8.2280: train_loss/word=4.767803 (steps=2235, words/sec=9338.77, time=0-00:07:38)
[switchout.my-en] Epoch 8.3048: train_loss/word=4.774080 (steps=2254, words/sec=10831.67, time=0-00:07:39)
[switchout.my-en] Epoch 8.3820: train_loss/word=4.777337 (steps=2274, words/sec=11931.57, time=0-00:07:41)
[switchout.my-en] Epoch 8.4569: train_loss/word=4.685150 (steps=2293, words/sec=11566.76, time=0-00:07:42)
[switchout.my-en] Epoch 8.5331: train_loss/word=4.789318 (steps=2316, words/sec=9457.76, time=0-00:07:44)
[switchout.my-en] Epoch 8.6136: train_loss/word=4.759075 (steps=2339, words/sec=9955.02, time=0-00:07:46)
[switchout.my-en] Epoch 8.6931: train_loss/word=4.786823 (steps=2358, words/sec=11479.33, time=0-00:07:47)
[switchout.my-en] Epoch 8.7728: train_loss/word=4.846546 (steps=2380, words/sec=10193.11, time=0-00:07:49)
[switchout.my-en] Epoch 8.8469: train_loss/word=4.801493 (steps=2398, words/sec=10903.88, time=0-00:07:50)
[switchout.my-en] Epoch 8.9246: train_loss/word=4.872773 (steps=2417, words/sec=10129.44, time=0-00:07:51)
[switchout.my-en] Epoch 9.0000: train_loss/word=4.875549 (steps=2438, words/sec=9489.45, time=0-00:07:53)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 9.0000 dev BLEU4: 0.09486908325942713, 0.368792/0.126316/0.071295/0.043418 (BP = 0.865729, ratio=0.87, hyp_len=5819, ref_len=6658) (time=0-00:08:16)
[switchout.my-en]              dev auxiliary GLEU: 0.136218
[switchout.my-en]              dev auxiliary Loss: 4.775 (ref_len=6658)
             checkpoint took 0-00:00:22
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 9.0060: train_loss/word=4.837711 (steps=2439, words/sec=17377.03, time=0-00:08:25)
[switchout.my-en] Epoch 9.0800: train_loss/word=4.572650 (steps=2460, words/sec=10517.97, time=0-00:08:26)
[switchout.my-en] Epoch 9.1602: train_loss/word=4.684499 (steps=2480, words/sec=11819.35, time=0-00:08:28)
[switchout.my-en] Epoch 9.2344: train_loss/word=4.657639 (steps=2499, words/sec=10545.52, time=0-00:08:29)
[switchout.my-en] Epoch 9.3118: train_loss/word=4.675306 (steps=2520, words/sec=10031.62, time=0-00:08:31)
[switchout.my-en] Epoch 9.3868: train_loss/word=4.565484 (steps=2542, words/sec=10289.83, time=0-00:08:32)
[switchout.my-en] Epoch 9.4627: train_loss/word=4.667374 (steps=2564, words/sec=9878.51, time=0-00:08:34)
[switchout.my-en] Epoch 9.5383: train_loss/word=4.705441 (steps=2586, words/sec=8804.27, time=0-00:08:36)
[switchout.my-en] Epoch 9.6137: train_loss/word=4.646555 (steps=2607, words/sec=11048.58, time=0-00:08:37)
[switchout.my-en] Epoch 9.6906: train_loss/word=4.616094 (steps=2625, words/sec=11659.46, time=0-00:08:38)
[switchout.my-en] Epoch 9.7673: train_loss/word=4.661777 (steps=2645, words/sec=10994.48, time=0-00:08:40)
[switchout.my-en] Epoch 9.8424: train_loss/word=4.600236 (steps=2665, words/sec=11107.30, time=0-00:08:41)
[switchout.my-en] Epoch 9.9177: train_loss/word=4.629465 (steps=2684, words/sec=11073.78, time=0-00:08:42)
[switchout.my-en] Epoch 9.9916: train_loss/word=4.679911 (steps=2707, words/sec=9012.05, time=0-00:08:44)
[switchout.my-en] Epoch 10.0000: train_loss/word=4.458101 (steps=2709, words/sec=12132.83, time=0-00:08:45)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 10.0000 dev BLEU4: 0.10999001209937286, 0.375101/0.135948/0.079191/0.049212 (BP = 0.926376, ratio=0.93, hyp_len=6185, ref_len=6658) (time=0-00:09:08)
[switchout.my-en]              dev auxiliary GLEU: 0.149114
[switchout.my-en]              dev auxiliary Loss: 4.729 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 10.0024: train_loss/word=4.799545 (steps=2710, words/sec=9050.81, time=0-00:09:17)
[switchout.my-en] Epoch 10.0781: train_loss/word=4.470439 (steps=2731, words/sec=10653.35, time=0-00:09:19)
[switchout.my-en] Epoch 10.1524: train_loss/word=4.462941 (steps=2754, words/sec=8955.10, time=0-00:09:21)
[switchout.my-en] Epoch 10.2282: train_loss/word=4.527555 (steps=2774, words/sec=10874.25, time=0-00:09:22)
[switchout.my-en] Epoch 10.3060: train_loss/word=4.454044 (steps=2794, words/sec=11177.09, time=0-00:09:24)
[switchout.my-en] Epoch 10.3813: train_loss/word=4.409518 (steps=2815, words/sec=10722.84, time=0-00:09:25)
[switchout.my-en] Epoch 10.4556: train_loss/word=4.561665 (steps=2838, words/sec=8660.26, time=0-00:09:27)
[switchout.my-en] Epoch 10.5296: train_loss/word=4.513081 (steps=2860, words/sec=10017.29, time=0-00:09:29)
[switchout.my-en] Epoch 10.6034: train_loss/word=4.561209 (steps=2882, words/sec=9629.30, time=0-00:09:31)
[switchout.my-en] Epoch 10.6787: train_loss/word=4.664849 (steps=2898, words/sec=11950.39, time=0-00:09:32)
[switchout.my-en] Epoch 10.7540: train_loss/word=4.545874 (steps=2917, words/sec=11544.02, time=0-00:09:33)
[switchout.my-en] Epoch 10.8302: train_loss/word=4.618510 (steps=2935, words/sec=11209.51, time=0-00:09:34)
[switchout.my-en] Epoch 10.9072: train_loss/word=4.573230 (steps=2955, words/sec=10748.29, time=0-00:09:36)
[switchout.my-en] Epoch 10.9818: train_loss/word=4.506099 (steps=2974, words/sec=11256.38, time=0-00:09:37)
[switchout.my-en] Epoch 11.0000: train_loss/word=4.542444 (steps=2980, words/sec=9384.37, time=0-00:09:37)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 11.0000 dev BLEU4: 0.11896427979663199, 0.379711/0.144732/0.086340/0.053378 (BP = 0.943014, ratio=0.94, hyp_len=6289, ref_len=6658) (time=0-00:10:01)
[switchout.my-en]              dev auxiliary GLEU: 0.155440
[switchout.my-en]              dev auxiliary Loss: 4.642 (ref_len=6658)
             checkpoint took 0-00:00:24
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 11.0013: train_loss/word=4.578781 (steps=2981, words/sec=3769.82, time=0-00:10:11)
[switchout.my-en] Epoch 11.0778: train_loss/word=4.280808 (steps=3003, words/sec=11151.52, time=0-00:10:12)
[switchout.my-en] Epoch 11.1546: train_loss/word=4.309491 (steps=3024, words/sec=10652.42, time=0-00:10:14)
[switchout.my-en] Epoch 11.2307: train_loss/word=4.366200 (steps=3047, words/sec=10338.26, time=0-00:10:15)
[switchout.my-en] Epoch 11.3139: train_loss/word=4.548009 (steps=3065, words/sec=11021.50, time=0-00:10:17)
[switchout.my-en] Epoch 11.3918: train_loss/word=4.381491 (steps=3085, words/sec=10731.45, time=0-00:10:18)
[switchout.my-en] Epoch 11.4661: train_loss/word=4.434947 (steps=3105, words/sec=10275.99, time=0-00:10:19)
[switchout.my-en] Epoch 11.5430: train_loss/word=4.392711 (steps=3126, words/sec=10280.14, time=0-00:10:21)
[switchout.my-en] Epoch 11.6196: train_loss/word=4.327725 (steps=3147, words/sec=11039.05, time=0-00:10:22)
[switchout.my-en] Epoch 11.6934: train_loss/word=4.433697 (steps=3169, words/sec=9150.47, time=0-00:10:24)
[switchout.my-en] Epoch 11.7673: train_loss/word=4.398401 (steps=3188, words/sec=10249.06, time=0-00:10:26)
[switchout.my-en] Epoch 11.8417: train_loss/word=4.399427 (steps=3211, words/sec=9231.68, time=0-00:10:28)
[switchout.my-en] Epoch 11.9173: train_loss/word=4.409471 (steps=3229, words/sec=12421.94, time=0-00:10:29)
[switchout.my-en] Epoch 11.9924: train_loss/word=4.355608 (steps=3249, words/sec=10528.94, time=0-00:10:30)
[switchout.my-en] Epoch 12.0000: train_loss/word=4.271779 (steps=3251, words/sec=11830.03, time=0-00:10:30)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 12.0000 dev BLEU4: 0.13266440057911935, 0.392801/0.159331/0.096738/0.061627 (BP = 0.954540, ratio=0.96, hyp_len=6362, ref_len=6658) (time=0-00:10:54)
[switchout.my-en]              dev auxiliary GLEU: 0.167553
[switchout.my-en]              dev auxiliary Loss: 4.602 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 12.0032: train_loss/word=4.144129 (steps=3252, words/sec=10463.69, time=0-00:11:03)
[switchout.my-en] Epoch 12.0775: train_loss/word=4.190510 (steps=3273, words/sec=9246.22, time=0-00:11:05)
[switchout.my-en] Epoch 12.1522: train_loss/word=4.267960 (steps=3294, words/sec=9411.40, time=0-00:11:06)
[switchout.my-en] Epoch 12.2284: train_loss/word=4.244552 (steps=3314, words/sec=11104.64, time=0-00:11:08)
[switchout.my-en] Epoch 12.3033: train_loss/word=4.311871 (steps=3333, words/sec=10730.38, time=0-00:11:09)
[switchout.my-en] Epoch 12.3774: train_loss/word=4.292078 (steps=3353, words/sec=10592.40, time=0-00:11:11)
[switchout.my-en] Epoch 12.4519: train_loss/word=4.328423 (steps=3374, words/sec=10579.85, time=0-00:11:12)
[switchout.my-en] Epoch 12.5300: train_loss/word=4.219994 (steps=3396, words/sec=11104.11, time=0-00:11:14)
[switchout.my-en] Epoch 12.6062: train_loss/word=4.272991 (steps=3417, words/sec=9599.91, time=0-00:11:15)
[switchout.my-en] Epoch 12.6814: train_loss/word=4.273849 (steps=3437, words/sec=11380.68, time=0-00:11:17)
[switchout.my-en] Epoch 12.7567: train_loss/word=4.427850 (steps=3460, words/sec=8843.19, time=0-00:11:19)
[switchout.my-en] Epoch 12.8334: train_loss/word=4.304467 (steps=3481, words/sec=10502.76, time=0-00:11:20)
[switchout.my-en] Epoch 12.9126: train_loss/word=4.259719 (steps=3502, words/sec=11075.10, time=0-00:11:22)
[switchout.my-en] Epoch 12.9882: train_loss/word=4.352907 (steps=3519, words/sec=12299.55, time=0-00:11:23)
[switchout.my-en] Epoch 13.0000: train_loss/word=4.400640 (steps=3522, words/sec=11549.74, time=0-00:11:23)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 13.0000 dev BLEU4: 0.13370023639034484, 0.408324/0.167890/0.099502/0.061958 (BP = 0.932485, ratio=0.93, hyp_len=6223, ref_len=6658) (time=0-00:11:47)
[switchout.my-en]              dev auxiliary GLEU: 0.171400
[switchout.my-en]              dev auxiliary Loss: 4.551 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 13.0031: train_loss/word=4.111768 (steps=3523, words/sec=10392.22, time=0-00:11:56)
[switchout.my-en] Epoch 13.0781: train_loss/word=4.115644 (steps=3545, words/sec=9582.93, time=0-00:11:57)
[switchout.my-en] Epoch 13.1546: train_loss/word=4.097724 (steps=3566, words/sec=10349.11, time=0-00:11:59)
[switchout.my-en] Epoch 13.2301: train_loss/word=4.186526 (steps=3587, words/sec=9366.56, time=0-00:12:01)
[switchout.my-en] Epoch 13.3042: train_loss/word=4.308279 (steps=3605, words/sec=10911.81, time=0-00:12:02)
[switchout.my-en] Epoch 13.3808: train_loss/word=4.132761 (steps=3624, words/sec=11928.81, time=0-00:12:03)
[switchout.my-en] Epoch 13.4603: train_loss/word=4.164750 (steps=3642, words/sec=12368.67, time=0-00:12:04)
[switchout.my-en] Epoch 13.5372: train_loss/word=4.153459 (steps=3664, words/sec=10296.06, time=0-00:12:06)
[switchout.my-en] Epoch 13.6112: train_loss/word=4.128637 (steps=3684, words/sec=11153.46, time=0-00:12:07)
[switchout.my-en] Epoch 13.6847: train_loss/word=4.154460 (steps=3704, words/sec=10967.04, time=0-00:12:09)
[switchout.my-en] Epoch 13.7602: train_loss/word=4.195046 (steps=3726, words/sec=9030.41, time=0-00:12:11)
[switchout.my-en] Epoch 13.8378: train_loss/word=4.190577 (steps=3749, words/sec=10471.66, time=0-00:12:12)
[switchout.my-en] Epoch 13.9174: train_loss/word=4.198018 (steps=3771, words/sec=9933.25, time=0-00:12:14)
[switchout.my-en] Epoch 13.9938: train_loss/word=4.146199 (steps=3792, words/sec=11147.73, time=0-00:12:15)
[switchout.my-en] Epoch 14.0000: train_loss/word=4.476255 (steps=3793, words/sec=19947.83, time=0-00:12:15)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 14.0000 dev BLEU4: 0.14274097338699074, 0.409383/0.174357/0.105322/0.066038 (BP = 0.956265, ratio=0.96, hyp_len=6373, ref_len=6658) (time=0-00:12:40)
[switchout.my-en]              dev auxiliary GLEU: 0.177183
[switchout.my-en]              dev auxiliary Loss: 4.529 (ref_len=6658)
             checkpoint took 0-00:00:24
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 14.0031: train_loss/word=4.082676 (steps=3794, words/sec=10094.48, time=0-00:12:49)
[switchout.my-en] Epoch 14.0777: train_loss/word=3.979868 (steps=3815, words/sec=9695.73, time=0-00:12:50)
[switchout.my-en] Epoch 14.1546: train_loss/word=4.082284 (steps=3836, words/sec=10018.66, time=0-00:12:52)
[switchout.my-en] Epoch 14.2288: train_loss/word=4.012745 (steps=3855, words/sec=11123.05, time=0-00:12:53)
[switchout.my-en] Epoch 14.3030: train_loss/word=4.086635 (steps=3875, words/sec=9364.60, time=0-00:12:55)
[switchout.my-en] Epoch 14.3790: train_loss/word=4.053846 (steps=3895, words/sec=10148.49, time=0-00:12:56)
[switchout.my-en] Epoch 14.4527: train_loss/word=4.143661 (steps=3913, words/sec=10725.83, time=0-00:12:58)
[switchout.my-en] Epoch 14.5271: train_loss/word=4.004833 (steps=3934, words/sec=10990.44, time=0-00:12:59)
[switchout.my-en] Epoch 14.6014: train_loss/word=4.069454 (steps=3955, words/sec=9089.56, time=0-00:13:01)
[switchout.my-en] Epoch 14.6753: train_loss/word=4.105670 (steps=3976, words/sec=10294.10, time=0-00:13:02)
[switchout.my-en] Epoch 14.7528: train_loss/word=4.110546 (steps=3996, words/sec=11222.33, time=0-00:13:04)
[switchout.my-en] Epoch 14.8280: train_loss/word=4.085918 (steps=4018, words/sec=10592.90, time=0-00:13:05)
[switchout.my-en] Epoch 14.9023: train_loss/word=4.083118 (steps=4038, words/sec=11118.60, time=0-00:13:07)
[switchout.my-en] Epoch 14.9779: train_loss/word=4.048986 (steps=4058, words/sec=11169.42, time=0-00:13:08)
[switchout.my-en] Epoch 15.0000: train_loss/word=3.967985 (steps=4064, words/sec=10572.58, time=0-00:13:09)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 15.0000 dev BLEU4: 0.15006031622072488, 0.408798/0.176613/0.108160/0.064933 (BP = 1.000000, ratio=1.00, hyp_len=6683, ref_len=6658) (time=0-00:13:34)
[switchout.my-en]              dev auxiliary GLEU: 0.184167
[switchout.my-en]              dev auxiliary Loss: 4.506 (ref_len=6658)
             checkpoint took 0-00:00:25
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 15.0032: train_loss/word=3.991217 (steps=4065, words/sec=9805.98, time=0-00:13:43)
[switchout.my-en] Epoch 15.0783: train_loss/word=3.880443 (steps=4086, words/sec=10173.11, time=0-00:13:44)
[switchout.my-en] Epoch 15.1531: train_loss/word=3.942420 (steps=4106, words/sec=10125.67, time=0-00:13:46)
[switchout.my-en] Epoch 15.2273: train_loss/word=3.950100 (steps=4124, words/sec=12853.63, time=0-00:13:47)
[switchout.my-en] Epoch 15.3024: train_loss/word=4.014163 (steps=4141, words/sec=12030.76, time=0-00:13:48)
[switchout.my-en] Epoch 15.3765: train_loss/word=3.964571 (steps=4162, words/sec=9642.95, time=0-00:13:49)
[switchout.my-en] Epoch 15.4534: train_loss/word=3.976922 (steps=4184, words/sec=10143.33, time=0-00:13:51)
[switchout.my-en] Epoch 15.5291: train_loss/word=4.063851 (steps=4203, words/sec=10387.47, time=0-00:13:53)
[switchout.my-en] Epoch 15.6039: train_loss/word=3.964702 (steps=4225, words/sec=9703.54, time=0-00:13:54)
[switchout.my-en] Epoch 15.6836: train_loss/word=3.969154 (steps=4247, words/sec=10418.33, time=0-00:13:56)
[switchout.my-en] Epoch 15.7581: train_loss/word=3.876906 (steps=4269, words/sec=10662.66, time=0-00:13:57)
[switchout.my-en] Epoch 15.8362: train_loss/word=3.976072 (steps=4290, words/sec=10519.36, time=0-00:13:59)
[switchout.my-en] Epoch 15.9136: train_loss/word=3.968748 (steps=4311, words/sec=10663.14, time=0-00:14:01)
[switchout.my-en] Epoch 15.9883: train_loss/word=4.122631 (steps=4331, words/sec=9491.23, time=0-00:14:02)
[switchout.my-en] Epoch 16.0000: train_loss/word=3.846886 (steps=4335, words/sec=9225.21, time=0-00:14:02)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 16.0000 dev BLEU4: 0.16175611762689995, 0.443560/0.199576/0.127738/0.083834 (BP = 0.921852, ratio=0.92, hyp_len=6157, ref_len=6658) (time=0-00:14:26)
[switchout.my-en]              dev auxiliary GLEU: 0.194571
[switchout.my-en]              dev auxiliary Loss: 4.475 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 16.0053: train_loss/word=3.687126 (steps=4336, words/sec=16154.64, time=0-00:14:35)
[switchout.my-en] Epoch 16.0838: train_loss/word=3.797474 (steps=4360, words/sec=9787.50, time=0-00:14:37)
[switchout.my-en] Epoch 16.1585: train_loss/word=3.828542 (steps=4382, words/sec=9254.25, time=0-00:14:38)
[switchout.my-en] Epoch 16.2343: train_loss/word=3.820215 (steps=4403, words/sec=10973.89, time=0-00:14:40)
[switchout.my-en] Epoch 16.3081: train_loss/word=3.847504 (steps=4421, words/sec=11132.43, time=0-00:14:41)
[switchout.my-en] Epoch 16.3837: train_loss/word=3.849521 (steps=4442, words/sec=10502.33, time=0-00:14:43)
[switchout.my-en] Epoch 16.4575: train_loss/word=3.819761 (steps=4463, words/sec=10654.90, time=0-00:14:44)
[switchout.my-en] Epoch 16.5312: train_loss/word=3.898975 (steps=4483, words/sec=10475.44, time=0-00:14:46)
[switchout.my-en] Epoch 16.6061: train_loss/word=3.894212 (steps=4500, words/sec=12125.27, time=0-00:14:47)
[switchout.my-en] Epoch 16.6822: train_loss/word=3.840678 (steps=4520, words/sec=10565.85, time=0-00:14:48)
[switchout.my-en] Epoch 16.7557: train_loss/word=3.857987 (steps=4539, words/sec=10962.70, time=0-00:14:50)
[switchout.my-en] Epoch 16.8312: train_loss/word=3.907104 (steps=4559, words/sec=10913.31, time=0-00:14:51)
[switchout.my-en] Epoch 16.9070: train_loss/word=3.924180 (steps=4577, words/sec=12244.60, time=0-00:14:52)
[switchout.my-en] Epoch 16.9834: train_loss/word=3.928059 (steps=4600, words/sec=8943.12, time=0-00:14:54)
[switchout.my-en] Epoch 17.0000: train_loss/word=3.810658 (steps=4605, words/sec=10674.38, time=0-00:14:54)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 17.0000 dev BLEU4: 0.1700943320880795, 0.463471/0.214631/0.135650/0.090020 (BP = 0.911113, ratio=0.91, hyp_len=6091, ref_len=6658) (time=0-00:15:17)
[switchout.my-en]              dev auxiliary GLEU: 0.205424
[switchout.my-en]              dev auxiliary Loss: 4.447 (ref_len=6658)
             checkpoint took 0-00:00:22
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 17.0071: train_loss/word=3.982985 (steps=4606, words/sec=18183.73, time=0-00:15:26)
[switchout.my-en] Epoch 17.0812: train_loss/word=3.671791 (steps=4628, words/sec=9855.25, time=0-00:15:28)
[switchout.my-en] Epoch 17.1558: train_loss/word=3.782772 (steps=4649, words/sec=9706.76, time=0-00:15:29)
[switchout.my-en] Epoch 17.2302: train_loss/word=3.732526 (steps=4666, words/sec=13015.46, time=0-00:15:30)
[switchout.my-en] Epoch 17.3055: train_loss/word=3.794472 (steps=4687, words/sec=9290.23, time=0-00:15:32)
[switchout.my-en] Epoch 17.3800: train_loss/word=3.758581 (steps=4706, words/sec=11885.88, time=0-00:15:33)
[switchout.my-en] Epoch 17.4545: train_loss/word=3.782431 (steps=4725, words/sec=10453.59, time=0-00:15:35)
[switchout.my-en] Epoch 17.5348: train_loss/word=3.771456 (steps=4746, words/sec=10997.49, time=0-00:15:36)
[switchout.my-en] Epoch 17.6098: train_loss/word=3.709952 (steps=4769, words/sec=10605.88, time=0-00:15:38)
[switchout.my-en] Epoch 17.6870: train_loss/word=3.721459 (steps=4790, words/sec=11373.32, time=0-00:15:39)
[switchout.my-en] Epoch 17.7624: train_loss/word=3.811831 (steps=4811, words/sec=10666.91, time=0-00:15:41)
[switchout.my-en] Epoch 17.8403: train_loss/word=3.814667 (steps=4832, words/sec=9539.51, time=0-00:15:43)
[switchout.my-en] Epoch 17.9151: train_loss/word=3.889434 (steps=4852, words/sec=9930.14, time=0-00:15:44)
[switchout.my-en] Epoch 17.9932: train_loss/word=3.807553 (steps=4873, words/sec=10290.73, time=0-00:15:46)
[switchout.my-en] Epoch 18.0000: train_loss/word=3.936872 (steps=4875, words/sec=9538.27, time=0-00:15:46)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 18.0000 dev BLEU4: 0.18813230411292, 0.460559/0.221521/0.145705/0.101375 (BP = 0.954853, ratio=0.96, hyp_len=6364, ref_len=6658) (time=0-00:16:09)
[switchout.my-en]              dev auxiliary GLEU: 0.216201
[switchout.my-en]              dev auxiliary Loss: 4.420 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 18.0025: train_loss/word=3.495489 (steps=4876, words/sec=8820.32, time=0-00:16:18)
[switchout.my-en] Epoch 18.0768: train_loss/word=3.571071 (steps=4900, words/sec=9475.04, time=0-00:16:20)
[switchout.my-en] Epoch 18.1537: train_loss/word=3.696102 (steps=4920, words/sec=10539.99, time=0-00:16:22)
[switchout.my-en] Epoch 18.2303: train_loss/word=3.745081 (steps=4937, words/sec=12918.62, time=0-00:16:23)
[switchout.my-en] Epoch 18.3055: train_loss/word=3.652610 (steps=4959, words/sec=10507.74, time=0-00:16:24)
[switchout.my-en] Epoch 18.3796: train_loss/word=3.726160 (steps=4976, words/sec=12769.91, time=0-00:16:25)
[switchout.my-en] Epoch 18.4552: train_loss/word=3.721593 (steps=4997, words/sec=9620.05, time=0-00:16:27)
[switchout.my-en] Epoch 18.5302: train_loss/word=3.622375 (steps=5019, words/sec=10228.54, time=0-00:16:29)
[switchout.my-en] Epoch 18.6059: train_loss/word=3.850900 (steps=5037, words/sec=8945.71, time=0-00:16:30)
[switchout.my-en] Epoch 18.6832: train_loss/word=3.770731 (steps=5058, words/sec=11056.89, time=0-00:16:32)
[switchout.my-en] Epoch 18.7578: train_loss/word=3.786296 (steps=5078, words/sec=10741.57, time=0-00:16:33)
[switchout.my-en] Epoch 18.8320: train_loss/word=3.729551 (steps=5099, words/sec=9805.54, time=0-00:16:35)
[switchout.my-en] Epoch 18.9076: train_loss/word=3.715335 (steps=5120, words/sec=11033.92, time=0-00:16:36)
[switchout.my-en] Epoch 18.9816: train_loss/word=3.744464 (steps=5140, words/sec=10794.60, time=0-00:16:38)
[switchout.my-en] Epoch 19.0000: train_loss/word=3.688807 (steps=5145, words/sec=11572.78, time=0-00:16:38)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 19.0000 dev BLEU4: 0.18775674206388068, 0.469868/0.231646/0.148687/0.097104 (BP = 0.943014, ratio=0.94, hyp_len=6289, ref_len=6658) (time=0-00:17:01)
[switchout.my-en]              dev auxiliary GLEU: 0.220803
[switchout.my-en]              dev auxiliary Loss: 4.413 (ref_len=6658)
             checkpoint took 0-00:00:23
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 19.0031: train_loss/word=3.426126 (steps=5146, words/sec=10591.07, time=0-00:17:04)
[switchout.my-en] Epoch 19.0778: train_loss/word=3.490455 (steps=5166, words/sec=11026.80, time=0-00:17:05)
[switchout.my-en] Epoch 19.1563: train_loss/word=3.583302 (steps=5186, words/sec=11222.60, time=0-00:17:07)
[switchout.my-en] Epoch 19.2326: train_loss/word=3.518723 (steps=5207, words/sec=10539.16, time=0-00:17:08)
[switchout.my-en] Epoch 19.3072: train_loss/word=3.653263 (steps=5231, words/sec=8597.22, time=0-00:17:10)
[switchout.my-en] Epoch 19.3834: train_loss/word=3.642777 (steps=5248, words/sec=10566.14, time=0-00:17:11)
[switchout.my-en] Epoch 19.4575: train_loss/word=3.758187 (steps=5266, words/sec=10702.05, time=0-00:17:13)
[switchout.my-en] Epoch 19.5317: train_loss/word=3.618598 (steps=5287, words/sec=10421.21, time=0-00:17:14)
[switchout.my-en] Epoch 19.6062: train_loss/word=3.604353 (steps=5309, words/sec=9960.21, time=0-00:17:16)
[switchout.my-en] Epoch 19.6823: train_loss/word=3.595279 (steps=5331, words/sec=9859.38, time=0-00:17:18)
[switchout.my-en] Epoch 19.7573: train_loss/word=3.631418 (steps=5353, words/sec=10139.84, time=0-00:17:19)
[switchout.my-en] Epoch 19.8348: train_loss/word=3.700772 (steps=5374, words/sec=10627.74, time=0-00:17:21)
[switchout.my-en] Epoch 19.9094: train_loss/word=3.655729 (steps=5392, words/sec=10974.21, time=0-00:17:22)
[switchout.my-en] Epoch 19.9847: train_loss/word=3.669287 (steps=5411, words/sec=12664.18, time=0-00:17:23)
[switchout.my-en] Epoch 20.0000: train_loss/word=3.773443 (steps=5416, words/sec=8486.02, time=0-00:17:24)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 20.0000 dev BLEU4: 0.19789512909015602, 0.483461/0.237733/0.156303/0.108029 (BP = 0.942856, ratio=0.94, hyp_len=6288, ref_len=6658) (time=0-00:17:47)
[switchout.my-en]              dev auxiliary GLEU: 0.229467
[switchout.my-en]              dev auxiliary Loss: 4.356 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 20.0032: train_loss/word=3.220897 (steps=5417, words/sec=10681.29, time=0-00:17:56)
[switchout.my-en] Epoch 20.0774: train_loss/word=3.563558 (steps=5437, words/sec=9234.91, time=0-00:17:57)
[switchout.my-en] Epoch 20.1521: train_loss/word=3.432261 (steps=5461, words/sec=9467.10, time=0-00:17:59)
[switchout.my-en] Epoch 20.2307: train_loss/word=3.577038 (steps=5481, words/sec=10684.62, time=0-00:18:01)
[switchout.my-en] Epoch 20.3056: train_loss/word=3.538883 (steps=5500, words/sec=11288.94, time=0-00:18:02)
[switchout.my-en] Epoch 20.3821: train_loss/word=3.551050 (steps=5521, words/sec=11095.13, time=0-00:18:04)
[switchout.my-en] Epoch 20.4596: train_loss/word=3.549078 (steps=5540, words/sec=11163.48, time=0-00:18:05)
[switchout.my-en] Epoch 20.5342: train_loss/word=3.628338 (steps=5562, words/sec=9889.09, time=0-00:18:07)
[switchout.my-en] Epoch 20.6109: train_loss/word=3.595994 (steps=5580, words/sec=11274.06, time=0-00:18:08)
[switchout.my-en] Epoch 20.6871: train_loss/word=3.565343 (steps=5599, words/sec=11435.51, time=0-00:18:09)
[switchout.my-en] Epoch 20.7682: train_loss/word=3.573058 (steps=5622, words/sec=10651.80, time=0-00:18:11)
[switchout.my-en] Epoch 20.8429: train_loss/word=3.545401 (steps=5640, words/sec=12400.73, time=0-00:18:12)
[switchout.my-en] Epoch 20.9175: train_loss/word=3.604237 (steps=5664, words/sec=9143.48, time=0-00:18:14)
[switchout.my-en] Epoch 20.9929: train_loss/word=3.607536 (steps=5685, words/sec=9394.81, time=0-00:18:16)
[switchout.my-en] Epoch 21.0000: train_loss/word=3.494965 (steps=5687, words/sec=12090.41, time=0-00:18:16)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 21.0000 dev BLEU4: 0.2009207678746329, 0.494521/0.249036/0.160875/0.110074 (BP = 0.929756, ratio=0.93, hyp_len=6206, ref_len=6658) (time=0-00:18:39)
[switchout.my-en]              dev auxiliary GLEU: 0.233964
[switchout.my-en]              dev auxiliary Loss: 4.389 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 21.0044: train_loss/word=3.337028 (steps=5688, words/sec=14820.35, time=0-00:18:48)
[switchout.my-en] Epoch 21.0795: train_loss/word=3.562659 (steps=5706, words/sec=10138.12, time=0-00:18:49)
[switchout.my-en] Epoch 21.1569: train_loss/word=3.352147 (steps=5728, words/sec=10722.87, time=0-00:18:51)
[switchout.my-en] Epoch 21.2326: train_loss/word=3.289595 (steps=5751, words/sec=9670.70, time=0-00:18:52)
[switchout.my-en] Epoch 21.3095: train_loss/word=3.454341 (steps=5769, words/sec=12239.54, time=0-00:18:54)
[switchout.my-en] Epoch 21.3849: train_loss/word=3.458465 (steps=5789, words/sec=10304.62, time=0-00:18:55)
[switchout.my-en] Epoch 21.4612: train_loss/word=3.430626 (steps=5810, words/sec=10669.17, time=0-00:18:57)
[switchout.my-en] Epoch 21.5369: train_loss/word=3.562254 (steps=5831, words/sec=10017.50, time=0-00:18:58)
[switchout.my-en] Epoch 21.6111: train_loss/word=3.534841 (steps=5851, words/sec=10385.43, time=0-00:19:00)
[switchout.my-en] Epoch 21.6874: train_loss/word=3.457186 (steps=5875, words/sec=9649.07, time=0-00:19:02)
[switchout.my-en] Epoch 21.7616: train_loss/word=3.527319 (steps=5897, words/sec=9452.71, time=0-00:19:03)
[switchout.my-en] Epoch 21.8360: train_loss/word=3.441997 (steps=5917, words/sec=11200.18, time=0-00:19:05)
[switchout.my-en] Epoch 21.9125: train_loss/word=3.582114 (steps=5937, words/sec=11662.10, time=0-00:19:06)
[switchout.my-en] Epoch 21.9864: train_loss/word=3.634266 (steps=5954, words/sec=11033.80, time=0-00:19:07)
[switchout.my-en] Epoch 22.0000: train_loss/word=3.523126 (steps=5958, words/sec=10485.21, time=0-00:19:08)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 22.0000 dev BLEU4: 0.21285057806529922, 0.497621/0.256203/0.170373/0.118295 (BP = 0.945393, ratio=0.95, hyp_len=6304, ref_len=6658) (time=0-00:19:31)
[switchout.my-en]              dev auxiliary GLEU: 0.242928
[switchout.my-en]              dev auxiliary Loss: 4.361 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 22.0028: train_loss/word=3.481942 (steps=5959, words/sec=9571.20, time=0-00:19:40)
[switchout.my-en] Epoch 22.0789: train_loss/word=3.351442 (steps=5978, words/sec=11370.60, time=0-00:19:41)
[switchout.my-en] Epoch 22.1535: train_loss/word=3.315891 (steps=6000, words/sec=9834.06, time=0-00:19:43)
[switchout.my-en] Epoch 22.2301: train_loss/word=3.474865 (steps=6019, words/sec=11421.94, time=0-00:19:44)
[switchout.my-en] Epoch 22.3047: train_loss/word=3.353055 (steps=6037, words/sec=11569.56, time=0-00:19:45)
[switchout.my-en] Epoch 22.3796: train_loss/word=3.364380 (steps=6060, words/sec=9306.48, time=0-00:19:47)
[switchout.my-en] Epoch 22.4542: train_loss/word=3.449457 (steps=6080, words/sec=9665.74, time=0-00:19:49)
[switchout.my-en] Epoch 22.5285: train_loss/word=3.362202 (steps=6100, words/sec=10881.87, time=0-00:19:50)
[switchout.my-en] Epoch 22.6026: train_loss/word=3.384470 (steps=6121, words/sec=10184.42, time=0-00:19:52)
[switchout.my-en] Epoch 22.6774: train_loss/word=3.427529 (steps=6142, words/sec=10455.33, time=0-00:19:53)
[switchout.my-en] Epoch 22.7530: train_loss/word=3.477232 (steps=6162, words/sec=9790.45, time=0-00:19:55)
[switchout.my-en] Epoch 22.8266: train_loss/word=3.466654 (steps=6182, words/sec=10154.62, time=0-00:19:56)
[switchout.my-en] Epoch 22.9003: train_loss/word=3.474298 (steps=6202, words/sec=10078.69, time=0-00:19:58)
[switchout.my-en] Epoch 22.9752: train_loss/word=3.457744 (steps=6221, words/sec=12385.55, time=0-00:19:59)
[switchout.my-en] Epoch 23.0000: train_loss/word=3.458589 (steps=6229, words/sec=9946.57, time=0-00:20:00)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 23.0000 dev BLEU4: 0.21132317864145658, 0.505758/0.259910/0.168982/0.116411 (BP = 0.937124, ratio=0.94, hyp_len=6252, ref_len=6658) (time=0-00:20:23)
[switchout.my-en]              dev auxiliary GLEU: 0.243211
[switchout.my-en]              dev auxiliary Loss: 4.354 (ref_len=6658)
             checkpoint took 0-00:00:23
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 23.0032: train_loss/word=3.214133 (steps=6230, words/sec=9772.64, time=0-00:20:26)
[switchout.my-en] Epoch 23.0774: train_loss/word=3.362481 (steps=6249, words/sec=9752.09, time=0-00:20:27)
[switchout.my-en] Epoch 23.1530: train_loss/word=3.374827 (steps=6267, words/sec=9901.25, time=0-00:20:28)
[switchout.my-en] Epoch 23.2316: train_loss/word=3.271513 (steps=6290, words/sec=10629.14, time=0-00:20:30)
[switchout.my-en] Epoch 23.3064: train_loss/word=3.315266 (steps=6310, words/sec=11305.08, time=0-00:20:32)
[switchout.my-en] Epoch 23.3821: train_loss/word=3.500534 (steps=6328, words/sec=10607.13, time=0-00:20:33)
[switchout.my-en] Epoch 23.4579: train_loss/word=3.392300 (steps=6348, words/sec=10686.27, time=0-00:20:34)
[switchout.my-en] Epoch 23.5338: train_loss/word=3.398557 (steps=6369, words/sec=10450.22, time=0-00:20:36)
[switchout.my-en] Epoch 23.6080: train_loss/word=3.325084 (steps=6392, words/sec=9734.05, time=0-00:20:38)
[switchout.my-en] Epoch 23.6825: train_loss/word=3.323455 (steps=6414, words/sec=10618.57, time=0-00:20:39)
[switchout.my-en] Epoch 23.7613: train_loss/word=3.249381 (steps=6434, words/sec=12119.36, time=0-00:20:41)
[switchout.my-en] Epoch 23.8364: train_loss/word=3.392689 (steps=6456, words/sec=9280.57, time=0-00:20:42)
[switchout.my-en] Epoch 23.9105: train_loss/word=3.355819 (steps=6475, words/sec=10840.81, time=0-00:20:44)
[switchout.my-en] Epoch 23.9872: train_loss/word=3.427894 (steps=6496, words/sec=10093.89, time=0-00:20:45)
[switchout.my-en] Epoch 24.0000: train_loss/word=3.228503 (steps=6500, words/sec=10409.99, time=0-00:20:45)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 24.0000 dev BLEU4: 0.21199079373637555, 0.503326/0.256794/0.168140/0.115560 (BP = 0.946975, ratio=0.95, hyp_len=6314, ref_len=6658) (time=0-00:21:09)
[switchout.my-en]              dev auxiliary GLEU: 0.242850
[switchout.my-en]              dev auxiliary Loss: 4.347 (ref_len=6658)
             checkpoint took 0-00:00:23
  new learning rate: 0.5
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 24.0082: train_loss/word=4.219769 (steps=6501, words/sec=20837.23, time=0-00:21:12)
[switchout.my-en] Epoch 24.0821: train_loss/word=3.221654 (steps=6522, words/sec=10627.49, time=0-00:21:13)
[switchout.my-en] Epoch 24.1578: train_loss/word=3.204981 (steps=6540, words/sec=10899.99, time=0-00:21:15)
[switchout.my-en] Epoch 24.2320: train_loss/word=3.241372 (steps=6560, words/sec=11082.95, time=0-00:21:16)
[switchout.my-en] Epoch 24.3064: train_loss/word=3.200806 (steps=6580, words/sec=10676.70, time=0-00:21:17)
[switchout.my-en] Epoch 24.3812: train_loss/word=3.142343 (steps=6602, words/sec=10218.31, time=0-00:21:19)
[switchout.my-en] Epoch 24.4548: train_loss/word=3.221485 (steps=6623, words/sec=10001.58, time=0-00:21:21)
[switchout.my-en] Epoch 24.5285: train_loss/word=3.261273 (steps=6642, words/sec=10327.24, time=0-00:21:22)
[switchout.my-en] Epoch 24.6031: train_loss/word=3.189961 (steps=6663, words/sec=10883.68, time=0-00:21:24)
[switchout.my-en] Epoch 24.6782: train_loss/word=3.165249 (steps=6682, words/sec=11039.06, time=0-00:21:25)
[switchout.my-en] Epoch 24.7525: train_loss/word=3.243113 (steps=6703, words/sec=9620.81, time=0-00:21:27)
[switchout.my-en] Epoch 24.8298: train_loss/word=3.183095 (steps=6726, words/sec=9401.08, time=0-00:21:28)
[switchout.my-en] Epoch 24.9038: train_loss/word=3.294840 (steps=6745, words/sec=10913.51, time=0-00:21:30)
[switchout.my-en] Epoch 24.9837: train_loss/word=3.265806 (steps=6766, words/sec=9985.10, time=0-00:21:31)
[switchout.my-en] Epoch 25.0000: train_loss/word=3.099186 (steps=6771, words/sec=10222.23, time=0-00:21:32)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 25.0000 dev BLEU4: 0.22238950222738113, 0.512051/0.269211/0.179799/0.126834 (BP = 0.939198, ratio=0.94, hyp_len=6265, ref_len=6658) (time=0-00:21:55)
[switchout.my-en]              dev auxiliary GLEU: 0.251946
[switchout.my-en]              dev auxiliary Loss: 4.315 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 25.0082: train_loss/word=3.736386 (steps=6772, words/sec=21572.01, time=0-00:22:04)
[switchout.my-en] Epoch 25.0820: train_loss/word=3.272821 (steps=6786, words/sec=13398.74, time=0-00:22:05)
[switchout.my-en] Epoch 25.1557: train_loss/word=3.133332 (steps=6807, words/sec=10241.38, time=0-00:22:06)
[switchout.my-en] Epoch 25.2314: train_loss/word=3.192252 (steps=6827, words/sec=10586.09, time=0-00:22:08)
[switchout.my-en] Epoch 25.3065: train_loss/word=3.174277 (steps=6847, words/sec=10697.78, time=0-00:22:09)
[switchout.my-en] Epoch 25.3813: train_loss/word=3.089225 (steps=6869, words/sec=9978.75, time=0-00:22:11)
[switchout.my-en] Epoch 25.4618: train_loss/word=3.108987 (steps=6891, words/sec=10775.76, time=0-00:22:12)
[switchout.my-en] Epoch 25.5354: train_loss/word=3.126503 (steps=6911, words/sec=10358.84, time=0-00:22:14)
[switchout.my-en] Epoch 25.6100: train_loss/word=3.172770 (steps=6930, words/sec=12091.99, time=0-00:22:15)
[switchout.my-en] Epoch 25.6848: train_loss/word=3.206212 (steps=6949, words/sec=11295.91, time=0-00:22:16)
[switchout.my-en] Epoch 25.7617: train_loss/word=3.106982 (steps=6972, words/sec=8936.66, time=0-00:22:18)
[switchout.my-en] Epoch 25.8354: train_loss/word=3.171381 (steps=6993, words/sec=10671.46, time=0-00:22:20)
[switchout.my-en] Epoch 25.9094: train_loss/word=3.118802 (steps=7014, words/sec=10836.31, time=0-00:22:21)
[switchout.my-en] Epoch 25.9844: train_loss/word=3.215399 (steps=7037, words/sec=8845.80, time=0-00:22:23)
[switchout.my-en] Epoch 26.0000: train_loss/word=3.153555 (steps=7042, words/sec=8881.02, time=0-00:22:24)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 26.0000 dev BLEU4: 0.22202818802457366, 0.517713/0.272855/0.181661/0.126378 (BP = 0.930399, ratio=0.93, hyp_len=6210, ref_len=6658) (time=0-00:22:47)
[switchout.my-en]              dev auxiliary GLEU: 0.252267
[switchout.my-en]              dev auxiliary Loss: 4.317 (ref_len=6658)
             checkpoint took 0-00:00:23
  new learning rate: 0.25
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 26.0078: train_loss/word=3.862043 (steps=7043, words/sec=21995.36, time=0-00:22:50)
[switchout.my-en] Epoch 26.0838: train_loss/word=3.090889 (steps=7063, words/sec=10278.55, time=0-00:22:51)
[switchout.my-en] Epoch 26.1580: train_loss/word=3.085721 (steps=7081, words/sec=12557.64, time=0-00:22:52)
[switchout.my-en] Epoch 26.2328: train_loss/word=2.975319 (steps=7102, words/sec=11235.05, time=0-00:22:54)
[switchout.my-en] Epoch 26.3075: train_loss/word=3.107998 (steps=7122, words/sec=10843.44, time=0-00:22:55)
[switchout.my-en] Epoch 26.3835: train_loss/word=3.136653 (steps=7140, words/sec=10190.17, time=0-00:22:57)
[switchout.my-en] Epoch 26.4605: train_loss/word=3.065718 (steps=7163, words/sec=9877.58, time=0-00:22:58)
[switchout.my-en] Epoch 26.5382: train_loss/word=3.032361 (steps=7186, words/sec=9941.96, time=0-00:23:00)
[switchout.my-en] Epoch 26.6129: train_loss/word=3.173268 (steps=7204, words/sec=11669.13, time=0-00:23:01)
[switchout.my-en] Epoch 26.6872: train_loss/word=3.147134 (steps=7224, words/sec=10346.26, time=0-00:23:03)
[switchout.my-en] Epoch 26.7634: train_loss/word=3.058649 (steps=7244, words/sec=10091.85, time=0-00:23:04)
[switchout.my-en] Epoch 26.8387: train_loss/word=3.061683 (steps=7265, words/sec=10000.01, time=0-00:23:06)
[switchout.my-en] Epoch 26.9136: train_loss/word=3.064118 (steps=7287, words/sec=10107.93, time=0-00:23:07)
[switchout.my-en] Epoch 26.9884: train_loss/word=3.054204 (steps=7309, words/sec=9843.67, time=0-00:23:09)
[switchout.my-en] Epoch 27.0000: train_loss/word=3.154230 (steps=7312, words/sec=11900.93, time=0-00:23:09)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 27.0000 dev BLEU4: 0.22891812887481092, 0.517436/0.274463/0.181632/0.127900 (BP = 0.955167, ratio=0.96, hyp_len=6366, ref_len=6658) (time=0-00:23:33)
[switchout.my-en]              dev auxiliary GLEU: 0.257760
[switchout.my-en]              dev auxiliary Loss: 4.290 (ref_len=6658)
             checkpoint took 0-00:00:23
  best dev score, writing out model
Starting to read ./data/train.my and ./data/train.en
Done reading ./data/train.my and ./data/train.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 27.0036: train_loss/word=3.219322 (steps=7313, words/sec=10466.64, time=0-00:23:42)
[switchout.my-en] Epoch 27.0814: train_loss/word=2.936779 (steps=7337, words/sec=9434.68, time=0-00:23:44)
[switchout.my-en] Epoch 27.1575: train_loss/word=3.045483 (steps=7357, words/sec=10697.91, time=0-00:23:45)
[switchout.my-en] Epoch 27.2323: train_loss/word=2.974236 (steps=7381, words/sec=8815.40, time=0-00:23:47)
[switchout.my-en] Epoch 27.3062: train_loss/word=3.069798 (steps=7399, words/sec=10829.30, time=0-00:23:49)
[switchout.my-en] Epoch 27.3823: train_loss/word=3.093437 (steps=7419, words/sec=10364.60, time=0-00:23:50)
[switchout.my-en] Epoch 27.4565: train_loss/word=3.053819 (steps=7441, words/sec=9228.07, time=0-00:23:52)
[switchout.my-en] Epoch 27.5304: train_loss/word=2.898344 (steps=7464, words/sec=9304.39, time=0-00:23:54)
[switchout.my-en] Epoch 27.6102: train_loss/word=3.123353 (steps=7485, words/sec=10495.50, time=0-00:23:55)
[switchout.my-en] Epoch 27.6854: train_loss/word=3.096622 (steps=7505, words/sec=10814.84, time=0-00:23:57)
[switchout.my-en] Epoch 27.7616: train_loss/word=3.154150 (steps=7523, words/sec=11911.12, time=0-00:23:58)
[switchout.my-en] Epoch 27.8412: train_loss/word=3.079800 (steps=7543, words/sec=11614.14, time=0-00:23:59)
[switchout.my-en] Epoch 27.9154: train_loss/word=3.089527 (steps=7561, words/sec=11730.80, time=0-00:24:01)
[switchout.my-en] Epoch 27.9907: train_loss/word=3.103528 (steps=7580, words/sec=10607.69, time=0-00:24:02)
[switchout.my-en] Epoch 28.0000: train_loss/word=2.820757 (steps=7583, words/sec=9903.33, time=0-00:24:02)
> Checkpoint [switchout.my-en]
Performing inference on ./data/dev.my and ./data/dev.en
Starting to read ./data/dev.my and ./data/dev.en
Done reading ./data/dev.my and ./data/dev.en. Packing into batches.
Done packing batches.
[switchout.my-en] Epoch 28.0000 dev BLEU4: 0.22603841565029836, 0.519840/0.276000/0.183549/0.128707 (BP = 0.936805, ratio=0.94, hyp_len=6250, ref_len=6658) (time=0-00:24:26)
[switchout.my-en]              dev auxiliary GLEU: 0.255978
[switchout.my-en]              dev auxiliary Loss: 4.286 (ref_len=6658)
             checkpoint took 0-00:00:23
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.my and ./data/dev.en
Performing inference on ./data/test.my and ./data/test.en
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.my-en               | BLEU4: 0.22891812887481092, 0.517436/0.274463/0.181632/0.127900 (BP = 0.955167, ratio=0.96, hyp_len=6366, ref_len=6658)
                              | GLEU: 0.257760
                              | WER: 65.18% ( C/S/I/D: 2983/2718/665/957; hyp_len=6366, ref_len=6658 )
                              | CER: 59.26% ( C/S/I/D: 13597/7683/2684/5506; hyp_len=23964, ref_len=26786 )
                              | BLEU4: 0.2322950876367574, 0.516022/0.275094/0.184313/0.131793 (BP = 0.958606, ratio=0.96, hyp_len=6647, ref_len=6928)
                              | GLEU: 0.260500
                              | WER: 64.78% ( C/S/I/D: 3068/2951/628/909; hyp_len=6647, ref_len=6928 )
                              | CER: 58.63% ( C/S/I/D: 14094/8108/2700/5339; hyp_len=24902, ref_len=27541 )
```

ပထမ run ခဲ့တဲ့ experiment တုန်းက ရခဲ့တဲ့ (word, no data-argumentation, my-en) က အောက်ပါအတိုင်း...  

```
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.my-en                 | BLEU4: 0.23651943640021703, 0.513891/0.271322/0.184702/0.132669 (BP = 0.978290, ratio=0.98, hyp_len=6515, ref_len=6658)
                              | GLEU: 0.262422
                              | WER: 65.06% ( C/S/I/D: 2996/2849/670/813; hyp_len=6515, ref_len=6658 )
                              | CER: 59.09% ( C/S/I/D: 13643/8225/2686/4918; hyp_len=24554, ref_len=26786 )
                              | BLEU4: 0.22773123029482975, 0.506559/0.268524/0.178953/0.125983 (BP = 0.967735, ratio=0.97, hyp_len=6708, ref_len=6928)
                              | GLEU: 0.256017
                              | WER: 64.97% ( C/S/I/D: 3089/2957/662/882; hyp_len=6708, ref_len=6928 )
                              | CER: 59.00% ( C/S/I/D: 14100/8166/2809/5275; hyp_len=25075, ref_len=27541 )
```

***အထက်ပါ ရလဒ် နှစ်ခုကို နှိုင်းယှဉ်ကြည့်ရင် dev မှာက switchout က မသာပေမဲ့ testing မှာ သာပါတယ်။  :)***  

## Updating Config File for Syllable Unit (en-my)

ပြောရရင် အထက်က word unit, en-my အတွက်တုန်းက သုံးခဲ့တဲ့ config ဖိုင်နဲ့ အတူတူပါပဲ။  
နာမည်ကိုပဲ အောက်ပါအတိုင်း ပြောင်းခဲ့တယ်။  

```yaml
switchout.syl.en-my: !Experiment
```

## Training for Syllable-SwitchOut (en-my)

syllable unit နဲ့ ဆိုရင် ရလဒ်က ပိုကောင်းမယ်လို့ မျှော်လင့်တယ်။ run ကြည့်ကြရအောင်...   

```
(xnmt-py3.6) ye@ye-System-Product-Name:~/tool/xnmt/exp/medical1/syl_switchout$ time xnmt --backend torch --gpu ./config.switchout.en-my-word.yaml | tee switchout.en-my.log1
running XNMT revision d93f8f3 on ye-System-Product-Name with PyTorch on 2022-05-03 16:57:57
=> Running switchout.syl.en-my
> Preprocessing
> use randomly initialized neural network parameters for all components
  neural network param count: 15725870
> Training
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 0.0748: train_loss/word=6.600142 (steps=22, words/sec=11193.72, time=0-00:00:06)
[switchout.syl.en-my] Epoch 0.1488: train_loss/word=6.204799 (steps=44, words/sec=12319.36, time=0-00:00:08)
[switchout.syl.en-my] Epoch 0.2228: train_loss/word=6.142360 (steps=64, words/sec=12024.14, time=0-00:00:10)
[switchout.syl.en-my] Epoch 0.2971: train_loss/word=6.068276 (steps=88, words/sec=11113.28, time=0-00:00:13)
[switchout.syl.en-my] Epoch 0.3725: train_loss/word=5.896748 (steps=113, words/sec=11716.70, time=0-00:00:16)
[switchout.syl.en-my] Epoch 0.4474: train_loss/word=5.714019 (steps=134, words/sec=13771.04, time=0-00:00:18)
[switchout.syl.en-my] Epoch 0.5211: train_loss/word=5.590586 (steps=156, words/sec=12856.84, time=0-00:00:20)
[switchout.syl.en-my] Epoch 0.5949: train_loss/word=5.451092 (steps=179, words/sec=11510.18, time=0-00:00:22)
[switchout.syl.en-my] Epoch 0.6706: train_loss/word=5.341688 (steps=203, words/sec=10947.50, time=0-00:00:25)
[switchout.syl.en-my] Epoch 0.7457: train_loss/word=5.202961 (steps=225, words/sec=12543.12, time=0-00:00:27)
[switchout.syl.en-my] Epoch 0.8195: train_loss/word=5.160759 (steps=247, words/sec=11822.83, time=0-00:00:29)
[switchout.syl.en-my] Epoch 0.8935: train_loss/word=5.106708 (steps=272, words/sec=10916.27, time=0-00:00:32)
[switchout.syl.en-my] Epoch 0.9670: train_loss/word=4.983754 (steps=294, words/sec=12367.44, time=0-00:00:34)
[switchout.syl.en-my] Epoch 1.0000: train_loss/word=5.055214 (steps=304, words/sec=11026.93, time=0-00:00:35)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 1.0000 dev BLEU4: 0.01433681136143846, 0.080592/0.030695/0.008852/0.001929 (BP = 1.000000, ratio=2.20, hyp_len=28452, ref_len=12957) (time=0-00:01:59)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.029590
[switchout.syl.en-my]              dev auxiliary Loss: 4.760 (ref_len=12957)
             checkpoint took 0-00:01:23
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 1.0029: train_loss/word=5.081064 (steps=305, words/sec=12878.30, time=0-00:02:11)
[switchout.syl.en-my] Epoch 1.0776: train_loss/word=4.970377 (steps=327, words/sec=12097.79, time=0-00:02:13)
[switchout.syl.en-my] Epoch 1.1525: train_loss/word=4.862243 (steps=348, words/sec=13375.49, time=0-00:02:15)
[switchout.syl.en-my] Epoch 1.2288: train_loss/word=4.832123 (steps=373, words/sec=11967.62, time=0-00:02:18)
[switchout.syl.en-my] Epoch 1.3078: train_loss/word=4.818702 (steps=397, words/sec=11452.59, time=0-00:02:21)
[switchout.syl.en-my] Epoch 1.3838: train_loss/word=4.794497 (steps=420, words/sec=11623.31, time=0-00:02:23)
[switchout.syl.en-my] Epoch 1.4595: train_loss/word=4.695942 (steps=441, words/sec=13354.73, time=0-00:02:25)
[switchout.syl.en-my] Epoch 1.5343: train_loss/word=4.655045 (steps=464, words/sec=12132.32, time=0-00:02:27)
[switchout.syl.en-my] Epoch 1.6093: train_loss/word=4.639504 (steps=487, words/sec=12769.09, time=0-00:02:29)
[switchout.syl.en-my] Epoch 1.6850: train_loss/word=4.616884 (steps=512, words/sec=11656.71, time=0-00:02:32)
[switchout.syl.en-my] Epoch 1.7585: train_loss/word=4.556861 (steps=534, words/sec=12734.93, time=0-00:02:34)
[switchout.syl.en-my] Epoch 1.8346: train_loss/word=4.547848 (steps=557, words/sec=12099.03, time=0-00:02:37)
[switchout.syl.en-my] Epoch 1.9111: train_loss/word=4.558160 (steps=580, words/sec=11902.94, time=0-00:02:39)
[switchout.syl.en-my] Epoch 1.9846: train_loss/word=4.401505 (steps=602, words/sec=11747.93, time=0-00:02:41)
[switchout.syl.en-my] Epoch 2.0000: train_loss/word=4.534295 (steps=608, words/sec=11597.15, time=0-00:02:42)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 2.0000 dev BLEU4: 0.06451367753947944, 0.250879/0.105624/0.040809/0.016019 (BP = 1.000000, ratio=1.14, hyp_len=14796, ref_len=12957) (time=0-00:03:27)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.092722
[switchout.syl.en-my]              dev auxiliary Loss: 4.217 (ref_len=12957)
             checkpoint took 0-00:00:45
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 2.0026: train_loss/word=4.578211 (steps=609, words/sec=6698.87, time=0-00:03:33)
[switchout.syl.en-my] Epoch 2.0808: train_loss/word=4.387340 (steps=634, words/sec=11715.78, time=0-00:03:36)
[switchout.syl.en-my] Epoch 2.1560: train_loss/word=4.384007 (steps=654, words/sec=13382.75, time=0-00:03:37)
[switchout.syl.en-my] Epoch 2.2307: train_loss/word=4.360498 (steps=678, words/sec=11822.09, time=0-00:03:40)
[switchout.syl.en-my] Epoch 2.3097: train_loss/word=4.341584 (steps=703, words/sec=11246.25, time=0-00:03:43)
[switchout.syl.en-my] Epoch 2.3834: train_loss/word=4.283053 (steps=725, words/sec=12597.67, time=0-00:03:45)
[switchout.syl.en-my] Epoch 2.4573: train_loss/word=4.317719 (steps=744, words/sec=14045.66, time=0-00:03:46)
[switchout.syl.en-my] Epoch 2.5324: train_loss/word=4.263313 (steps=767, words/sec=12094.03, time=0-00:03:49)
[switchout.syl.en-my] Epoch 2.6079: train_loss/word=4.260797 (steps=787, words/sec=12890.87, time=0-00:03:51)
[switchout.syl.en-my] Epoch 2.6844: train_loss/word=4.233573 (steps=815, words/sec=10895.08, time=0-00:03:54)
[switchout.syl.en-my] Epoch 2.7594: train_loss/word=4.208749 (steps=836, words/sec=12071.12, time=0-00:03:56)
[switchout.syl.en-my] Epoch 2.8341: train_loss/word=4.197261 (steps=860, words/sec=11631.60, time=0-00:03:59)
[switchout.syl.en-my] Epoch 2.9127: train_loss/word=4.205889 (steps=885, words/sec=11459.23, time=0-00:04:01)
[switchout.syl.en-my] Epoch 2.9864: train_loss/word=4.202344 (steps=907, words/sec=11753.64, time=0-00:04:04)
[switchout.syl.en-my] Epoch 3.0000: train_loss/word=4.134276 (steps=912, words/sec=9424.29, time=0-00:04:04)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 3.0000 dev BLEU4: 0.11592956445215172, 0.400299/0.193124/0.091146/0.044640 (BP = 0.870510, ratio=0.88, hyp_len=11379, ref_len=12957) (time=0-00:04:40)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.155715
[switchout.syl.en-my]              dev auxiliary Loss: 3.885 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 3.0046: train_loss/word=4.003398 (steps=913, words/sec=16629.03, time=0-00:04:46)
[switchout.syl.en-my] Epoch 3.0838: train_loss/word=4.040811 (steps=936, words/sec=13973.98, time=0-00:04:48)
[switchout.syl.en-my] Epoch 3.1601: train_loss/word=4.119657 (steps=960, words/sec=12094.20, time=0-00:04:51)
[switchout.syl.en-my] Epoch 3.2347: train_loss/word=4.090252 (steps=983, words/sec=11288.18, time=0-00:04:53)
[switchout.syl.en-my] Epoch 3.3083: train_loss/word=4.016608 (steps=1005, words/sec=13231.23, time=0-00:04:55)
[switchout.syl.en-my] Epoch 3.3834: train_loss/word=4.015719 (steps=1031, words/sec=11123.01, time=0-00:04:58)
[switchout.syl.en-my] Epoch 3.4577: train_loss/word=4.046572 (steps=1051, words/sec=13357.97, time=0-00:05:00)
[switchout.syl.en-my] Epoch 3.5322: train_loss/word=4.023245 (steps=1074, words/sec=12036.65, time=0-00:05:02)
[switchout.syl.en-my] Epoch 3.6077: train_loss/word=3.947874 (steps=1097, words/sec=12786.54, time=0-00:05:05)
[switchout.syl.en-my] Epoch 3.6830: train_loss/word=3.929566 (steps=1120, words/sec=12292.44, time=0-00:05:07)
[switchout.syl.en-my] Epoch 3.7602: train_loss/word=3.949227 (steps=1144, words/sec=11819.61, time=0-00:05:10)
[switchout.syl.en-my] Epoch 3.8373: train_loss/word=3.984590 (steps=1164, words/sec=13056.20, time=0-00:05:11)
[switchout.syl.en-my] Epoch 3.9111: train_loss/word=3.932285 (steps=1186, words/sec=12066.12, time=0-00:05:13)
[switchout.syl.en-my] Epoch 3.9853: train_loss/word=3.916850 (steps=1212, words/sec=11562.57, time=0-00:05:16)
[switchout.syl.en-my] Epoch 4.0000: train_loss/word=3.860302 (steps=1216, words/sec=13551.94, time=0-00:05:17)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 4.0000 dev BLEU4: 0.14838044359907143, 0.460272/0.248341/0.130078/0.074178 (BP = 0.814218, ratio=0.83, hyp_len=10748, ref_len=12957) (time=0-00:05:51)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.184955
[switchout.syl.en-my]              dev auxiliary Loss: 3.630 (ref_len=12957)
             checkpoint took 0-00:00:34
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 4.0016: train_loss/word=3.830293 (steps=1217, words/sec=6920.31, time=0-00:05:57)
[switchout.syl.en-my] Epoch 4.0755: train_loss/word=3.848020 (steps=1235, words/sec=14741.53, time=0-00:05:58)
[switchout.syl.en-my] Epoch 4.1513: train_loss/word=3.862052 (steps=1257, words/sec=13139.01, time=0-00:06:00)
[switchout.syl.en-my] Epoch 4.2254: train_loss/word=3.746354 (steps=1278, words/sec=13800.86, time=0-00:06:02)
[switchout.syl.en-my] Epoch 4.3008: train_loss/word=3.760861 (steps=1300, words/sec=12442.38, time=0-00:06:04)
[switchout.syl.en-my] Epoch 4.3791: train_loss/word=3.810612 (steps=1327, words/sec=10550.19, time=0-00:06:07)
[switchout.syl.en-my] Epoch 4.4565: train_loss/word=3.772641 (steps=1350, words/sec=12302.16, time=0-00:06:10)
[switchout.syl.en-my] Epoch 4.5330: train_loss/word=3.773395 (steps=1373, words/sec=12219.29, time=0-00:06:12)
[switchout.syl.en-my] Epoch 4.6104: train_loss/word=3.798978 (steps=1397, words/sec=12423.72, time=0-00:06:15)
[switchout.syl.en-my] Epoch 4.6855: train_loss/word=3.783849 (steps=1422, words/sec=11475.57, time=0-00:06:17)
[switchout.syl.en-my] Epoch 4.7620: train_loss/word=3.761565 (steps=1449, words/sec=11886.60, time=0-00:06:20)
[switchout.syl.en-my] Epoch 4.8375: train_loss/word=3.716258 (steps=1469, words/sec=12971.60, time=0-00:06:22)
[switchout.syl.en-my] Epoch 4.9128: train_loss/word=3.690955 (steps=1490, words/sec=14042.56, time=0-00:06:24)
[switchout.syl.en-my] Epoch 4.9877: train_loss/word=3.760478 (steps=1516, words/sec=11846.01, time=0-00:06:27)
[switchout.syl.en-my] Epoch 5.0000: train_loss/word=3.786955 (steps=1520, words/sec=10193.52, time=0-00:06:27)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 5.0000 dev BLEU4: 0.18413813413224742, 0.437426/0.245809/0.137949/0.083267 (BP = 0.982248, ratio=0.98, hyp_len=12729, ref_len=12957) (time=0-00:07:05)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.200631
[switchout.syl.en-my]              dev auxiliary Loss: 3.462 (ref_len=12957)
             checkpoint took 0-00:00:38
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 5.0034: train_loss/word=3.410530 (steps=1521, words/sec=13046.57, time=0-00:07:11)
[switchout.syl.en-my] Epoch 5.0786: train_loss/word=3.577874 (steps=1543, words/sec=12558.98, time=0-00:07:13)
[switchout.syl.en-my] Epoch 5.1544: train_loss/word=3.600766 (steps=1567, words/sec=12466.69, time=0-00:07:16)
[switchout.syl.en-my] Epoch 5.2292: train_loss/word=3.613901 (steps=1588, words/sec=12911.59, time=0-00:07:18)
[switchout.syl.en-my] Epoch 5.3036: train_loss/word=3.583521 (steps=1610, words/sec=12617.53, time=0-00:07:20)
[switchout.syl.en-my] Epoch 5.3802: train_loss/word=3.620489 (steps=1632, words/sec=13165.29, time=0-00:07:22)
[switchout.syl.en-my] Epoch 5.4548: train_loss/word=3.543717 (steps=1653, words/sec=13462.86, time=0-00:07:24)
[switchout.syl.en-my] Epoch 5.5302: train_loss/word=3.595792 (steps=1678, words/sec=12054.22, time=0-00:07:26)
[switchout.syl.en-my] Epoch 5.6053: train_loss/word=3.578821 (steps=1705, words/sec=11515.31, time=0-00:07:29)
[switchout.syl.en-my] Epoch 5.6800: train_loss/word=3.582787 (steps=1729, words/sec=11363.96, time=0-00:07:32)
[switchout.syl.en-my] Epoch 5.7557: train_loss/word=3.608103 (steps=1753, words/sec=10936.94, time=0-00:07:35)
[switchout.syl.en-my] Epoch 5.8313: train_loss/word=3.581877 (steps=1775, words/sec=12954.41, time=0-00:07:37)
[switchout.syl.en-my] Epoch 5.9055: train_loss/word=3.613597 (steps=1799, words/sec=12332.80, time=0-00:07:39)
[switchout.syl.en-my] Epoch 5.9815: train_loss/word=3.592754 (steps=1819, words/sec=13024.91, time=0-00:07:41)
[switchout.syl.en-my] Epoch 6.0000: train_loss/word=3.753053 (steps=1825, words/sec=10321.85, time=0-00:07:42)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 6.0000 dev BLEU4: 0.21428030367202697, 0.472563/0.275267/0.160492/0.100986 (BP = 1.000000, ratio=1.00, hyp_len=12957, ref_len=12957) (time=0-00:08:21)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.231962
[switchout.syl.en-my]              dev auxiliary Loss: 3.325 (ref_len=12957)
             checkpoint took 0-00:00:39
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 6.0032: train_loss/word=3.437036 (steps=1826, words/sec=11846.60, time=0-00:08:27)
[switchout.syl.en-my] Epoch 6.0781: train_loss/word=3.511097 (steps=1849, words/sec=12075.86, time=0-00:08:29)
[switchout.syl.en-my] Epoch 6.1549: train_loss/word=3.411993 (steps=1872, words/sec=12285.38, time=0-00:08:31)
[switchout.syl.en-my] Epoch 6.2286: train_loss/word=3.502457 (steps=1895, words/sec=11808.93, time=0-00:08:34)
[switchout.syl.en-my] Epoch 6.3031: train_loss/word=3.508384 (steps=1917, words/sec=12760.84, time=0-00:08:36)
[switchout.syl.en-my] Epoch 6.3777: train_loss/word=3.448094 (steps=1938, words/sec=13028.10, time=0-00:08:38)
[switchout.syl.en-my] Epoch 6.4526: train_loss/word=3.470186 (steps=1960, words/sec=13260.66, time=0-00:08:40)
[switchout.syl.en-my] Epoch 6.5296: train_loss/word=3.460788 (steps=1985, words/sec=11303.22, time=0-00:08:43)
[switchout.syl.en-my] Epoch 6.6062: train_loss/word=3.422988 (steps=2010, words/sec=11609.19, time=0-00:08:45)
[switchout.syl.en-my] Epoch 6.6814: train_loss/word=3.433834 (steps=2034, words/sec=12394.74, time=0-00:08:48)
[switchout.syl.en-my] Epoch 6.7590: train_loss/word=3.431132 (steps=2056, words/sec=11725.45, time=0-00:08:50)
[switchout.syl.en-my] Epoch 6.8349: train_loss/word=3.389575 (steps=2080, words/sec=12569.18, time=0-00:08:52)
[switchout.syl.en-my] Epoch 6.9112: train_loss/word=3.377868 (steps=2103, words/sec=13239.56, time=0-00:08:55)
[switchout.syl.en-my] Epoch 6.9865: train_loss/word=3.506286 (steps=2126, words/sec=11185.00, time=0-00:08:57)
[switchout.syl.en-my] Epoch 7.0000: train_loss/word=3.537042 (steps=2129, words/sec=13486.21, time=0-00:08:57)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 7.0000 dev BLEU4: 0.22900682023362806, 0.537662/0.326878/0.198009/0.128657 (BP = 0.885309, ratio=0.89, hyp_len=11550, ref_len=12957) (time=0-00:09:33)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.252582
[switchout.syl.en-my]              dev auxiliary Loss: 3.228 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 7.0016: train_loss/word=3.494090 (steps=2130, words/sec=7902.56, time=0-00:09:40)
[switchout.syl.en-my] Epoch 7.0791: train_loss/word=3.291922 (steps=2152, words/sec=12545.77, time=0-00:09:42)
[switchout.syl.en-my] Epoch 7.1560: train_loss/word=3.237431 (steps=2172, words/sec=13604.97, time=0-00:09:43)
[switchout.syl.en-my] Epoch 7.2303: train_loss/word=3.326496 (steps=2199, words/sec=10450.10, time=0-00:09:47)
[switchout.syl.en-my] Epoch 7.3056: train_loss/word=3.305080 (steps=2219, words/sec=14300.94, time=0-00:09:48)
[switchout.syl.en-my] Epoch 7.3804: train_loss/word=3.351255 (steps=2244, words/sec=11167.37, time=0-00:09:51)
[switchout.syl.en-my] Epoch 7.4543: train_loss/word=3.324210 (steps=2265, words/sec=13125.82, time=0-00:09:53)
[switchout.syl.en-my] Epoch 7.5299: train_loss/word=3.313516 (steps=2285, words/sec=14408.23, time=0-00:09:55)
[switchout.syl.en-my] Epoch 7.6037: train_loss/word=3.368162 (steps=2306, words/sec=11820.56, time=0-00:09:57)
[switchout.syl.en-my] Epoch 7.6780: train_loss/word=3.305093 (steps=2330, words/sec=12286.78, time=0-00:09:59)
[switchout.syl.en-my] Epoch 7.7526: train_loss/word=3.324158 (steps=2357, words/sec=10744.54, time=0-00:10:02)
[switchout.syl.en-my] Epoch 7.8281: train_loss/word=3.304051 (steps=2379, words/sec=13713.20, time=0-00:10:04)
[switchout.syl.en-my] Epoch 7.9043: train_loss/word=3.263616 (steps=2404, words/sec=12147.09, time=0-00:10:07)
[switchout.syl.en-my] Epoch 7.9787: train_loss/word=3.292921 (steps=2428, words/sec=11616.82, time=0-00:10:10)
[switchout.syl.en-my] Epoch 8.0000: train_loss/word=3.233019 (steps=2433, words/sec=16005.53, time=0-00:10:10)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 8.0000 dev BLEU4: 0.25416741512615726, 0.540319/0.332199/0.202424/0.130769 (BP = 0.968090, ratio=0.97, hyp_len=12550, ref_len=12957) (time=0-00:10:47)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.272301
[switchout.syl.en-my]              dev auxiliary Loss: 3.131 (ref_len=12957)
             checkpoint took 0-00:00:37
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 8.0043: train_loss/word=3.135723 (steps=2434, words/sec=15890.32, time=0-00:10:53)
[switchout.syl.en-my] Epoch 8.0797: train_loss/word=3.162816 (steps=2459, words/sec=11413.76, time=0-00:10:56)
[switchout.syl.en-my] Epoch 8.1566: train_loss/word=3.191228 (steps=2482, words/sec=12154.96, time=0-00:10:58)
[switchout.syl.en-my] Epoch 8.2308: train_loss/word=3.186285 (steps=2506, words/sec=11762.55, time=0-00:11:01)
[switchout.syl.en-my] Epoch 8.3071: train_loss/word=3.271578 (steps=2528, words/sec=11524.24, time=0-00:11:03)
[switchout.syl.en-my] Epoch 8.3817: train_loss/word=3.194986 (steps=2550, words/sec=12340.38, time=0-00:11:05)
[switchout.syl.en-my] Epoch 8.4566: train_loss/word=3.176672 (steps=2570, words/sec=13835.16, time=0-00:11:07)
[switchout.syl.en-my] Epoch 8.5332: train_loss/word=3.202125 (steps=2593, words/sec=13096.90, time=0-00:11:09)
[switchout.syl.en-my] Epoch 8.6087: train_loss/word=3.159530 (steps=2616, words/sec=13321.45, time=0-00:11:11)
[switchout.syl.en-my] Epoch 8.6825: train_loss/word=3.241549 (steps=2637, words/sec=11054.74, time=0-00:11:14)
[switchout.syl.en-my] Epoch 8.7579: train_loss/word=3.227467 (steps=2659, words/sec=12507.58, time=0-00:11:16)
[switchout.syl.en-my] Epoch 8.8325: train_loss/word=3.212025 (steps=2685, words/sec=12229.18, time=0-00:11:18)
[switchout.syl.en-my] Epoch 8.9070: train_loss/word=3.202024 (steps=2707, words/sec=13189.06, time=0-00:11:20)
[switchout.syl.en-my] Epoch 8.9807: train_loss/word=3.189386 (steps=2732, words/sec=11901.29, time=0-00:11:23)
[switchout.syl.en-my] Epoch 9.0000: train_loss/word=3.210311 (steps=2737, words/sec=13447.29, time=0-00:11:24)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 9.0000 dev BLEU4: 0.26788966446756446, 0.573926/0.365600/0.230287/0.155274 (BP = 0.910225, ratio=0.91, hyp_len=11843, ref_len=12957) (time=0-00:11:59)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.288146
[switchout.syl.en-my]              dev auxiliary Loss: 3.074 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 9.0017: train_loss/word=3.036307 (steps=2738, words/sec=6231.42, time=0-00:12:04)
[switchout.syl.en-my] Epoch 9.0758: train_loss/word=3.116828 (steps=2760, words/sec=13052.26, time=0-00:12:07)
[switchout.syl.en-my] Epoch 9.1526: train_loss/word=3.023867 (steps=2782, words/sec=13668.34, time=0-00:12:09)
[switchout.syl.en-my] Epoch 9.2276: train_loss/word=3.085270 (steps=2803, words/sec=13322.53, time=0-00:12:10)
[switchout.syl.en-my] Epoch 9.3030: train_loss/word=3.064688 (steps=2824, words/sec=13083.64, time=0-00:12:12)
[switchout.syl.en-my] Epoch 9.3810: train_loss/word=3.141528 (steps=2848, words/sec=12186.87, time=0-00:12:15)
[switchout.syl.en-my] Epoch 9.4573: train_loss/word=3.119678 (steps=2873, words/sec=11683.55, time=0-00:12:17)
[switchout.syl.en-my] Epoch 9.5336: train_loss/word=3.111527 (steps=2894, words/sec=13184.72, time=0-00:12:19)
[switchout.syl.en-my] Epoch 9.6082: train_loss/word=3.114223 (steps=2915, words/sec=12370.37, time=0-00:12:21)
[switchout.syl.en-my] Epoch 9.6841: train_loss/word=3.159575 (steps=2938, words/sec=12589.84, time=0-00:12:24)
[switchout.syl.en-my] Epoch 9.7600: train_loss/word=3.132680 (steps=2966, words/sec=11003.74, time=0-00:12:27)
[switchout.syl.en-my] Epoch 9.8354: train_loss/word=3.124669 (steps=2992, words/sec=11763.68, time=0-00:12:30)
[switchout.syl.en-my] Epoch 9.9097: train_loss/word=3.072720 (steps=3015, words/sec=12181.61, time=0-00:12:32)
[switchout.syl.en-my] Epoch 9.9835: train_loss/word=3.107276 (steps=3037, words/sec=11296.11, time=0-00:12:34)
[switchout.syl.en-my] Epoch 10.0000: train_loss/word=3.324836 (steps=3042, words/sec=12623.07, time=0-00:12:35)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 10.0000 dev BLEU4: 0.28606156906868185, 0.579828/0.374006/0.240375/0.164937 (BP = 0.939428, ratio=0.94, hyp_len=12195, ref_len=12957) (time=0-00:13:12)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.303065
[switchout.syl.en-my]              dev auxiliary Loss: 3.008 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 10.0041: train_loss/word=2.941849 (steps=3043, words/sec=18956.35, time=0-00:13:18)
[switchout.syl.en-my] Epoch 10.0801: train_loss/word=2.951701 (steps=3067, words/sec=12823.39, time=0-00:13:20)
[switchout.syl.en-my] Epoch 10.1552: train_loss/word=2.975755 (steps=3089, words/sec=12914.06, time=0-00:13:22)
[switchout.syl.en-my] Epoch 10.2290: train_loss/word=3.032496 (steps=3111, words/sec=13109.08, time=0-00:13:24)
[switchout.syl.en-my] Epoch 10.3067: train_loss/word=3.046753 (steps=3133, words/sec=12704.37, time=0-00:13:26)
[switchout.syl.en-my] Epoch 10.3804: train_loss/word=3.013862 (steps=3156, words/sec=12039.01, time=0-00:13:29)
[switchout.syl.en-my] Epoch 10.4562: train_loss/word=3.002880 (steps=3179, words/sec=12580.23, time=0-00:13:31)
[switchout.syl.en-my] Epoch 10.5309: train_loss/word=3.001213 (steps=3206, words/sec=10534.65, time=0-00:13:34)
[switchout.syl.en-my] Epoch 10.6063: train_loss/word=3.000482 (steps=3230, words/sec=11630.52, time=0-00:13:37)
[switchout.syl.en-my] Epoch 10.6869: train_loss/word=3.008516 (steps=3253, words/sec=12165.45, time=0-00:13:39)
[switchout.syl.en-my] Epoch 10.7641: train_loss/word=3.064818 (steps=3272, words/sec=13147.77, time=0-00:13:41)
[switchout.syl.en-my] Epoch 10.8403: train_loss/word=3.057422 (steps=3297, words/sec=10696.66, time=0-00:13:44)
[switchout.syl.en-my] Epoch 10.9153: train_loss/word=3.089501 (steps=3322, words/sec=10465.40, time=0-00:13:47)
[switchout.syl.en-my] Epoch 10.9891: train_loss/word=3.020583 (steps=3341, words/sec=13008.23, time=0-00:13:48)
[switchout.syl.en-my] Epoch 11.0000: train_loss/word=3.149732 (steps=3345, words/sec=8274.50, time=0-00:13:49)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 11.0000 dev BLEU4: 0.2966634632338212, 0.601366/0.388107/0.251928/0.171579 (BP = 0.936066, ratio=0.94, hyp_len=12154, ref_len=12957) (time=0-00:14:25)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.315832
[switchout.syl.en-my]              dev auxiliary Loss: 2.966 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 11.0029: train_loss/word=2.584202 (steps=3346, words/sec=12694.05, time=0-00:14:31)
[switchout.syl.en-my] Epoch 11.0792: train_loss/word=2.942893 (steps=3370, words/sec=11301.72, time=0-00:14:33)
[switchout.syl.en-my] Epoch 11.1536: train_loss/word=2.922739 (steps=3393, words/sec=11345.68, time=0-00:14:36)
[switchout.syl.en-my] Epoch 11.2300: train_loss/word=2.861832 (steps=3419, words/sec=12291.41, time=0-00:14:39)
[switchout.syl.en-my] Epoch 11.3072: train_loss/word=2.936730 (steps=3442, words/sec=12609.38, time=0-00:14:41)
[switchout.syl.en-my] Epoch 11.3817: train_loss/word=2.964237 (steps=3464, words/sec=12030.54, time=0-00:14:43)
[switchout.syl.en-my] Epoch 11.4565: train_loss/word=2.930322 (steps=3487, words/sec=11838.10, time=0-00:14:45)
[switchout.syl.en-my] Epoch 11.5328: train_loss/word=2.924211 (steps=3507, words/sec=14060.61, time=0-00:14:47)
[switchout.syl.en-my] Epoch 11.6086: train_loss/word=2.968829 (steps=3528, words/sec=13068.03, time=0-00:14:49)
[switchout.syl.en-my] Epoch 11.6834: train_loss/word=2.972106 (steps=3551, words/sec=11127.04, time=0-00:14:51)
[switchout.syl.en-my] Epoch 11.7570: train_loss/word=2.949243 (steps=3574, words/sec=12300.87, time=0-00:14:54)
[switchout.syl.en-my] Epoch 11.8323: train_loss/word=2.957862 (steps=3599, words/sec=11557.83, time=0-00:14:56)
[switchout.syl.en-my] Epoch 11.9081: train_loss/word=2.933057 (steps=3622, words/sec=12407.00, time=0-00:14:59)
[switchout.syl.en-my] Epoch 11.9832: train_loss/word=2.941288 (steps=3645, words/sec=12428.49, time=0-00:15:01)
[switchout.syl.en-my] Epoch 12.0000: train_loss/word=2.914578 (steps=3650, words/sec=14175.61, time=0-00:15:02)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 12.0000 dev BLEU4: 0.3025887560030793, 0.599025/0.388734/0.254135/0.175104 (BP = 0.948393, ratio=0.95, hyp_len=12305, ref_len=12957) (time=0-00:15:38)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.319643
[switchout.syl.en-my]              dev auxiliary Loss: 2.925 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 12.0051: train_loss/word=2.796856 (steps=3651, words/sec=18060.64, time=0-00:15:44)
[switchout.syl.en-my] Epoch 12.0806: train_loss/word=2.803510 (steps=3674, words/sec=12287.82, time=0-00:15:46)
[switchout.syl.en-my] Epoch 12.1577: train_loss/word=2.811699 (steps=3697, words/sec=12553.36, time=0-00:15:48)
[switchout.syl.en-my] Epoch 12.2337: train_loss/word=2.823292 (steps=3719, words/sec=13790.83, time=0-00:15:50)
[switchout.syl.en-my] Epoch 12.3100: train_loss/word=2.839608 (steps=3742, words/sec=12368.92, time=0-00:15:53)
[switchout.syl.en-my] Epoch 12.3854: train_loss/word=2.914856 (steps=3766, words/sec=11412.66, time=0-00:15:55)
[switchout.syl.en-my] Epoch 12.4619: train_loss/word=2.877785 (steps=3789, words/sec=11823.46, time=0-00:15:58)
[switchout.syl.en-my] Epoch 12.5374: train_loss/word=2.959597 (steps=3810, words/sec=11865.69, time=0-00:16:00)
[switchout.syl.en-my] Epoch 12.6124: train_loss/word=2.826417 (steps=3834, words/sec=12664.17, time=0-00:16:02)
[switchout.syl.en-my] Epoch 12.6883: train_loss/word=2.828983 (steps=3860, words/sec=11433.59, time=0-00:16:05)
[switchout.syl.en-my] Epoch 12.7638: train_loss/word=2.925769 (steps=3883, words/sec=11469.28, time=0-00:16:07)
[switchout.syl.en-my] Epoch 12.8390: train_loss/word=2.908668 (steps=3905, words/sec=12842.84, time=0-00:16:10)
[switchout.syl.en-my] Epoch 12.9166: train_loss/word=2.898683 (steps=3928, words/sec=10549.44, time=0-00:16:12)
[switchout.syl.en-my] Epoch 12.9902: train_loss/word=2.914322 (steps=3951, words/sec=11143.67, time=0-00:16:15)
[switchout.syl.en-my] Epoch 13.0000: train_loss/word=2.756423 (steps=3954, words/sec=14174.01, time=0-00:16:15)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 13.0000 dev BLEU4: 0.3066390317166343, 0.622977/0.412916/0.274623/0.189318 (BP = 0.901699, ratio=0.91, hyp_len=11742, ref_len=12957) (time=0-00:16:51)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.326980
[switchout.syl.en-my]              dev auxiliary Loss: 2.909 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 13.0041: train_loss/word=2.746415 (steps=3955, words/sec=16629.39, time=0-00:16:57)
[switchout.syl.en-my] Epoch 13.0786: train_loss/word=2.739592 (steps=3976, words/sec=12240.51, time=0-00:16:59)
[switchout.syl.en-my] Epoch 13.1538: train_loss/word=2.770231 (steps=4000, words/sec=10560.57, time=0-00:17:02)
[switchout.syl.en-my] Epoch 13.2291: train_loss/word=2.804610 (steps=4022, words/sec=11410.96, time=0-00:17:04)
[switchout.syl.en-my] Epoch 13.3031: train_loss/word=2.842707 (steps=4046, words/sec=10791.14, time=0-00:17:07)
[switchout.syl.en-my] Epoch 13.3772: train_loss/word=2.817385 (steps=4072, words/sec=10156.02, time=0-00:17:10)
[switchout.syl.en-my] Epoch 13.4519: train_loss/word=2.780339 (steps=4093, words/sec=12464.19, time=0-00:17:12)
[switchout.syl.en-my] Epoch 13.5288: train_loss/word=2.792535 (steps=4115, words/sec=13277.80, time=0-00:17:14)
[switchout.syl.en-my] Epoch 13.6047: train_loss/word=2.785273 (steps=4138, words/sec=12364.52, time=0-00:17:17)
[switchout.syl.en-my] Epoch 13.6786: train_loss/word=2.775477 (steps=4160, words/sec=12773.13, time=0-00:17:19)
[switchout.syl.en-my] Epoch 13.7549: train_loss/word=2.759111 (steps=4186, words/sec=11147.61, time=0-00:17:22)
[switchout.syl.en-my] Epoch 13.8299: train_loss/word=2.817814 (steps=4207, words/sec=12908.73, time=0-00:17:24)
[switchout.syl.en-my] Epoch 13.9058: train_loss/word=2.868485 (steps=4230, words/sec=10757.31, time=0-00:17:26)
[switchout.syl.en-my] Epoch 13.9807: train_loss/word=2.840657 (steps=4252, words/sec=11930.75, time=0-00:17:29)
[switchout.syl.en-my] Epoch 14.0000: train_loss/word=2.788984 (steps=4258, words/sec=10499.80, time=0-00:17:29)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 14.0000 dev BLEU4: 0.3137217777321539, 0.635899/0.420847/0.279877/0.195491 (BP = 0.901868, ratio=0.91, hyp_len=11744, ref_len=12957) (time=0-00:18:05)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.334591
[switchout.syl.en-my]              dev auxiliary Loss: 2.879 (ref_len=12957)
             checkpoint took 0-00:00:35
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 14.0030: train_loss/word=2.625614 (steps=4259, words/sec=12538.59, time=0-00:18:11)
[switchout.syl.en-my] Epoch 14.0809: train_loss/word=2.732433 (steps=4284, words/sec=10994.17, time=0-00:18:14)
[switchout.syl.en-my] Epoch 14.1571: train_loss/word=2.749523 (steps=4305, words/sec=13322.68, time=0-00:18:16)
[switchout.syl.en-my] Epoch 14.2312: train_loss/word=2.698965 (steps=4328, words/sec=11547.87, time=0-00:18:18)
[switchout.syl.en-my] Epoch 14.3075: train_loss/word=2.706656 (steps=4352, words/sec=11789.42, time=0-00:18:21)
[switchout.syl.en-my] Epoch 14.3837: train_loss/word=2.704177 (steps=4373, words/sec=13579.52, time=0-00:18:23)
[switchout.syl.en-my] Epoch 14.4603: train_loss/word=2.728907 (steps=4397, words/sec=11092.83, time=0-00:18:26)
[switchout.syl.en-my] Epoch 14.5347: train_loss/word=2.765583 (steps=4420, words/sec=10188.01, time=0-00:18:28)
[switchout.syl.en-my] Epoch 14.6120: train_loss/word=2.712520 (steps=4444, words/sec=13080.74, time=0-00:18:31)
[switchout.syl.en-my] Epoch 14.6877: train_loss/word=2.734486 (steps=4465, words/sec=13377.40, time=0-00:18:33)
[switchout.syl.en-my] Epoch 14.7643: train_loss/word=2.779529 (steps=4489, words/sec=10920.79, time=0-00:18:35)
[switchout.syl.en-my] Epoch 14.8401: train_loss/word=2.791570 (steps=4515, words/sec=9800.48, time=0-00:18:38)
[switchout.syl.en-my] Epoch 14.9139: train_loss/word=2.761268 (steps=4536, words/sec=13269.61, time=0-00:18:40)
[switchout.syl.en-my] Epoch 14.9888: train_loss/word=2.813780 (steps=4559, words/sec=11602.96, time=0-00:18:43)
[switchout.syl.en-my] Epoch 15.0000: train_loss/word=2.898258 (steps=4562, words/sec=11010.23, time=0-00:18:43)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 15.0000 dev BLEU4: 0.3215352211957523, 0.619032/0.408188/0.273993/0.192872 (BP = 0.945874, ratio=0.95, hyp_len=12274, ref_len=12957) (time=0-00:19:19)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.335889
[switchout.syl.en-my]              dev auxiliary Loss: 2.868 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 15.0068: train_loss/word=3.139070 (steps=4563, words/sec=18042.39, time=0-00:19:25)
[switchout.syl.en-my] Epoch 15.0823: train_loss/word=2.688020 (steps=4584, words/sec=12049.80, time=0-00:19:27)
[switchout.syl.en-my] Epoch 15.1574: train_loss/word=2.641353 (steps=4611, words/sec=11348.24, time=0-00:19:30)
[switchout.syl.en-my] Epoch 15.2315: train_loss/word=2.621345 (steps=4632, words/sec=13852.42, time=0-00:19:32)
[switchout.syl.en-my] Epoch 15.3073: train_loss/word=2.619518 (steps=4655, words/sec=11747.84, time=0-00:19:35)
[switchout.syl.en-my] Epoch 15.3822: train_loss/word=2.666230 (steps=4679, words/sec=11650.16, time=0-00:19:37)
[switchout.syl.en-my] Epoch 15.4573: train_loss/word=2.663718 (steps=4702, words/sec=12795.67, time=0-00:19:39)
[switchout.syl.en-my] Epoch 15.5325: train_loss/word=2.654926 (steps=4725, words/sec=12304.26, time=0-00:19:42)
[switchout.syl.en-my] Epoch 15.6071: train_loss/word=2.709091 (steps=4748, words/sec=11924.10, time=0-00:19:44)
[switchout.syl.en-my] Epoch 15.6812: train_loss/word=2.669131 (steps=4769, words/sec=12707.44, time=0-00:19:46)
[switchout.syl.en-my] Epoch 15.7553: train_loss/word=2.721795 (steps=4794, words/sec=10050.39, time=0-00:19:49)
[switchout.syl.en-my] Epoch 15.8331: train_loss/word=2.692315 (steps=4817, words/sec=12648.93, time=0-00:19:51)
[switchout.syl.en-my] Epoch 15.9069: train_loss/word=2.681273 (steps=4837, words/sec=13459.80, time=0-00:19:53)
[switchout.syl.en-my] Epoch 15.9812: train_loss/word=2.735171 (steps=4863, words/sec=11283.00, time=0-00:19:56)
[switchout.syl.en-my] Epoch 16.0000: train_loss/word=2.807665 (steps=4867, words/sec=16027.38, time=0-00:19:56)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 16.0000 dev BLEU4: 0.31744241884745006, 0.649175/0.433397/0.292452/0.208681 (BP = 0.876938, ratio=0.88, hyp_len=11453, ref_len=12957) (time=0-00:20:31)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.338415
[switchout.syl.en-my]              dev auxiliary Loss: 2.849 (ref_len=12957)
             checkpoint took 0-00:00:34
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 16.0020: train_loss/word=2.573586 (steps=4868, words/sec=8821.64, time=0-00:20:34)
[switchout.syl.en-my] Epoch 16.0774: train_loss/word=2.572252 (steps=4890, words/sec=12358.43, time=0-00:20:36)
[switchout.syl.en-my] Epoch 16.1546: train_loss/word=2.581794 (steps=4915, words/sec=11810.98, time=0-00:20:39)
[switchout.syl.en-my] Epoch 16.2285: train_loss/word=2.626447 (steps=4940, words/sec=10435.41, time=0-00:20:42)
[switchout.syl.en-my] Epoch 16.3065: train_loss/word=2.572169 (steps=4966, words/sec=11509.00, time=0-00:20:45)
[switchout.syl.en-my] Epoch 16.3824: train_loss/word=2.631681 (steps=4988, words/sec=12937.70, time=0-00:20:47)
[switchout.syl.en-my] Epoch 16.4574: train_loss/word=2.653018 (steps=5009, words/sec=11570.39, time=0-00:20:49)
[switchout.syl.en-my] Epoch 16.5341: train_loss/word=2.635053 (steps=5030, words/sec=12776.65, time=0-00:20:51)
[switchout.syl.en-my] Epoch 16.6101: train_loss/word=2.616902 (steps=5055, words/sec=10983.37, time=0-00:20:54)
[switchout.syl.en-my] Epoch 16.6859: train_loss/word=2.666148 (steps=5075, words/sec=12354.99, time=0-00:20:56)
[switchout.syl.en-my] Epoch 16.7609: train_loss/word=2.649062 (steps=5095, words/sec=12813.45, time=0-00:20:58)
[switchout.syl.en-my] Epoch 16.8354: train_loss/word=2.621560 (steps=5117, words/sec=11784.66, time=0-00:21:00)
[switchout.syl.en-my] Epoch 16.9096: train_loss/word=2.662917 (steps=5142, words/sec=10929.10, time=0-00:21:03)
[switchout.syl.en-my] Epoch 16.9849: train_loss/word=2.663625 (steps=5167, words/sec=10910.70, time=0-00:21:06)
[switchout.syl.en-my] Epoch 17.0000: train_loss/word=2.849862 (steps=5171, words/sec=10138.89, time=0-00:21:06)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 17.0000 dev BLEU4: 0.33091688640128586, 0.638762/0.426847/0.289462/0.207759 (BP = 0.924759, ratio=0.93, hyp_len=12017, ref_len=12957) (time=0-00:21:43)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.347048
[switchout.syl.en-my]              dev auxiliary Loss: 2.845 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 17.0045: train_loss/word=2.578897 (steps=5172, words/sec=17860.98, time=0-00:21:49)
[switchout.syl.en-my] Epoch 17.0789: train_loss/word=2.585819 (steps=5195, words/sec=11125.17, time=0-00:21:51)
[switchout.syl.en-my] Epoch 17.1554: train_loss/word=2.563848 (steps=5219, words/sec=11154.94, time=0-00:21:54)
[switchout.syl.en-my] Epoch 17.2301: train_loss/word=2.564241 (steps=5242, words/sec=12394.52, time=0-00:21:56)
[switchout.syl.en-my] Epoch 17.3061: train_loss/word=2.593581 (steps=5269, words/sec=10542.22, time=0-00:21:59)
[switchout.syl.en-my] Epoch 17.3863: train_loss/word=2.533176 (steps=5292, words/sec=12631.04, time=0-00:22:01)
[switchout.syl.en-my] Epoch 17.4629: train_loss/word=2.594742 (steps=5317, words/sec=11285.83, time=0-00:22:04)
[switchout.syl.en-my] Epoch 17.5396: train_loss/word=2.606944 (steps=5343, words/sec=10511.69, time=0-00:22:07)
[switchout.syl.en-my] Epoch 17.6137: train_loss/word=2.627100 (steps=5364, words/sec=12552.20, time=0-00:22:09)
[switchout.syl.en-my] Epoch 17.6883: train_loss/word=2.593168 (steps=5386, words/sec=12152.69, time=0-00:22:11)
[switchout.syl.en-my] Epoch 17.7635: train_loss/word=2.605469 (steps=5407, words/sec=12738.04, time=0-00:22:13)
[switchout.syl.en-my] Epoch 17.8443: train_loss/word=2.725303 (steps=5427, words/sec=11820.42, time=0-00:22:15)
[switchout.syl.en-my] Epoch 17.9200: train_loss/word=2.651632 (steps=5449, words/sec=11629.12, time=0-00:22:18)
[switchout.syl.en-my] Epoch 17.9960: train_loss/word=2.548717 (steps=5474, words/sec=11945.86, time=0-00:22:20)
[switchout.syl.en-my] Epoch 18.0000: train_loss/word=2.553685 (steps=5476, words/sec=8951.18, time=0-00:22:21)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 18.0000 dev BLEU4: 0.3334840347957794, 0.640720/0.426882/0.287749/0.203825 (BP = 0.937051, ratio=0.94, hyp_len=12166, ref_len=12957) (time=0-00:22:57)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.348198
[switchout.syl.en-my]              dev auxiliary Loss: 2.827 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 18.0054: train_loss/word=2.709752 (steps=5477, words/sec=18117.91, time=0-00:23:03)
[switchout.syl.en-my] Epoch 18.0806: train_loss/word=2.502607 (steps=5500, words/sec=12108.16, time=0-00:23:05)
[switchout.syl.en-my] Epoch 18.1556: train_loss/word=2.513929 (steps=5521, words/sec=13031.73, time=0-00:23:07)
[switchout.syl.en-my] Epoch 18.2312: train_loss/word=2.554594 (steps=5543, words/sec=12286.99, time=0-00:23:09)
[switchout.syl.en-my] Epoch 18.3051: train_loss/word=2.505944 (steps=5567, words/sec=12192.92, time=0-00:23:12)
[switchout.syl.en-my] Epoch 18.3787: train_loss/word=2.521737 (steps=5589, words/sec=11967.16, time=0-00:23:14)
[switchout.syl.en-my] Epoch 18.4548: train_loss/word=2.568503 (steps=5612, words/sec=12700.49, time=0-00:23:17)
[switchout.syl.en-my] Epoch 18.5296: train_loss/word=2.517907 (steps=5638, words/sec=10784.27, time=0-00:23:19)
[switchout.syl.en-my] Epoch 18.6038: train_loss/word=2.570264 (steps=5661, words/sec=11358.89, time=0-00:23:22)
[switchout.syl.en-my] Epoch 18.6797: train_loss/word=2.555675 (steps=5683, words/sec=13074.57, time=0-00:23:24)
[switchout.syl.en-my] Epoch 18.7548: train_loss/word=2.567846 (steps=5706, words/sec=11696.79, time=0-00:23:26)
[switchout.syl.en-my] Epoch 18.8284: train_loss/word=2.582796 (steps=5728, words/sec=12092.21, time=0-00:23:29)
[switchout.syl.en-my] Epoch 18.9063: train_loss/word=2.546757 (steps=5753, words/sec=12011.51, time=0-00:23:31)
[switchout.syl.en-my] Epoch 18.9812: train_loss/word=2.555680 (steps=5775, words/sec=12690.39, time=0-00:23:33)
[switchout.syl.en-my] Epoch 19.0000: train_loss/word=2.604120 (steps=5780, words/sec=11906.48, time=0-00:23:34)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 19.0000 dev BLEU4: 0.3402104991972831, 0.646487/0.434842/0.296203/0.210507 (BP = 0.934999, ratio=0.94, hyp_len=12141, ref_len=12957) (time=0-00:24:10)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.355073
[switchout.syl.en-my]              dev auxiliary Loss: 2.820 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 19.0051: train_loss/word=2.629315 (steps=5781, words/sec=16673.48, time=0-00:24:16)
[switchout.syl.en-my] Epoch 19.0803: train_loss/word=2.433604 (steps=5803, words/sec=12197.64, time=0-00:24:19)
[switchout.syl.en-my] Epoch 19.1540: train_loss/word=2.471297 (steps=5829, words/sec=10399.31, time=0-00:24:22)
[switchout.syl.en-my] Epoch 19.2290: train_loss/word=2.508409 (steps=5849, words/sec=12888.11, time=0-00:24:24)
[switchout.syl.en-my] Epoch 19.3043: train_loss/word=2.468048 (steps=5874, words/sec=10791.50, time=0-00:24:26)
[switchout.syl.en-my] Epoch 19.3785: train_loss/word=2.558563 (steps=5897, words/sec=11258.96, time=0-00:24:29)
[switchout.syl.en-my] Epoch 19.4523: train_loss/word=2.473827 (steps=5919, words/sec=12321.91, time=0-00:24:31)
[switchout.syl.en-my] Epoch 19.5282: train_loss/word=2.493770 (steps=5940, words/sec=12572.03, time=0-00:24:33)
[switchout.syl.en-my] Epoch 19.6027: train_loss/word=2.482682 (steps=5963, words/sec=11046.75, time=0-00:24:36)
[switchout.syl.en-my] Epoch 19.6770: train_loss/word=2.530841 (steps=5983, words/sec=12521.88, time=0-00:24:38)
[switchout.syl.en-my] Epoch 19.7507: train_loss/word=2.520583 (steps=6007, words/sec=10717.88, time=0-00:24:40)
[switchout.syl.en-my] Epoch 19.8243: train_loss/word=2.507346 (steps=6031, words/sec=11258.07, time=0-00:24:43)
[switchout.syl.en-my] Epoch 19.8994: train_loss/word=2.534047 (steps=6055, words/sec=10919.25, time=0-00:24:46)
[switchout.syl.en-my] Epoch 19.9737: train_loss/word=2.495104 (steps=6078, words/sec=12361.04, time=0-00:24:48)
[switchout.syl.en-my] Epoch 20.0000: train_loss/word=2.619957 (steps=6085, words/sec=11469.71, time=0-00:24:49)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 20.0000 dev BLEU4: 0.33972076896647957, 0.628777/0.421649/0.286794/0.202089 (BP = 0.964899, ratio=0.97, hyp_len=12510, ref_len=12957) (time=0-00:25:26)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.350528
[switchout.syl.en-my]              dev auxiliary Loss: 2.824 (ref_len=12957)
             checkpoint took 0-00:00:37
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 20.0060: train_loss/word=2.911707 (steps=6086, words/sec=15749.22, time=0-00:25:29)
[switchout.syl.en-my] Epoch 20.0805: train_loss/word=2.443875 (steps=6108, words/sec=11497.59, time=0-00:25:31)
[switchout.syl.en-my] Epoch 20.1543: train_loss/word=2.418591 (steps=6132, words/sec=12197.17, time=0-00:25:34)
[switchout.syl.en-my] Epoch 20.2284: train_loss/word=2.450036 (steps=6154, words/sec=12220.16, time=0-00:25:36)
[switchout.syl.en-my] Epoch 20.3069: train_loss/word=2.411863 (steps=6180, words/sec=12034.02, time=0-00:25:39)
[switchout.syl.en-my] Epoch 20.3815: train_loss/word=2.436050 (steps=6203, words/sec=11154.68, time=0-00:25:41)
[switchout.syl.en-my] Epoch 20.4553: train_loss/word=2.393005 (steps=6228, words/sec=12380.51, time=0-00:25:44)
[switchout.syl.en-my] Epoch 20.5291: train_loss/word=2.460930 (steps=6251, words/sec=11647.55, time=0-00:25:46)
[switchout.syl.en-my] Epoch 20.6036: train_loss/word=2.440804 (steps=6275, words/sec=11944.19, time=0-00:25:48)
[switchout.syl.en-my] Epoch 20.6779: train_loss/word=2.446787 (steps=6301, words/sec=10218.34, time=0-00:25:52)
[switchout.syl.en-my] Epoch 20.7521: train_loss/word=2.454282 (steps=6324, words/sec=10625.32, time=0-00:25:54)
[switchout.syl.en-my] Epoch 20.8266: train_loss/word=2.483569 (steps=6344, words/sec=12867.23, time=0-00:25:56)
[switchout.syl.en-my] Epoch 20.9033: train_loss/word=2.521982 (steps=6364, words/sec=13159.35, time=0-00:25:58)
[switchout.syl.en-my] Epoch 20.9784: train_loss/word=2.588039 (steps=6384, words/sec=11263.56, time=0-00:26:00)
[switchout.syl.en-my] Epoch 21.0000: train_loss/word=2.447473 (steps=6390, words/sec=12432.02, time=0-00:26:01)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 21.0000 dev BLEU4: 0.32923675824545096, 0.640224/0.430058/0.290821/0.206457 (BP = 0.918184, ratio=0.92, hyp_len=11938, ref_len=12957) (time=0-00:26:37)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.345015
[switchout.syl.en-my]              dev auxiliary Loss: 2.832 (ref_len=12957)
             checkpoint took 0-00:00:36
  new learning rate: 0.5
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 21.0040: train_loss/word=2.434452 (steps=6391, words/sec=15824.33, time=0-00:26:40)
[switchout.syl.en-my] Epoch 21.0781: train_loss/word=2.321693 (steps=6416, words/sec=11140.96, time=0-00:26:43)
[switchout.syl.en-my] Epoch 21.1535: train_loss/word=2.359561 (steps=6438, words/sec=12115.50, time=0-00:26:45)
[switchout.syl.en-my] Epoch 21.2287: train_loss/word=2.404416 (steps=6461, words/sec=10849.20, time=0-00:26:48)
[switchout.syl.en-my] Epoch 21.3027: train_loss/word=2.370089 (steps=6483, words/sec=12459.20, time=0-00:26:50)
[switchout.syl.en-my] Epoch 21.3810: train_loss/word=2.344229 (steps=6506, words/sec=12380.42, time=0-00:26:52)
[switchout.syl.en-my] Epoch 21.4582: train_loss/word=2.352775 (steps=6530, words/sec=11713.85, time=0-00:26:55)
[switchout.syl.en-my] Epoch 21.5331: train_loss/word=2.377149 (steps=6554, words/sec=11010.11, time=0-00:26:58)
[switchout.syl.en-my] Epoch 21.6109: train_loss/word=2.348338 (steps=6579, words/sec=10468.33, time=0-00:27:00)
[switchout.syl.en-my] Epoch 21.6872: train_loss/word=2.360156 (steps=6603, words/sec=11182.24, time=0-00:27:03)
[switchout.syl.en-my] Epoch 21.7624: train_loss/word=2.396600 (steps=6623, words/sec=12514.90, time=0-00:27:05)
[switchout.syl.en-my] Epoch 21.8367: train_loss/word=2.378489 (steps=6647, words/sec=11181.49, time=0-00:27:07)
[switchout.syl.en-my] Epoch 21.9105: train_loss/word=2.342061 (steps=6668, words/sec=11265.42, time=0-00:27:10)
[switchout.syl.en-my] Epoch 21.9865: train_loss/word=2.359341 (steps=6692, words/sec=10391.19, time=0-00:27:13)
[switchout.syl.en-my] Epoch 22.0000: train_loss/word=2.400187 (steps=6696, words/sec=15152.24, time=0-00:27:13)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 22.0000 dev BLEU4: 0.34330066961550065, 0.653840/0.441126/0.300433/0.214002 (BP = 0.930304, ratio=0.93, hyp_len=12084, ref_len=12957) (time=0-00:27:50)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.358608
[switchout.syl.en-my]              dev auxiliary Loss: 2.796 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 22.0022: train_loss/word=2.109972 (steps=6697, words/sec=11101.44, time=0-00:27:55)
[switchout.syl.en-my] Epoch 22.0767: train_loss/word=2.251506 (steps=6719, words/sec=13149.72, time=0-00:27:58)
[switchout.syl.en-my] Epoch 22.1510: train_loss/word=2.352173 (steps=6743, words/sec=10414.58, time=0-00:28:00)
[switchout.syl.en-my] Epoch 22.2272: train_loss/word=2.363449 (steps=6765, words/sec=12766.44, time=0-00:28:02)
[switchout.syl.en-my] Epoch 22.3016: train_loss/word=2.349527 (steps=6786, words/sec=13344.58, time=0-00:28:04)
[switchout.syl.en-my] Epoch 22.3756: train_loss/word=2.329304 (steps=6808, words/sec=13172.83, time=0-00:28:06)
[switchout.syl.en-my] Epoch 22.4505: train_loss/word=2.311266 (steps=6831, words/sec=12602.40, time=0-00:28:09)
[switchout.syl.en-my] Epoch 22.5250: train_loss/word=2.296502 (steps=6854, words/sec=12096.17, time=0-00:28:11)
[switchout.syl.en-my] Epoch 22.6032: train_loss/word=2.326974 (steps=6880, words/sec=10738.32, time=0-00:28:14)
[switchout.syl.en-my] Epoch 22.6775: train_loss/word=2.287834 (steps=6902, words/sec=13173.16, time=0-00:28:16)
[switchout.syl.en-my] Epoch 22.7556: train_loss/word=2.412160 (steps=6924, words/sec=11918.40, time=0-00:28:18)
[switchout.syl.en-my] Epoch 22.8325: train_loss/word=2.323583 (steps=6947, words/sec=13283.11, time=0-00:28:20)
[switchout.syl.en-my] Epoch 22.9083: train_loss/word=2.345373 (steps=6970, words/sec=11343.48, time=0-00:28:23)
[switchout.syl.en-my] Epoch 22.9820: train_loss/word=2.314531 (steps=6995, words/sec=10576.44, time=0-00:28:26)
[switchout.syl.en-my] Epoch 23.0000: train_loss/word=2.229891 (steps=7001, words/sec=11830.98, time=0-00:28:26)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 23.0000 dev BLEU4: 0.34603028796453894, 0.660879/0.449308/0.308277/0.221647 (BP = 0.916847, ratio=0.92, hyp_len=11922, ref_len=12957) (time=0-00:29:01)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.363382
[switchout.syl.en-my]              dev auxiliary Loss: 2.794 (ref_len=12957)
             checkpoint took 0-00:00:34
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 23.0026: train_loss/word=2.188988 (steps=7002, words/sec=11746.31, time=0-00:29:07)
[switchout.syl.en-my] Epoch 23.0773: train_loss/word=2.291919 (steps=7025, words/sec=11769.84, time=0-00:29:09)
[switchout.syl.en-my] Epoch 23.1535: train_loss/word=2.314569 (steps=7048, words/sec=12649.53, time=0-00:29:12)
[switchout.syl.en-my] Epoch 23.2301: train_loss/word=2.270732 (steps=7072, words/sec=12761.30, time=0-00:29:14)
[switchout.syl.en-my] Epoch 23.3055: train_loss/word=2.278996 (steps=7095, words/sec=12105.34, time=0-00:29:16)
[switchout.syl.en-my] Epoch 23.3802: train_loss/word=2.305767 (steps=7117, words/sec=13419.08, time=0-00:29:18)
[switchout.syl.en-my] Epoch 23.4542: train_loss/word=2.316689 (steps=7142, words/sec=10715.09, time=0-00:29:21)
[switchout.syl.en-my] Epoch 23.5280: train_loss/word=2.261186 (steps=7165, words/sec=11827.36, time=0-00:29:24)
[switchout.syl.en-my] Epoch 23.6039: train_loss/word=2.346565 (steps=7186, words/sec=12520.97, time=0-00:29:26)
[switchout.syl.en-my] Epoch 23.6806: train_loss/word=2.364426 (steps=7209, words/sec=12190.54, time=0-00:29:28)
[switchout.syl.en-my] Epoch 23.7560: train_loss/word=2.317366 (steps=7233, words/sec=12181.45, time=0-00:29:30)
[switchout.syl.en-my] Epoch 23.8307: train_loss/word=2.338908 (steps=7254, words/sec=12427.05, time=0-00:29:33)
[switchout.syl.en-my] Epoch 23.9053: train_loss/word=2.348674 (steps=7275, words/sec=11740.34, time=0-00:29:35)
[switchout.syl.en-my] Epoch 23.9795: train_loss/word=2.296137 (steps=7301, words/sec=11028.32, time=0-00:29:38)
[switchout.syl.en-my] Epoch 24.0000: train_loss/word=2.374144 (steps=7306, words/sec=13684.13, time=0-00:29:38)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 24.0000 dev BLEU4: 0.3526960460799318, 0.643521/0.435425/0.299321/0.214546 (BP = 0.962980, ratio=0.96, hyp_len=12486, ref_len=12957) (time=0-00:30:14)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.364142
[switchout.syl.en-my]              dev auxiliary Loss: 2.788 (ref_len=12957)
             checkpoint took 0-00:00:36
  best dev score, writing out model
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 24.0058: train_loss/word=2.302764 (steps=7307, words/sec=23515.18, time=0-00:30:20)
[switchout.syl.en-my] Epoch 24.0804: train_loss/word=2.257426 (steps=7332, words/sec=10558.01, time=0-00:30:23)
[switchout.syl.en-my] Epoch 24.1575: train_loss/word=2.308403 (steps=7354, words/sec=12451.84, time=0-00:30:25)
[switchout.syl.en-my] Epoch 24.2355: train_loss/word=2.261515 (steps=7377, words/sec=13368.81, time=0-00:30:27)
[switchout.syl.en-my] Epoch 24.3102: train_loss/word=2.283562 (steps=7400, words/sec=11933.42, time=0-00:30:30)
[switchout.syl.en-my] Epoch 24.3876: train_loss/word=2.254461 (steps=7424, words/sec=11713.92, time=0-00:30:32)
[switchout.syl.en-my] Epoch 24.4627: train_loss/word=2.269803 (steps=7449, words/sec=11379.32, time=0-00:30:35)
[switchout.syl.en-my] Epoch 24.5390: train_loss/word=2.281682 (steps=7474, words/sec=11029.75, time=0-00:30:38)
[switchout.syl.en-my] Epoch 24.6147: train_loss/word=2.328641 (steps=7496, words/sec=13315.80, time=0-00:30:40)
[switchout.syl.en-my] Epoch 24.6888: train_loss/word=2.281391 (steps=7517, words/sec=12796.04, time=0-00:30:42)
[switchout.syl.en-my] Epoch 24.7658: train_loss/word=2.263281 (steps=7540, words/sec=13504.88, time=0-00:30:44)
[switchout.syl.en-my] Epoch 24.8408: train_loss/word=2.368676 (steps=7560, words/sec=12656.29, time=0-00:30:46)
[switchout.syl.en-my] Epoch 24.9181: train_loss/word=2.311552 (steps=7586, words/sec=10886.79, time=0-00:30:49)
[switchout.syl.en-my] Epoch 24.9934: train_loss/word=2.308299 (steps=7608, words/sec=12274.48, time=0-00:30:51)
[switchout.syl.en-my] Epoch 25.0000: train_loss/word=2.158812 (steps=7610, words/sec=13757.08, time=0-00:30:51)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 25.0000 dev BLEU4: 0.34483528447708667, 0.661132/0.447177/0.306453/0.220624 (BP = 0.917098, ratio=0.92, hyp_len=11925, ref_len=12957) (time=0-00:31:27)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.362891
[switchout.syl.en-my]              dev auxiliary Loss: 2.794 (ref_len=12957)
             checkpoint took 0-00:00:35
  new learning rate: 0.25
Starting to read ./data/train.en and ./data/train.my
Done reading ./data/train.en and ./data/train.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 25.0028: train_loss/word=2.154679 (steps=7611, words/sec=12484.83, time=0-00:31:30)
[switchout.syl.en-my] Epoch 25.0776: train_loss/word=2.209253 (steps=7636, words/sec=11188.68, time=0-00:31:32)
[switchout.syl.en-my] Epoch 25.1531: train_loss/word=2.239698 (steps=7661, words/sec=11162.53, time=0-00:31:35)
[switchout.syl.en-my] Epoch 25.2272: train_loss/word=2.279582 (steps=7684, words/sec=10725.01, time=0-00:31:37)
[switchout.syl.en-my] Epoch 25.3021: train_loss/word=2.259647 (steps=7706, words/sec=12652.02, time=0-00:31:40)
[switchout.syl.en-my] Epoch 25.3782: train_loss/word=2.211313 (steps=7731, words/sec=11659.57, time=0-00:31:42)
[switchout.syl.en-my] Epoch 25.4539: train_loss/word=2.240002 (steps=7755, words/sec=11536.75, time=0-00:31:45)
[switchout.syl.en-my] Epoch 25.5298: train_loss/word=2.232909 (steps=7779, words/sec=11473.95, time=0-00:31:48)
[switchout.syl.en-my] Epoch 25.6070: train_loss/word=2.308788 (steps=7798, words/sec=14349.86, time=0-00:31:49)
[switchout.syl.en-my] Epoch 25.6827: train_loss/word=2.224701 (steps=7821, words/sec=12185.20, time=0-00:31:52)
[switchout.syl.en-my] Epoch 25.7568: train_loss/word=2.330484 (steps=7842, words/sec=12382.38, time=0-00:31:54)
[switchout.syl.en-my] Epoch 25.8312: train_loss/word=2.292653 (steps=7862, words/sec=14403.27, time=0-00:31:55)
[switchout.syl.en-my] Epoch 25.9099: train_loss/word=2.202923 (steps=7887, words/sec=12797.00, time=0-00:31:58)
[switchout.syl.en-my] Epoch 25.9837: train_loss/word=2.234274 (steps=7908, words/sec=13192.30, time=0-00:32:00)
[switchout.syl.en-my] Epoch 26.0000: train_loss/word=2.194806 (steps=7914, words/sec=11842.82, time=0-00:32:00)
> Checkpoint [switchout.syl.en-my]
Performing inference on ./data/dev.en and ./data/dev.my
Starting to read ./data/dev.en and ./data/dev.my
Done reading ./data/dev.en and ./data/dev.my. Packing into batches.
Done packing batches.
[switchout.syl.en-my] Epoch 26.0000 dev BLEU4: 0.34857190627985746, 0.660722/0.446906/0.306558/0.219991 (BP = 0.927907, ratio=0.93, hyp_len=12055, ref_len=12957) (time=0-00:32:35)
[switchout.syl.en-my]              dev auxiliary GLEU: 0.365939
[switchout.syl.en-my]              dev auxiliary Loss: 2.782 (ref_len=12957)
             checkpoint took 0-00:00:34
  Early stopping
reverting learned weights to best checkpoint..
> Performing final evaluation
Performing inference on ./data/dev.en and ./data/dev.my
Performing inference on ./data/test.en and ./data/test.my
Experiment                    | Final Scores
-----------------------------------------------------------------------
switchout.syl.en-my           | BLEU4: 0.3526960460799318, 0.643521/0.435425/0.299321/0.214546 (BP = 0.962980, ratio=0.96, hyp_len=12486, ref_len=12957)
                              | GLEU: 0.364142
                              | WER: 59.02% ( C/S/I/D: 6901/3994/1591/2062; hyp_len=12486, ref_len=12957 )
                              | CER: 53.54% ( C/S/I/D: 22050/8744/4793/6346; hyp_len=35587, ref_len=37140 )
                              | BLEU4: 0.3622726495083123, 0.651440/0.445344/0.310464/0.227225 (BP = 0.957803, ratio=0.96, hyp_len=12850, ref_len=13404)
                              | GLEU: 0.372263
                              | WER: 58.36% ( C/S/I/D: 7182/4068/1600/2154; hyp_len=12850, ref_len=13404 )
                              | CER: 52.92% ( C/S/I/D: 22783/8797/4760/6700; hyp_len=36340, ref_len=38280 )
```

ပထမပိုင်း training လုပ်ခဲ့တဲ့ (no data argumentation or no switchout, syllable unit, en-my) ရဲ့ ရလဒ်က အောက်ပါအတိုင်းပါ။  

```
Experiment                    | Final Scores
-----------------------------------------------------------------------
medical.syl.en-my             | BLEU4: 0.36375391673239676, 0.647598/0.440523/0.304478/0.221674 (BP = 0.976497, ratio=0.98, hyp_len=12656, ref_len=12957)
                              | GLEU: 0.372705
                              | WER: 58.85% ( C/S/I/D: 7057/3874/1725/2026; hyp_len=12656, ref_len=12957 )
                              | CER: 53.36% ( C/S/I/D: 22375/8440/5053/6325; hyp_len=35868, ref_len=37140 )
                              | BLEU4: 0.3669128759686029, 0.652303/0.443451/0.307870/0.220885 (BP = 0.979729, ratio=0.98, hyp_len=13135, ref_len=13404)
                              | GLEU: 0.376249
                              | WER: 58.39% ( C/S/I/D: 7325/4063/1747/2016; hyp_len=13135, ref_len=13404 )
                              | CER: 53.03% ( C/S/I/D: 23025/9022/5043/6233; hyp_len=37090, ref_len=38280 )
```

ရလဒ် နှစ်ခုကို နှိုင်းယှဉ်ကြည့်တဲ့အခါမှာ switchout က syllable မှာ လည်းအလုပ်လုပ်ပါတယ်။ သို့သော် detail analysis အနေနဲ့ လုပ်ကြည့်ရင်တော့...    
**BLEU score နဲ့ GLEU score နှစ်မျိုးတည်းကို ကြည့်ရင်တော့ test data မှာ (BLEU: 36.22 vs 36.69, GLEU: 37.22 vs 37.62) ဆိုတော့ တက်ပေမဲ့ WER, CER score တွေမှာတော့ comparable ဖြစ်တယ်။**  


## Updating Config File for Syllable Unit (my-en)

ပြောရရင် အထက်က word unit, my-en အတွက်တုန်းက သုံးခဲ့တဲ့ config ဖိုင်နဲ့ အတူတူပါပဲ။  
နာမည်ကိုပဲ အောက်ပါအတိုင်း ပြောင်းခဲ့တယ်။  

```yaml
switchout.syl.my-en: !Experiment
```

## Training for Syllable-SwitchOut (my-en)

```

```

## Reference

- [https://arxiv.org/pdf/1808.07512.pdf](https://arxiv.org/pdf/1808.07512.pdf)
- [Example SwitchOut Configuration File](https://xnmt.readthedocs.io/en/latest/experiment_config_files.html#switchout)

