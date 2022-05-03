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

```

## Training for Word-SwitchOut (en-my)

```
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

## Updating Config File for Word Unit (my-en)

```yaml

```

## Training for Word-SwitchOut (my-en)

```

```

## Updating Config File for Syllable Unit (en-my)

```yaml

```

## Training for Syllable-SwitchOut (en-my)

```

```

## Updating Config File for Syllable Unit (my-en)

```yaml

```

## Training for Syllable-SwitchOut (my-en)

```

```

