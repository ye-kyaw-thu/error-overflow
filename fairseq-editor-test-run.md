# fairseq-editor Test Running Note

## git clone

အရင်ဆုံး ကိုယ့်စက်ထဲကို git clone လုပ်ခဲ့တယ်...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ git clone https://github.com/Izecson/fairseq-editor.git
Cloning into 'fairseq-editor'...
remote: Enumerating objects: 9038, done.
remote: Counting objects: 100% (9038/9038), done.
remote: Compressing objects: 100% (2157/2157), done.
remote: Total 9038 (delta 6774), reused 9034 (delta 6770), pack-reused 0
Receiving objects: 100% (9038/9038), 5.40 MiB | 14.91 MiB/s, done.
Resolving deltas: 100% (6774/6774), done.
```

## run pip install

pip install နဲ့ installation လုပ်ခဲ့တယ်...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool$ cd fairseq-editor/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor$ pip install --editable .
Obtaining file:///home/ye/tool/fairseq-editor
  Installing build dependencies ... done
  Getting requirements to build wheel ... done
  Installing backend dependencies ... done
    Preparing wheel metadata ... done
Requirement already satisfied: cffi in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from fairseq==0.9.0) (1.14.6)
Requirement already satisfied: cython in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from fairseq==0.9.0) (0.29.24)
Requirement already satisfied: regex in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from fairseq==0.9.0) (2021.8.3)
Requirement already satisfied: tqdm in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from fairseq==0.9.0) (4.62.2)
Requirement already satisfied: sacrebleu in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from fairseq==0.9.0) (2.0.0)
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from fairseq==0.9.0) (1.19.4)
Requirement already satisfied: torch in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from fairseq==0.9.0) (1.8.1)
Requirement already satisfied: pycparser in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from cffi->fairseq==0.9.0) (2.20)
Requirement already satisfied: colorama in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from sacrebleu->fairseq==0.9.0) (0.4.4)
Requirement already satisfied: tabulate>=0.8.9 in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from sacrebleu->fairseq==0.9.0) (0.8.9)
Requirement already satisfied: portalocker in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from sacrebleu->fairseq==0.9.0) (2.3.2)
Requirement already satisfied: typing-extensions in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from torch->fairseq==0.9.0) (3.7.4.3)
Requirement already satisfied: dataclasses in /home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages (from torch->fairseq==0.9.0) (0.8)
Installing collected packages: fairseq
  Attempting uninstall: fairseq
    Found existing installation: fairseq 0.10.1
    Uninstalling fairseq-0.10.1:
      Successfully uninstalled fairseq-0.10.1
  Running setup.py develop for fairseq
Successfully installed fairseq-0.7.1
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor$
```

## call --help

