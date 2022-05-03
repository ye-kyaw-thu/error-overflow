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

## Updating Config File for Word Unit (en-my)

```yaml

```

## Training for Word-SwitchOut (en-my)

```

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