ထုံးစံအတိုင်း install လုပ်ထားတဲ့ program က run လို့ ရမရကို --help ခေါ်ကြည့်ပြီး confirmation လုပ်ခဲ့တယ်...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor$ fairseq-interactive --help
usage: fairseq-interactive [-h] [--no-progress-bar] [--log-interval N]
                           [--log-format {json,none,simple,tqdm}]
                           [--tensorboard-logdir DIR] [--seed N] [--cpu]
                           [--fp16] [--memory-efficient-fp16]
                           [--fp16-no-flatten-grads]
                           [--fp16-init-scale FP16_INIT_SCALE]
                           [--fp16-scale-window FP16_SCALE_WINDOW]
                           [--fp16-scale-tolerance FP16_SCALE_TOLERANCE]
                           [--min-loss-scale D]
                           [--threshold-loss-scale THRESHOLD_LOSS_SCALE]
                           [--user-dir USER_DIR]
                           [--empty-cache-freq EMPTY_CACHE_FREQ]
                           [--all-gather-list-size ALL_GATHER_LIST_SIZE]
                           [--criterion {masked_lm,sentence_ranking,composite_loss,sentence_prediction,label_smoothed_cross_entropy,label_smoothed_cross_entropy_with_alignment,binary_cross_entropy,cross_entropy,legacy_masked_lm_loss,adaptive_loss,nat_loss}]
                           [--tokenizer {space,nltk,moses}]
                           [--bpe {gpt2,bert,fastbpe,subword_nmt,hf_byte_bpe,sentencepiece}]
                           [--optimizer {adamax,adadelta,adam,adafactor,lamb,nag,adagrad,sgd}]
                           [--lr-scheduler {reduce_lr_on_plateau,tri_stage,triangular,fixed,cosine,inverse_sqrt,polynomial_decay}]
                           [--task TASK] [--num-workers N]
                           [--skip-invalid-size-inputs-valid-test]
                           [--max-tokens N] [--max-sentences N]
                           [--required-batch-size-multiple N]
                           [--dataset-impl FORMAT] [--gen-subset SPLIT]
                           [--num-shards N] [--shard-id ID] [--path FILE]
                           [--remove-bpe [REMOVE_BPE]] [--quiet]
                           [--model-overrides DICT] [--results-path RESDIR]
                           [--beam N] [--nbest N] [--max-len-a N]
                           [--max-len-b N] [--min-len N] [--match-source-len]
                           [--no-early-stop] [--unnormalized]
                           [--no-beamable-mm] [--lenpen LENPEN]
                           [--unkpen UNKPEN] [--replace-unk [REPLACE_UNK]]
                           [--sacrebleu] [--score-reference]
                           [--prefix-size PS] [--no-repeat-ngram-size N]
                           [--sampling] [--sampling-topk PS]
                           [--sampling-topp PS] [--temperature N]
                           [--diverse-beam-groups N]
                           [--diverse-beam-strength N] [--diversity-rate N]
                           [--print-alignment] [--print-step]
                           [--iter-decode-eos-penalty N]
                           [--iter-decode-deletion-reward ITER_DECODE_DELETION_REWARD]
                           [--iter-decode-max-iter N]
                           [--iter-decode-force-max-iter]
                           [--iter-decode-with-beam N]
                           [--iter-decode-with-external-reranker]
                           [--retain-iter-history] [--constrained-decoding]
                           [--hard-constrained-decoding]
                           [--decoding-format {unigram,ensemble,vote,dp,bs}]
                           [--buffer-size N] [--input FILE] [--has-target]

optional arguments:
  -h, --help            show this help message and exit
  --no-progress-bar     disable progress bar
  --log-interval N      log progress every N batches (when progress bar is
                        disabled)
  --log-format {json,none,simple,tqdm}
                        log format to use
  --tensorboard-logdir DIR
                        path to save logs for tensorboard, should match
                        --logdir of running tensorboard (default: no
                        tensorboard logging)
  --seed N              pseudo random number generator seed
  --cpu                 use CPU instead of CUDA
  --fp16                use FP16
  --memory-efficient-fp16
                        use a memory-efficient version of FP16 training;
                        implies --fp16
  --fp16-no-flatten-grads
                        don't flatten FP16 grads tensor
  --fp16-init-scale FP16_INIT_SCALE
                        default FP16 loss scale
  --fp16-scale-window FP16_SCALE_WINDOW
                        number of updates before increasing loss scale
  --fp16-scale-tolerance FP16_SCALE_TOLERANCE
                        pct of updates that can overflow before decreasing the
                        loss scale
  --min-loss-scale D    minimum FP16 loss scale, after which training is
                        stopped
  --threshold-loss-scale THRESHOLD_LOSS_SCALE
                        threshold FP16 loss scale from below
  --user-dir USER_DIR   path to a python module containing custom extensions
                        (tasks and/or architectures)
  --empty-cache-freq EMPTY_CACHE_FREQ
                        how often to clear the PyTorch CUDA cache (0 to
                        disable)
  --all-gather-list-size ALL_GATHER_LIST_SIZE
                        number of bytes reserved for gathering stats from
                        workers
  --criterion {masked_lm,sentence_ranking,composite_loss,sentence_prediction,label_smoothed_cross_entropy,label_smoothed_cross_entropy_with_alignment,binary_cross_entropy,cross_entropy,legacy_masked_lm_loss,adaptive_loss,nat_loss}
  --tokenizer {space,nltk,moses}
  --bpe {gpt2,bert,fastbpe,subword_nmt,hf_byte_bpe,sentencepiece}
  --optimizer {adamax,adadelta,adam,adafactor,lamb,nag,adagrad,sgd}
  --lr-scheduler {reduce_lr_on_plateau,tri_stage,triangular,fixed,cosine,inverse_sqrt,polynomial_decay}
  --task TASK           task
  --dataset-impl FORMAT
                        output dataset implementation

Dataset and data loading:
  --num-workers N       how many subprocesses to use for data loading
  --skip-invalid-size-inputs-valid-test
                        ignore too long or too short lines in valid and test
                        set
  --max-tokens N        maximum number of tokens in a batch
  --max-sentences N, --batch-size N
                        maximum number of sentences in a batch
  --required-batch-size-multiple N
                        batch size will be a multiplier of this value
  --gen-subset SPLIT    data subset to generate (train, valid, test)
  --num-shards N        shard generation over N shards
  --shard-id ID         id of the shard to generate (id < num_shards)

Generation:
  --path FILE           path(s) to model file(s), colon separated
  --remove-bpe [REMOVE_BPE]
                        remove BPE tokens before scoring (can be set to
                        sentencepiece)
  --quiet               only print final scores
  --model-overrides DICT
                        a dictionary used to override model args at generation
                        that were used during model training
  --results-path RESDIR
                        path to save eval results (optional)"
  --beam N              beam size
  --nbest N             number of hypotheses to output
  --max-len-a N         generate sequences of maximum length ax + b, where x
                        is the source length
  --max-len-b N         generate sequences of maximum length ax + b, where x
                        is the source length
  --min-len N           minimum generation length
  --match-source-len    generations should match the source length
  --no-early-stop       deprecated
  --unnormalized        compare unnormalized hypothesis scores
  --no-beamable-mm      don't use BeamableMM in attention layers
  --lenpen LENPEN       length penalty: <1.0 favors shorter, >1.0 favors
                        longer sentences
  --unkpen UNKPEN       unknown word penalty: <0 produces more unks, >0
                        produces fewer
  --replace-unk [REPLACE_UNK]
                        perform unknown replacement (optionally with alignment
                        dictionary)
  --sacrebleu           score with sacrebleu
  --score-reference     just score the reference translation
  --prefix-size PS      initialize generation by target prefix of given length
  --no-repeat-ngram-size N
                        ngram blocking such that this size ngram cannot be
                        repeated in the generation
  --sampling            sample hypotheses instead of using beam search
  --sampling-topk PS    sample from top K likely next words instead of all
                        words
  --sampling-topp PS    sample from the smallest set whose cumulative
                        probability mass exceeds p for next words
  --temperature N       temperature for generation
  --diverse-beam-groups N
                        number of groups for Diverse Beam Search
  --diverse-beam-strength N
                        strength of diversity penalty for Diverse Beam Search
  --diversity-rate N    strength of diversity penalty for Diverse Siblings
                        Search
  --print-alignment     if set, uses attention feedback to compute and print
                        alignment to source tokens
  --print-step
  --iter-decode-eos-penalty N
                        if > 0.0, it penalizes early-stopping in decoding.
  --iter-decode-deletion-reward ITER_DECODE_DELETION_REWARD
                        it rewards deletion in decoding.
  --iter-decode-max-iter N
                        maximum iterations for iterative refinement.
  --iter-decode-force-max-iter
                        if set, run exact the maximum number of iterations
                        without early stop
  --iter-decode-with-beam N
                        if > 1, model will generate translations varying by
                        the lengths.
  --iter-decode-with-external-reranker
                        if set, the last checkpoint are assumed to be a
                        reranker to rescore the translations
  --retain-iter-history
                        if set, decoding returns the whole history of
                        iterative refinement
  --constrained-decoding
                        if set, run lexically constrained decoding
  --hard-constrained-decoding
                        if set, treat all lexical constraints as hard
                        constraints
  --decoding-format {unigram,ensemble,vote,dp,bs}

Interactive:
  --buffer-size N       read this many sentences into a buffer before
                        processing them
  --input FILE          file to read from; use - for stdin
  --has-target          if set, read target sequences from input
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor$
```

ဒီ fairseq-editor လို ပရိုဂရမ်မျိုးက researcher တွေအတွက် ရည်ရွယ်တာမို့ developing လုပ်နေတုန်းမို့ အထက်မှာ မြင်ရတဲ့ အတိုင်း option တွေက အများကြီးရှိတယ်။  
အားလုံး နားလည်ဖို့က အမျိုးမျိုး စမ်းကြည့်တာ၊ Neural Network modeling နဲ့ ပတ်သက်တာတွေလည်း လေ့လာတာတွေလုပ်ပြီးမှ နားလည်နိုင်လိမ့်မယ်။  

## copy pretrained-model folder

ဒီနေရာမှာတော့ training လုပ်တာ မဟုတ်ပဲ Facebook က example အနေနဲ့ training လုပ်ပေးထားတဲ့ pre-trained model ကိုပဲ သုံးပြီးတော့ ဘာသာပြန်ကြည့်ကြရအောင်...  
ဆရာ့ စက်ထဲမှာက download လုပ်ထားပြီးသားမို့ mv ဆိုတဲ့ command နဲ့ပဲ လက်ရှိ path အောက်ကို ရွှေ့လိုက်တယ်။ တနည်အားဖြင့်က copy ကူးယူတာပါပဲ...  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor$ mv ../pre-trained/ .
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor$ cd pre-trained/
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor/pre-trained$ ls
wmt14.en-fr.fconv-py
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor/pre-trained$ tree
.
└── wmt14.en-fr.fconv-py
    ├── bpecodes
    ├── dict.en.txt
    ├── dict.fr.txt
    ├── model.pt
    └── README.md

1 directory, 5 files
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor/pre-trained$ 
```

## Test with pre-trained model

Download လုပ်ထားတဲ့ pre-trained မော်ဒယ်က English ကနေ French ကို ဘာသာပြန်ပေးတဲ့ မော်ဒယ်မို့လို့ အောက်ပါအတိုင်း command ပေး run ပြီးတော့ အင်္ဂလိပ်စာကြောင်း ၃ ကြောင်းကို ဘာသာပြန်စမ်းကြည့်ခဲ့တယ်။  

```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq-editor/pre-trained$ fairseq-interactive --path /home/ye/tool/fairseq-editor/pre-trained/wmt14.en-fr.fconv-py/model.pt /home/ye/tool/fairseq-editor/pre-trained/wmt14.en-fr.fconv-py/ --beam 5 --source-lang en --target-lang fr
2021-08-31 20:24:21 | INFO | fairseq_cli.interactive | Namespace(all_gather_list_size=16384, beam=5, bpe=None, buffer_size=1, constrained_decoding=False, cpu=False, criterion='cross_entropy', data='/home/ye/tool/fairseq-editor/pre-trained/wmt14.en-fr.fconv-py/', dataset_impl=None, decoding_format=None, diverse_beam_groups=-1, diverse_beam_strength=0.5, diversity_rate=-1.0, empty_cache_freq=0, eval_bleu=False, eval_bleu_args=None, eval_bleu_detok='space', eval_bleu_detok_args=None, eval_bleu_print_samples=False, eval_bleu_remove_bpe=None, eval_tokenized_bleu=False, force_anneal=None, fp16=False, fp16_init_scale=128, fp16_no_flatten_grads=False, fp16_scale_tolerance=0.0, fp16_scale_window=None, gen_subset='test', hard_constrained_decoding=False, has_target=False, input='-', iter_decode_deletion_reward=0.0, iter_decode_eos_penalty=0.0, iter_decode_force_max_iter=False, iter_decode_max_iter=10, iter_decode_with_beam=1, iter_decode_with_external_reranker=False, left_pad_source='True', left_pad_target='False', lenpen=1, load_alignments=False, log_format=None, log_interval=100, lr_scheduler='fixed', lr_shrink=0.1, match_source_len=False, max_len_a=0, max_len_b=200, max_sentences=1, max_source_positions=1024, max_target_positions=1024, max_tokens=None, memory_efficient_fp16=False, min_len=1, min_loss_scale=0.0001, model_overrides='{}', momentum=0.99, nbest=1, no_beamable_mm=False, no_early_stop=False, no_progress_bar=False, no_repeat_ngram_size=0, num_shards=1, num_workers=1, optimizer='nag', path='/home/ye/tool/fairseq-editor/pre-trained/wmt14.en-fr.fconv-py/model.pt', prefix_size=0, print_alignment=False, print_step=False, quiet=False, remove_bpe=None, replace_unk=None, required_batch_size_multiple=8, results_path=None, retain_iter_history=False, sacrebleu=False, sampling=False, sampling_topk=-1, sampling_topp=-1.0, score_reference=False, seed=1, shard_id=0, skip_invalid_size_inputs_valid_test=False, source_lang='en', target_lang='fr', task='translation', temperature=1.0, tensorboard_logdir='', threshold_loss_scale=None, tokenizer=None, truncate_source=False, unkpen=0, unnormalized=False, upsample_primary=1, user_dir=None, warmup_updates=0, weight_decay=0.0)
2021-08-31 20:24:21 | INFO | fairseq.tasks.translation | [en] dictionary: 43771 types
2021-08-31 20:24:21 | INFO | fairseq.tasks.translation | [fr] dictionary: 43807 types
2021-08-31 20:24:21 | INFO | fairseq_cli.interactive | loading model(s) from /home/ye/tool/fairseq-editor/pre-trained/wmt14.en-fr.fconv-py/model.pt
2021-08-31 20:24:29 | INFO | fairseq_cli.interactive | NOTE: hypothesis and token scores are output in base 2
2021-08-31 20:24:29 | INFO | fairseq_cli.interactive | Type the input sentence and press return:
how are you ?
S-0	how are you ?
H-0	-0.5507358722786887	Comment êtes @-@ vous ?
P-0	-0.9831 -1.6671 -0.2074 -0.1149 -0.1515 -0.1804
my name is Ye and i am from Myanmar
S-1	my name is <unk> and i am from Myanmar
H-1	-1.1770918282111509	Mon nom est le suivant et je viens du Myanmar
P-1	-3.0630 -0.0656 -0.2386 -3.6837 -1.9361 -1.3733 -0.6389 -1.0310 -0.1910 -0.0497 -0.6770
I can speak french well
S-2	I can speak french well
H-2	-0.7469062921458309	Je peux parler français bien .
P-2	-0.6483 -0.8910 -0.4548 -0.4325 -1.3370 -1.2950 -0.1697
```

အထက်ပါအတိုင်း အင်္ဂလိပ်ကနေ ပြင်သစ် ဘာသာကို ပြန်ပေးတာကို တွေ့ရပါလိမ့်မယ်။  

## How to download the pre-trained model

တကယ်လို့ ကိုယ့်စက်ထဲမှာ pre-trained model က download မလုပ်ရသေးရင် အောက်ပါအတိုင်း download လုပ်ယူပါ...  

```
$ time curl https://dl.fbaipublicfiles.com/fairseq/models/wmt14.v2.en-fr.fconv-py.tar.bz2 | tar xvjf -
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0 1909M    0  545k    0     0   242k      0  2:14:24  0:00:02  2:14:22  242kwmt14.en-fr.fconv-py/
wmt14.en-fr.fconv-py/model.pt
 99 1909M   99 1902M    0     0  9830k      0  0:03:18  0:03:18 --:--:-- 10.0Mwmt14.en-fr.fconv-py/dict.en.txt
wmt14.en-fr.fconv-py/dict.fr.txt
100 1909M  100 1909M    0     0  9830k      0  0:03:18  0:03:18 --:--:--  9.8M
wmt14.en-fr.fconv-py/bpecodes
wmt14.en-fr.fconv-py/README.md

real	3m18.993s
user	2m16.286s
sys	0m20.857s
```

## Reference

- https://stackoverflow.com/questions/65543178/fairseq-transform-model-not-working-float-cant-be-cast-to-long
- https://varhowto.com/install-pytorch-ubuntu-20-04/

##  Error with fairseq (i.e. not fairseq-editor)

fairseq နဲ့က (fairseq-editor မဟုတ်ဘူးနော်) အောက်ပါလိုမျိုး error ရခဲ့သေးတယ်  
(ဆရာ့စက်ထဲမှာက fairseq က installation လုပ်ပြီးသားရှိခဲ့တယ်။ fairseq-editor ဆိုတဲ့ new approach သာ မရှိခဲ့တာ... )  

**When I run Test Translation with fairseq, I got following ERROR!**   

Ref: https://fairseq.readthedocs.io/en/latest/getting_started.html    

```bash
fairseq-interactive \
    --path /home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/model.pt /home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/ \
    --beam 5 --source-lang en --target-lang fr \
    --tokenizer /home/ye/tool/mosesbin/ubuntu-17.04/moses \
    --bpe subword_nmt --bpe-codes /home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/bpecodes
```

အထက်ပါအတိုင်း run ရင် error ပေးတယ်။   
--tokenizer နဲ့ --bpe နဲ့ --bpe-codes option တွေကို မသိဘူး။   

အဲဒီ option သုံးခုကို ဖြုတ်လိုက်ပြီး run တော့ model ကတော့ load လုပ်သွားတယ်။   
သို့သော် အင်္ဂလိပ်စာကို ရိုက်ပြီး ဘာသာပြန်ခိုင်းတဲ့အခါမှာတော့ ... အောက်ပါအတိုင်း error ပေးတယ်...  


```
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py$ fairseq-interactive     --path /home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/model.pt /home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/     --beam 5 --source-lang en --target-lang fr
Namespace(beam=5, buffer_size=1, cpu=False, criterion='cross_entropy', data='/home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/', dataset_impl='cached', diverse_beam_groups=-1, diverse_beam_strength=0.5, force_anneal=None, fp16=False, fp16_init_scale=128, fp16_scale_tolerance=0.0, fp16_scale_window=None, gen_subset='test', input='-', lazy_load=False, left_pad_source='True', left_pad_target='False', lenpen=1, log_format=None, log_interval=1000, lr_scheduler='fixed', lr_shrink=0.1, match_source_len=False, max_len_a=0, max_len_b=200, max_sentences=1, max_source_positions=1024, max_target_positions=1024, max_tokens=None, memory_efficient_fp16=False, min_len=1, min_loss_scale=0.0001, model_overrides='{}', momentum=0.99, nbest=1, no_beamable_mm=False, no_early_stop=False, no_progress_bar=False, no_repeat_ngram_size=0, num_shards=1, num_workers=0, optimizer='nag', path='/home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/model.pt', prefix_size=0, print_alignment=False, quiet=False, raw_text=False, remove_bpe=None, replace_unk=None, required_batch_size_multiple=8, results_path=None, sacrebleu=False, sampling=False, sampling_topk=-1, score_reference=False, seed=1, shard_id=0, skip_invalid_size_inputs_valid_test=False, source_lang='en', target_lang='fr', task='translation', tbmf_wrapper=False, temperature=1.0, tensorboard_logdir='', threshold_loss_scale=None, unkpen=0, unnormalized=False, upsample_primary=1, user_dir=None, warmup_updates=0, weight_decay=0.0)
| [en] dictionary: 43771 types
| [fr] dictionary: 43807 types
| loading model(s) from /home/ye/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py/model.pt
my name is Ye
| Type the input sentence and press return:
Traceback (most recent call last):
  File "/home/ye/anaconda3/envs/py3.6env/bin/fairseq-interactive", line 8, in <module>
    sys.exit(cli_main())
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/fairseq_cli/interactive.py", line 185, in cli_main
    main(args)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/fairseq_cli/interactive.py", line 144, in main
    translations = task.inference_step(generator, models, sample)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/fairseq/tasks/fairseq_task.py", line 245, in inference_step
    return generator.generate(models, sample, prefix_tokens=prefix_tokens)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/torch/autograd/grad_mode.py", line 27, in decorate_context
    return func(*args, **kwargs)
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/fairseq/sequence_generator.py", line 397, in generate
    scores.view(bsz, beam_size, -1)[:, :, :step],
  File "/home/ye/anaconda3/envs/py3.6env/lib/python3.6/site-packages/fairseq/search.py", line 83, in step
    torch.div(self.indices_buf, vocab_size, out=self.beams_buf)
RuntimeError: result type Float can't be cast to the desired output type Long
(py3.6env) ye@administrator-HP-Z2-Tower-G4-Workstation:~/tool/fairseq/pre-trained/wmt14.en-fr.fconv-py$ 
```
  
အဲဒီလိုမျိုး error က အောက်ပါ solution နဲ့ ပြေလည်ကောင်း ပြေလည်နိုင်တယ်...   

```
conda install -c conda-forge pytorch cudatoolkit=11.0 nvidia-apex fairseq==0.10.1 sentencepiece
```

