# Multi-Source MuHaung Braille Post Editing Experiment

## Some References

multi-source experiment ကို ရှေ့မှာလည်း လုပ်ခဲ့ပေမဲ့ မြန်မာမျက်မမြင်စာ မူဟောင်း post-editing အလုပ်အတွက် ပြန်လေ့လာခဲ့တယ်။  
တချို့ link တွေက အောက်ပါအတိုင်း...  

- [https://github.com/marian-nmt/marian-regression-tests/blob/master/tests/training/models/multi-source/test_multi-transformer.sh](https://github.com/marian-nmt/marian-regression-tests/blob/master/tests/training/models/multi-source/test_multi-transformer.sh)

```
$MRT_MARIAN/marian \
    --seed 1111 --no-shuffle --clip-norm 0 \
    --type multi-transformer --dim-emb 128 --dim-rnn 256 --cost-type ce-mean \
    -m multi-transformer/model.npz -t train.bpe.{en,xx,de} -v vocab.en.yml vocab.xx.yml vocab.de.yml \
    --disp-freq 20 --after-batches 100 \
    --log multi-transformer.log
```

- [https://marian-nmt.github.io/examples/postedit/](https://marian-nmt.github.io/examples/postedit/)
- [https://marian-nmt.github.io/examples/exploration/](https://marian-nmt.github.io/examples/exploration/)
- [https://groups.google.com/g/marian-nmt/c/_mYpKj21suY?pli=1](https://groups.google.com/g/marian-nmt/c/_mYpKj21suY?pli=1)
- [https://cris.fbk.eu/retrieve/handle/11582/316423/25741/WMT080.pdf](https://cris.fbk.eu/retrieve/handle/11582/316423/25741/WMT080.pdf)
- [opus-cat-a-state-of-the-art-neural-machine-translation-engine-on-your-local-computer](https://www.ata-chronicle.online/highlights/opus-cat-a-state-of-the-art-neural-machine-translation-engine-on-your-local-computer/)

## Command Line Arguments of Marian

marian command ရဲ့ option တွေကိုလည်း ပြန်လည်လေ့လာဖြစ်ခဲ့တယ်။  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ marian --help
Marian: Fast Neural Machine Translation in C++
Usage: marian [OPTIONS]

General options:
  -h,--help                             Print this help message and exit
  --version                             Print the version number and exit
  --authors                             Print list of authors and exit
  --cite                                Print citation and exit
  --build-info TEXT                     Print CMake build options and exit. Set to 'all' to print advanced options
  -c,--config VECTOR ...                Configuration file(s). If multiple, later overrides earlier
  -w,--workspace UINT=2048              Preallocate  arg  MB of work space
  --log TEXT                            Log training process information to file given by  arg
  --log-level TEXT=info                 Set verbosity level of logging: trace, debug, info, warn, err(or), critical, off
  --log-time-zone TEXT                  Set time zone for the date shown on logging
  --quiet                               Suppress all logging to stderr. Logging to files still works
  --quiet-translation                   Suppress logging for translation
  --seed UINT                           Seed for all random number generators. 0 means initialize randomly
  --interpolate-env-vars                allow the use of environment variables in paths, of the form ${VAR_NAME}
  --relative-paths                      All paths are relative to the config file location
  --dump-config TEXT                    Dump current (modified) configuration to stdout and exit. Possible values: full, minimal, expand
  --sigterm TEXT=save-and-exit          What to do with SIGTERM: save-and-exit or exit-immediately.


Model options:
  -m,--model TEXT=model.npz             Path prefix for model to be saved/resumed. Supported file extensions: .npz, .bin
  --pretrained-model TEXT               Path prefix for pre-trained model to initialize model weights
  --ignore-model-config                 Ignore the model configuration saved in npz file
  --type TEXT=amun                      Model type: amun, nematus, s2s, multi-s2s, transformer
  --dim-vocabs VECTOR=0,0 ...           Maximum items in vocabulary ordered by rank, 0 uses all items in the provided/created vocabulary file
  --dim-emb INT=512                     Size of embedding vector
  --lemma-dim-emb INT=0                 Re-embedding dimension of lemma in factors
  --dim-rnn INT=1024                    Size of rnn hidden state
  --enc-type TEXT=bidirectional         Type of encoder RNN : bidirectional, bi-unidirectional, alternating (s2s)
  --enc-cell TEXT=gru                   Type of RNN cell: gru, lstm, tanh (s2s)
  --enc-cell-depth INT=1                Number of transitional cells in encoder layers (s2s)
  --enc-depth INT=1                     Number of encoder layers (s2s)
  --dec-cell TEXT=gru                   Type of RNN cell: gru, lstm, tanh (s2s)
  --dec-cell-base-depth INT=2           Number of transitional cells in first decoder layer (s2s)
  --dec-cell-high-depth INT=1           Number of transitional cells in next decoder layers (s2s)
  --dec-depth INT=1                     Number of decoder layers (s2s)
  --skip                                Use skip connections (s2s)
  --layer-normalization                 Enable layer normalization
  --right-left                          Train right-to-left model
  --input-types VECTOR ...              Provide type of input data if different than 'sequence'. Possible values: sequence, class, alignment, weight. You need to provide one type per input file (if --train-sets) or per TSV field (if --tsv).
  --best-deep                           Use Edinburgh deep RNN configuration (s2s)
  --tied-embeddings                     Tie target embeddings and output embeddings in output layer
  --tied-embeddings-src                 Tie source and target embeddings
  --tied-embeddings-all                 Tie all embedding layers and output layer
  --output-omit-bias                    Do not use a bias vector in decoder output layer
  --transformer-heads INT=8             Number of heads in multi-head attention (transformer)
  --transformer-no-projection           Omit linear projection after multi-head attention (transformer)
  --transformer-pool                    Pool encoder states instead of using cross attention (selects first encoder state, best used with special token)
  --transformer-dim-ffn INT=2048        Size of position-wise feed-forward network (transformer)
  --transformer-ffn-depth INT=2         Depth of filters (transformer)
  --transformer-ffn-activation TEXT=swish
                                        Activation between filters: swish or relu (transformer)
  --transformer-dim-aan INT=2048        Size of position-wise feed-forward network in AAN (transformer)
  --transformer-aan-depth INT=2         Depth of filter for AAN (transformer)
  --transformer-aan-activation TEXT=swish
                                        Activation between filters in AAN: swish or relu (transformer)
  --transformer-aan-nogate              Omit gate in AAN (transformer)
  --transformer-decoder-autoreg TEXT=self-attention
                                        Type of autoregressive layer in transformer decoder: self-attention, average-attention (transformer)
  --transformer-tied-layers VECTOR ...  List of tied decoder layers (transformer)
  --transformer-guided-alignment-layer TEXT=last
                                        Last or number of layer to use for guided alignment training in transformer
  --transformer-preprocess TEXT         Operation before each transformer layer: d = dropout, a = add, n = normalize
  --transformer-postprocess-emb TEXT=d  Operation after transformer embedding layer: d = dropout, a = add, n = normalize
  --transformer-postprocess TEXT=dan    Operation after each transformer layer: d = dropout, a = add, n = normalize
  --transformer-postprocess-top TEXT    Final operation after a full transformer stack: d = dropout, a = add, n = normalize. The optional skip connection with 'a' by-passes the entire stack.
  --transformer-train-position-embeddings
                                        Train positional embeddings instead of using static sinusoidal embeddings
  --transformer-depth-scaling           Scale down weight initialization in transformer layers by 1 / sqrt(depth)
  --bert-mask-symbol TEXT=[MASK]        Masking symbol for BERT masked-LM training
  --bert-sep-symbol TEXT=[SEP]          Sentence separator symbol for BERT next sentence prediction training
  --bert-class-symbol TEXT=[CLS]        Class symbol BERT classifier training
  --bert-masking-fraction FLOAT=0.15    Fraction of masked out tokens during training
  --bert-train-type-embeddings=true     Train bert type embeddings, set to false to use static sinusoidal embeddings
  --bert-type-vocab-size INT=2          Size of BERT type vocab (sentence A and B)
  --dropout-rnn FLOAT                   Scaling dropout along rnn layers and time (0 = no dropout)
  --dropout-src FLOAT                   Dropout source words (0 = no dropout)
  --dropout-trg FLOAT                   Dropout target words (0 = no dropout)
  --grad-dropping-rate FLOAT            Gradient Dropping rate (0 = no gradient Dropping)
  --grad-dropping-momentum FLOAT        Gradient Dropping momentum decay rate (0.0 to 1.0)
  --grad-dropping-warmup UINT=100       Do not apply gradient dropping for the first arg steps
  --transformer-dropout FLOAT           Dropout between transformer layers (0 = no dropout)
  --transformer-dropout-attention FLOAT Dropout for transformer attention (0 = no dropout)
  --transformer-dropout-ffn FLOAT       Dropout for transformer filter (0 = no dropout)


Training options:
  --cost-type TEXT=ce-sum               Optimization criterion: ce-mean, ce-mean-words, ce-sum, perplexity
  --multi-loss-type TEXT=sum            How to accumulate multi-objective losses: sum, scaled, mean
  --unlikelihood-loss                   Use word-level weights as indicators for sequence-level unlikelihood training
  --overwrite                           Do not create model checkpoints, only overwrite main model file with last checkpoint. Reduces disk usage
  --no-reload                           Do not load existing model specified in --model arg
  -t,--train-sets VECTOR ...            Paths to training corpora: source target
  -v,--vocabs VECTOR ...                Paths to vocabulary files have to correspond to --train-sets. If this parameter is not supplied we look for vocabulary files source.{yml,json} and target.{yml,json}. If these files do not exist they are created
  --sentencepiece-alphas VECTOR ...     Sampling factors for SentencePiece vocabulary; i-th factor corresponds to i-th vocabulary
  --sentencepiece-options TEXT          Pass-through command-line options to SentencePiece trainer
  --sentencepiece-max-lines UINT=2000000
                                        Maximum lines to train SentencePiece vocabulary, selected with sampling from all data. When set to 0 all lines are going to be used.
  -e,--after-epochs UINT                Finish after this many epochs, 0 is infinity (deprecated, '--after-epochs N' corresponds to '--after Ne')
  --after-batches UINT                  Finish after this many batch updates, 0 is infinity (deprecated, '--after-batches N' corresponds to '--after Nu')
  -a,--after TEXT=0e                    Finish after this many chosen training units, 0 is infinity (e.g. 100e = 100 epochs, 10Gt = 10 billion target labels, 100Ku = 100,000 updates
  --disp-freq TEXT=1000u                Display information every  arg  updates (append 't' for every  arg  target labels)
  --disp-first UINT                     Display information for the first  arg  updates
  --disp-label-counts=true              Display label counts when logging loss progress
  --save-freq TEXT=10000u               Save model file every  arg  updates (append 't' for every  arg  target labels)
  --logical-epoch VECTOR=1e,0 ...       Redefine logical epoch counter as multiple of data epochs (e.g. 1e), updates (e.g. 100Ku) or labels (e.g. 1Gt). Second parameter defines width of fractional display, 0 by default.
  --max-length UINT=50                  Maximum length of a sentence in a training sentence pair
  --max-length-crop                     Crop a sentence to max-length instead of omitting it if longer than max-length
  --tsv                                 Tab-separated input
  --tsv-fields UINT                     Number of fields in the TSV input. By default, it is guessed based on the model type
  --shuffle TEXT=data                   How to shuffle input data (data: shuffles data and sorted batches; batches: data is read in order into batches, but batches are shuffled; none: no shuffling). Use with '--maxi-batch-sort none' in order to achieve exact reading order
  --no-shuffle                          Shortcut for backwards compatiblity, equivalent to --shuffle none (deprecated)
  --no-restore-corpus                   Skip restoring corpus state after training is restarted
  -T,--tempdir TEXT=/tmp                Directory for temporary (shuffled) files and database
  --sqlite TEXT                         Use disk-based sqlite3 database for training corpus storage, default is temporary with path creates persistent storage
  --sqlite-drop                         Drop existing tables in sqlite3 database
  -d,--devices VECTOR=0 ...             Specifies GPU ID(s) to use for training. Defaults to 0..num-devices-1
  --num-devices UINT                    Number of GPUs to use for this process. Defaults to length(devices) or 1
  --no-nccl                             Disable inter-GPU communication via NCCL
  --cpu-threads UINT=0                  Use CPU-based computation with this many independent threads, 0 means GPU-based computation
  --mini-batch INT=64                   Size of mini-batch used during update
  --mini-batch-words INT                Set mini-batch size based on words instead of sentences
  --mini-batch-fit                      Determine mini-batch size automatically based on sentence-length to fit reserved memory
  --mini-batch-fit-step UINT=10         Step size for mini-batch-fit statistics
  --gradient-checkpointing              Enable gradient-checkpointing to minimize memory usage
  --maxi-batch INT=100                  Number of batches to preload for length-based sorting
  --maxi-batch-sort TEXT=trg            Sorting strategy for maxi-batch: none, src, trg (not available for decoder)
  --shuffle-in-ram                      Keep shuffled corpus in RAM, do not write to temp file
  --all-caps-every UINT                 When forming minibatches, preprocess every Nth line on the fly to all-caps. Assumes UTF-8
  --english-title-case-every UINT       When forming minibatches, preprocess every Nth line on the fly to title-case. Assumes English (ASCII only)
  --mini-batch-words-ref INT            If given, the following hyper parameters are adjusted as-if we had this mini-batch size: --learn-rate, --optimizer-params, --exponential-smoothing, --mini-batch-warmup
  --mini-batch-warmup TEXT=0            Linear ramp-up of MB size, up to this #updates (append 't' for up to this #target labels). Auto-adjusted to --mini-batch-words-ref if given
  --mini-batch-track-lr                 Dynamically track mini-batch size inverse to actual learning rate (not considering lr-warmup)
  -o,--optimizer TEXT=adam              Optimization algorithm: sgd, adagrad, adam
  --optimizer-params VECTOR ...         Parameters for optimization algorithm, e.g. betas for Adam. Auto-adjusted to --mini-batch-words-ref if given
  --optimizer-delay FLOAT=1             SGD update delay (#batches between updates). 1 = no delay. Can be fractional, e.g. 0.1 to use only 10% of each batch
  --sync-sgd                            Use synchronous SGD instead of asynchronous for multi-gpu training
  -l,--learn-rate FLOAT=0.0001          Learning rate. Auto-adjusted to --mini-batch-words-ref if given
  --lr-report                           Report learning rate for each update
  --lr-decay FLOAT                      Per-update decay factor for learning rate: lr <- lr * arg (0 to disable)
  --lr-decay-strategy TEXT=epoch+stalled
                                        Strategy for learning rate decaying: epoch, batches, stalled, epoch+batches, epoch+stalled
  --lr-decay-start VECTOR=10,1 ...      The first number of (epoch, batches, stalled) validations to start learning rate decaying (tuple)
  --lr-decay-freq UINT=50000            Learning rate decaying frequency for batches, requires --lr-decay-strategy to be batches
  --lr-decay-reset-optimizer            Reset running statistics of optimizer whenever learning rate decays
  --lr-decay-repeat-warmup              Repeat learning rate warmup when learning rate is decayed
  --lr-decay-inv-sqrt VECTOR=0 ...      Decrease learning rate at arg / sqrt(no. batches) starting at arg  (append 't' or 'e' for sqrt(target labels or epochs)). Add second argument to define the starting point (default: same as first value)
  --lr-warmup TEXT=0                    Increase learning rate linearly for  arg  first batches (append 't' for  arg  first target labels)
  --lr-warmup-start-rate FLOAT          Start value for learning rate warmup
  --lr-warmup-cycle                     Apply cyclic warmup
  --lr-warmup-at-reload                 Repeat warmup after interrupted training
  --label-smoothing FLOAT               Epsilon for label smoothing (0 to disable)
  --factor-weight FLOAT=1               Weight for loss function for factors (factored vocab only) (1 to disable)
  --clip-norm FLOAT=1                   Clip gradient norm to  arg  (0 to disable)
  --exponential-smoothing FLOAT=0       Maintain smoothed version of parameters for validation and saving with smoothing factor. 0 to disable. Auto-adjusted to --mini-batch-words-ref if given.
  --guided-alignment TEXT=none          Path to a file with word alignments. Use guided alignment to guide attention or 'none'. If --tsv it specifies the index of a TSV field that contains the alignments (0-based)
  --guided-alignment-cost TEXT=mse      Cost type for guided alignment: ce (cross-entropy), mse (mean square error), mult (multiplication)
  --guided-alignment-weight FLOAT=0.1   Weight for guided alignment cost
  --data-weighting TEXT                 Path to a file with sentence or word weights. If --tsv it specifies the index of a TSV field that contains the weights (0-based)
  --data-weighting-type TEXT=sentence   Processing level for data weighting: sentence, word
  --embedding-vectors VECTOR ...        Paths to files with custom source and target embedding vectors
  --embedding-normalization             Normalize values from custom embedding vectors to [-1, 1]
  --embedding-fix-src                   Fix source embeddings. Affects all encoders
  --embedding-fix-trg                   Fix target embeddings. Affects all decoders
  --fp16                                Shortcut for mixed precision training with float16 and cost-scaling, corresponds to: --precision float16 float32 float32 --cost-scaling 7 2000 2 0.05 10 1
  --precision VECTOR=float32,float32,float32 ...
                                        Mixed precision training for forward/backward pass and optimizaton. Defines types for: forward/backward, optimization, saving.
  --cost-scaling VECTOR ...             Dynamic cost scaling for mixed precision training: power of 2, scaling window, scaling factor, tolerance, range, minimum factor
  --normalize-gradient                  Normalize gradient by multiplying with no. devices / total labels
  --train-embedder-rank VECTOR ...      Override model configuration and train a embedding similarity ranker with the model encoder, parameters encode margin and an optional normalization factor
  --multi-node                          Enable asynchronous multi-node training through MPI (and legacy sync if combined with --sync-sgd)
  --multi-node-overlap=true             Overlap model computations with MPI communication
  --quantize-bits UINT=0                Number of bits to compress model to. Set to 0 to disable
  --quantize-optimization-steps UINT=0  Adjust quantization scaling factor for N steps
  --quantize-log-based                  Uses log-based quantization
  --quantize-biases                     Apply quantization to biases
  --ulr                                 Enable ULR (Universal Language Representation)
  --ulr-query-vectors TEXT              Path to file with universal sources embeddings from projection into universal space
  --ulr-keys-vectors TEXT               Path to file with universal sources embeddings of traget keys from projection into universal space
  --ulr-trainable-transformation        Make Query Transformation Matrix A trainable
  --ulr-dim-emb INT                     ULR monolingual embeddings dimension
  --ulr-dropout FLOAT=0                 ULR dropout on embeddings attentions. Default is no dropout
  --ulr-softmax-temperature FLOAT=1     ULR softmax temperature to control randomness of predictions. Deafult is 1.0: no temperature
  --task VECTOR ...                     Use predefined set of options. Possible values: transformer, transformer-big


Validation set options:
  --valid-sets VECTOR ...               Paths to validation corpora: source target
  --valid-freq TEXT=10000u              Validate model every  arg  updates (append 't' for every  arg  target labels)
  --valid-metrics VECTOR=cross-entropy ...
                                        Metric to use during validation: cross-entropy, ce-mean-words, perplexity, valid-script, translation, bleu, bleu-detok (deprecated, same as bleu), bleu-segmented, chrf. Multiple metrics can be specified
  --valid-reset-stalled                 Reset all stalled validation metrics when the training is restarted
  --early-stopping UINT=10              Stop if the first validation metric does not improve for  arg  consecutive validation steps
  -b,--beam-size UINT=12                Beam size used during search with validating translator
  -n,--normalize FLOAT=0                Divide translation score by pow(translation length, arg)
  --max-length-factor FLOAT=3           Maximum target length as source length times factor
  --word-penalty FLOAT                  Subtract (arg * translation length) from translation score 
  --allow-unk                           Allow unknown words to appear in output
  --n-best                              Generate n-best list
  --word-scores                         Print word-level scores. One score per subword unit, not normalized even if --normalize
  --valid-mini-batch INT=32             Size of mini-batch used during validation
  --valid-max-length UINT=1000          Maximum length of a sentence in a validating sentence pair. Sentences longer than valid-max-length are cropped to valid-max-length
  --valid-script-path TEXT              Path to external validation script. It should print a single score to stdout. If the option is used with validating translation, the output translation file will be passed as a first argument
  --valid-script-args VECTOR ...        Additional args passed to --valid-script-path. These are inserted between the script path and the output translation-file path
  --valid-translation-output TEXT       (Template for) path to store the translation. E.g., validation-output-after-{U}-updates-{T}-tokens.txt. Template parameters: {E} for epoch; {B} for No. of batches within epoch; {U} for total No. of updates; {T} for total No. of tokens seen.
  --keep-best                           Keep best model for each validation metric
  --valid-log TEXT                      Log validation scores to file given by  arg
(base) ye@:/media/ye/project2/exp/braille-nmt$ 
```

## Study on APE-WMT16 Configuration File

Download လုပ်ခဲ့တဲ့ path က   
```https://data.statmt.org/romang/ape-wmt16/```  

### Data Format

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16$ tree data
data
├── 4M
│   ├── 4M.mt
│   ├── 4M.pe
│   └── 4M.src
└── 500K
    ├── 500K.mt
    ├── 500K.pe
    └── 500K.src

2 directories, 6 files
```

4M ဖိုလ်ဒါအောက်ကို ဝင်လေ့လာတော့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/data/4M$ wc *
   4391180   69577157  424504643 4M.mt
   4391180   73255351  458692150 4M.pe
   4391180   70841846  372567670 4M.src
  13173540  213674354 1255764463 total
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/data/4M$ head *
==> 4M.mt <==
unscharf maskieren wurde Radius = 6.0 , Betrag = 0.5 und einem Schwellend= * * * * Daphne Duck .
folgende Konstanten werden von dieser Erweiterung definiert und stehen nur zur Verfügung , wenn die Erweiterung entweder statisch in PHP kompiliert oder dynamisch zur Laufzeit geladen wurde .
schauen Sie auf über reguläre Ausdrücke mit einer zu Perl kompatiblen Syntax die PCRE Funktionen fnmatch ( ) bietet die Möglichkeit der Suche mit Platzhalter-Muster Stil . in Shell
dieses Element wird im Dokument nicht auftauchen , bis es mittels DomNode _ append _ child ( ) eingefügt wurde .
für eine Verbindung zwischen dem PHP script und dem DBH erforderlichen Parameter von CNF und NAM der SESAM-Konfiguration der Werte des BS2000 DBH gestartet .
das Verhalten , der Funktionsname und alles Andere was hier dokumentiert ist , kann sich in zukünftigen PHP-Versionen ohne Ankündigung ändern .
eine Kontrolle besteht aus einer oid die die Kontrolle identifiziert , einem wahlweisen wert , und einem wahlweisen Kennzeichen für Criticality .
gibt TRUE zurück ( Datensatz ) oder falsch ( abgerufen wurde keine weiteren Datensätze oder Auftreten eines Fehlers ) .
diese Funktion zerlegt einen Adress-String gemäß RFC822 und liefert ein Array von Objekten mit einem Eintrag je ermittelte Adresse .
in SESAM muss im Kommamdo DROP TABLE der Name entweder um die Schlüsselwörter restrict oder Cascade ergänzt werden .

==> 4M.pe <==
unscharf maskieren wurde mit Radius = 6.0 , Betrag = 0.5 und einem Schwellwert = 0.0 angewandt .
folgende Konstanten werden von dieser Erweiterung definiert und stehen nur zur Verfügung , wenn die Erweiterung entweder statisch in PHP kompiliert oder dynamisch zur Laufzeit geladen wurde .
schauen Sie sich bezüglich regulärer Ausdrücke mit einer zu Perl kompatiblen Syntax die PCRE Funktionen an. fnmatch ( ) bietet die Möglichkeit der Suche nach Übereinstimmungen mit Wildcard-Suchmustern im einfacheren Shell-Stil .
dieses Element wird solange nicht im Dokument auftauchen , bis es mittels DomNode _ append _ child ( ) eingefügt wurde .
für eine Verbindung zwischen dem PHP script und dem DBH müssen die Parameter von CNF und NAM der SESAM-Konfiguration den Werten des im BS2000 gestarteten DBH ensprechen .
das Verhalten , der Funktionsname und alles Andere was hier dokumentiert ist , kann sich in zukünftigen PHP-Versionen ohne Ankündigung ändern .
eine Kontrolle besteht aus einer oid die die Kontrolle identifiziert , einem wahlweisen wert , und einem wahlweisen Kennzeichen für Criticality .
gibt TRUE ( Datensatz wurde abgerufen ) oder FALSE ( keine weiteren Datensätze oder Auftreten eines Fehlers ) zurück .
diese Funktion zerlegt einen Adress-String gemäß RFC822 und liefert ein Array von Objekten mit einem Eintrag je erkannter Adresse .
in SESAM muss im Kommamdo DROP TABLE der Name entweder um die Schlüsselwörter restrict oder Cascade ergänzt werden .

==> 4M.src <==
Unsharp Mask was Radius = 6.0 , Amount = 0.5 , and a threshold = 0.0 .
the constants below are defined by this extension , and will only be available when the extension has either been compiled into PHP or dynamically loaded at runtime .
look at about regular expressions a Perl-compatible syntax using the PCRE functions the fnmatch ( ) offers the possibility of searching with wildcard pattern in simpler shell style .
this node will not show up in the document unless it is inserted with e.g. domnode _ append _ child ( ) .
for a connection between PHP script and the DBH necessary parameters of CNF and NAM SESAM configuration of the values of the BS2000 launched DBH .
the behaviour of this function , the name of this function , and anything else documented about this function may change without notice in a future release of PHP .
a control consists of an oid identifying the control , an optional value , and an optional flag for criticality .
returns TRUE ( record ) or FALSE ( retrieved was no more rows or occurrence of an error ) .
this function ses the address string as defined in RFC2822 and returns an array of objects with a record ever identified address .
in SESAM , in the DROP TABLE command , the table name must be either followed by the keyword restrict or cascade .
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/data/4M$
```

500K ဖိုလ်ဒါအောက်ကိုလည်း ဝင်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/data/500K$ wc *
   526368  10594049  63025735 500K.mt
   526368  11001440  66813242 500K.pe
   526368  10718110  55228230 500K.src
  1579104  32313599 185067207 total
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/data/500K$ head *
==> 500K.mt <==
Unscharf maskieren wurde Radius = 6.0 , Betrag = 0.5 und einem Schwellend= * * * * Daphne Duck .
Für eine Verbindung zwischen dem PHP script und dem DBH erforderlichen Parameter von CNF und NAM der SESAM-Konfiguration der Werte des BS2000 DBH gestartet .
Gibt TRUE zurück ( Datensatz ) oder falsch ( abgerufen wurde keine weiteren Datensätze oder Auftreten eines Fehlers ) .
Nachfolgende Aufrufe von Sesam _ fetch _ array ( ) geben die jeweils nächste Zeile ( oder die vorherige höchsten / niedrigsten je nach den Attributen ) im Ausgabesatz oder FALSE wenn keine Zeilen mehr verfügbar .
Auf der Basis der bestehenden Benutzer von PHP / FI Gebäude , beschlossen ANDi , Rasmus und Zeev zur Kooperation , und kündigten PHP 3.0 als den offiziellen Nachfolger von PHP / FI 2.0 an , und die Entwicklung von PHP / FI 2.0 wurde größtenteils eingestellt .
Sie haben auch beachten sie , dass PHP intern Ganzzahlwerte als unterzeichnet en-Thema deren Umfang Werte von Automatentyp abhängig speichert .
Die LDAP _ get _ entries ( ) Funktion wird verwendet , um mehrere Einträge des Ergebnisses lesen , angegebenen Ergebniskennung zu vereinfachen und erst nach die Merkmale und mehfachen Werte gelesen .
Falls ein zweiter Aufruf von ifx _ connect ( ) mit denselben Verbindungsoptionen erfolgt , wird keine neue Verbindung wird aufgebaut , sondern stattdessen die Verbindungs-Kennung einer schon geöffneten Verbindung .
Dieser Name ist in ihrer Position im Periodensystem begründet , da dort der Übergang durch die aufeinanderfolgende Zunahme von Elektronen in den d-Atomorbital entlang jeder Periode .
Der Datentyp " Number " verwendet diese 52 Bit und ein besonderes verborgenes Bit , um Ganzzahlen im Bereich von -9.007.199.254.740.992 ( -253 ) bis 9.007.199.254.740.992 ( 253 ) .

==> 500K.pe <==
Unscharf maskieren wurde mit Radius = 6.0 , Betrag = 0.5 und einem Schwellwert = 0.0 angewandt .
Für eine Verbindung zwischen dem PHP script und dem DBH müssen die Parameter von CNF und NAM der SESAM-Konfiguration den Werten des im BS2000 gestarteten DBH ensprechen .
Gibt TRUE ( Datensatz wurde abgerufen ) oder FALSE ( keine weiteren Datensätze oder Auftreten eines Fehlers ) zurück .
Nachfolgende Aufrufe von Sesam _ fetch _ array ( ) liefern die nächste Zeile ( oder die vorhergehende , höchste / niedrigste je nach den Attributen ) im Ausgabesatz oder FALSE wenn keine Zeilen mehr verfügabr sind .
Auf die Basis der bestehenden Benutzer von PHP / FI aufbauend , entschieden sich ANDi , Rasmus und Zeev zur Kooperation , und kündigten PHP 3.0 als den offiziellen Nachfolger von PHP / FI 2.0 an , und die Entwicklung von PHP / FI 2.0 wurde größtenteils eingestellt .
Beachten sie auch , dass PHP intern Ganzzahl-Werte als vorzeichen-behaftete Werte speichert , deren Umfang vom Maschinen-Typ abhängig ist .
Die LDAP _ get _ entries ( ) Funktion wird verwendet um das Lesen mehrfacher Einträge des Ergebnisses , angegeben mit Ergebnis-Kennung zu vereinfachen und danach werden die Merkmale und mehfachen Werte gelesen .
Falls ein zweiter Aufruf von ifx _ connect ( ) mit denselben Verbindungsoptionen erfolgt , wird keine neue Verbindung aufgebaut , stattdessen wird die Verbindungskennung der bereits geöffneten Verbindung zurückgegeben .
Dieser Name ist in ihrer Position im Periodensystem begründet , da sich dort der Übergang durch die aufeinanderfolgende Zunahme von Elektronen in den d-Atomorbital entlang jeder Periode zeigt .
Der Datentyp " Number " verwendet diese 52 Bit sowie ein spezielles verborgenes Bit , um Ganzzahlen im Bereich von -9.007.199.254.740.992 ( -253 ) bis 9.007.199.254.740.992 ( 253 ) darzustellen .

==> 500K.src <==
Unsharp Mask was Radius = 6.0 , Amount = 0.5 , and a threshold = 0.0 .
For a connection between PHP script and the DBH necessary parameters of CNF and NAM SESAM configuration of the values of the BS2000 launched DBH .
Returns TRUE ( record ) or FALSE ( retrieved was no more rows or occurrence of an error ) .
Subsequent calls to SESAM _ fetch _ array ( ) would return the next row ( or the previous highest / lowest depending on the attributes ) in the result set , or FALSE if no more rows available .
On the basis of existing users of PHP / FI building , decided ANDi , Rasmus and Zeev to cooperate , and announce PHP 3.0 as the official successor of PHP / FI 2.0 , and development of PHP / FI 2.0 was mostly halted .
They also note that PHP internally integer values as signed en-subject whose scope stores values by machine type addicted .
The LDAP _ get _ entries ( ) function is used to read multiple entries of the result , with specified result identifier to simplify and only after reading the attributes and multiple values .
If a second call made to ifx _ connect ( ) with the same arguments , no new link will be established , but instead , the link identifier of the already opened link .
This name is in its position on the periodic table justified since there the transition through the successive increase of electrons in atomic oride-ital along each period .
The Number data type uses these 52 bits and a special hidden bit to integers : The range is -9,007,199,254,740,992 ( -253 ) to 9,007,199,254,740,992 ( 253 ) .
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/data/500K$
```

### system/

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16$ tree system
system
├── data
│   ├── de.bpe
│   ├── en.bpe
│   ├── true.de
│   └── true.en
├── Makefile
├── models
│   ├── configs
│   │   ├── mt-pe.ensemble4.tuned.yml
│   │   ├── mtsrc-pe.ensemble.ape.tuned.yml
│   │   └── src-pe.ensemble4.yml
│   ├── mt-pe
│   │   ├── model.iter260000.npz
│   │   ├── model.iter270000.npz
│   │   ├── model.iter280000.npz
│   │   ├── model.iter290000.npz
│   │   ├── vocab.mt.json
│   │   └── vocab.pe.json
│   └── src-pe
│       ├── model.iter340000.npz
│       ├── model.iter350000.npz
│       ├── model.iter360000.npz
│       ├── model.iter370000.npz
│       ├── vocab.pe.json
│       └── vocab.src.json
├── scripts
│   ├── apply_bpe.py
│   ├── deescape-special-chars.perl
│   ├── detruecase.perl
│   ├── escape-special-chars.perl
│   ├── prepare_submission.py
│   ├── truecase.perl
│   └── unproc.sh
└── test
    ├── test.mt
    └── test.src

7 directories, 29 files
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16$
```

### Configuration Files

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/system/models/configs$ ll
total 2560
drwxr-xr-x 2 ye ye 524288 ဩ    29  2016 ./
drwxr-xr-x 5 ye ye 524288 ဩ    30  2016 ../
-rwxr-xr-x 1 ye ye    551 မေ    2  2016 mt-pe.ensemble4.tuned.yml*
-rwxr-xr-x 1 ye ye   2500 မေ    3  2016 mtsrc-pe.ensemble.ape.tuned.yml*
-rwxr-xr-x 1 ye ye    546 မေ    2  2016 src-pe.ensemble4.yml*
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/system/models/configs$ cat ./mt-pe.ensemble4.tuned.yml 
# amunn connfig file

relative-paths: yes

# Scorer configuration
scorers:
  F0:
    type: Nematus
    path: ../mt-pe/model.iter260000.npz
  F1:
    type: Nematus
    path: ../mt-pe/model.iter270000.npz
  F2:
    type: Nematus
    path: ../mt-pe/model.iter280000.npz
  F3:
    type: Nematus
    path: ../mt-pe/model.iter290000.npz

source-vocab: ../mt-pe/vocab.mt.json
target-vocab: ../mt-pe/vocab.pe.json

weights:
  F0: 0.3663
  F1: 0.3318
  F2: 0.1629
  F3: 0.1389

beam-size: 12
normalize: yes
n-best: no

devices: [0, 1, 2]
threads-per-device: 1
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/system/models/configs$ cat ./mtsrc-pe.ensemble.ape.tuned.yml 
# amunn config file

relative-paths: yes

# Scorer configuration
scorers:
  F0:
    type: Nematus                                                                          
    path: ../mt-pe/model.iter260000.npz                                                    
  F1:
    type: Nematus                                                                          
    path: ../mt-pe/model.iter270000.npz                                                    
  F2:                                                                                      
    type: Nematus                                                                          
    path: ../mt-pe/model.iter280000.npz                                                    
  F3:                                                                                      
    type: Nematus                                                                          
    path: ../mt-pe/model.iter290000.npz  
  F4:                                                                                      
    type: Nematus                                                                          
    path: ../src-pe/model.iter340000.npz                                                   
    tab: 1
  F5:                                                                                      
    type: Nematus                                                                          
    path: ../src-pe/model.iter350000.npz                                                   
    tab: 1
  F6:                                                                                      
    type: Nematus                                                                          
    path: ../src-pe/model.iter360000.npz                                                   
    tab: 1
  F7:                                                                                      
    type: Nematus                                                                          
    path: ../src-pe/model.iter370000.npz   
    tab: 1
  F8:
    type: APE

source-vocab:
  - ../mt-pe/vocab.mt.json
  - ../src-pe/vocab.src.json
target-vocab: ../mt-pe/vocab.pe.json

weights:
  F0: 0.0679875234050288
  F1: 0.136272622440232
  F2: 0.0447424881348462
  F3: 0.0505810091549122
  F4: 0.119029214497868
  F5: -0.0291262004966649
  F6: -0.0348248568202612
  F7: 0.131424048800743
  F8: 0.386012036249443

beam-size: 12
normalize: yes
n-best: no

devices: [0, 1, 2]
threads-per-device: 1
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/system/models/configs$ cat src-pe.ensemble4.yml 
# amunn connfig file

relative-paths: yes

# Scorer configuration
scorers:
  F0:
    type: Nematus
    path: ../src-pe/model.iter340000.npz
  F1:
    type: Nematus
    path: ../src-pe/model.iter350000.npz
  F2:
    type: Nematus
    path: ../src-pe/model.iter360000.npz
  F3:
    type: Nematus
    path: ../src-pe/model.iter370000.npz

source-vocab: ../src-pe/vocab.src.json
target-vocab: ../src-pe/vocab.pe.json

weights:
  F0: 1.0
  F1: 1.0
  F2: 1.0
  F3: 1.0

beam-size: 12
normalize: yes
n-best: no

devices: [0, 1, 2]
threads-per-device: 1
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/system/models/configs$
```

အထက်ပါ configuration ဖိုင်တွေကို ကြည့်ပြီး ငါနားလည်တာက model တွေကို ensemble လုပ်ထားတာလို့...  

နောက်ထပ် ```https://data.statmt.org/romang/ape-explore/``` အောက်က train.tgz ဖိုင်ကိုလည်း ကိုယ့် local path ```ape-explore/``` အောက်ကို download လုပ်ပြီး configuration file နဲ့ ပတ်သက်ပြီး လေ့လာခဲ့တယ်။ m-cgru.yml ဖိုင်ကတော့ အောက်ပါအတိုင်း ```multi-s2s``` ကို သုံးထားတာ တွေ့ရတယ် ...    

```
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/ape-explore/train/config$ cat ./m-cgru.yml 
devices:
  - 0
  - 1
  - 2
  - 3
dim-emb: 512
dim-rnn: 1024
dim-vocabs:
  - 40329
  - 40329
  - 40329
disp-freq: 1000
dropout-rnn: 0.2
dropout-src: 0.2
dropout-trg: 0.2
dynamic-batching: true
early-stopping: 10
layer-normalization: true
learn-rate: 0.0001
max-length: 50
maxi-batch: 100
mini-batch: 64
mini-batch-words: 0
model: m-cgru/model.npz
moving-average: true
moving-decay: 0.9999
save-freq: 10000
seed: 0
train-sets:
  - train.ape2016.mt
  - train.ape2016.src
  - train.ape2016.pe
type: multi-s2s
valid-freq: 10000
valid-metrics:
  - cross-entropy
  - valid-script
valid-script-path: ./m-cgru/validate.sh
valid-sets:
  - dev.mt
  - dev.src
  - dev.pe
valid-log: m-cgru/valid.log
log: m-cgru/train.log
vocabs:
  - vocab.mt-pe.step
  - vocab.src
  - vocab.mt-pe.step
workspace: 4000
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/ape-explore/train/config$
```

running scripts တွေကိုလည်း လေ့လာကြည့်တော့ အောက်ပါအတိုင်း တွေ့ရ...  

```bash
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/ape-explore/train/m-cgru$ cat ./validate_avg.sh 
#!/bin/bash -v

python ../marian/scripts/average.py -m `grep valid m-cgru/valid.log | sort -r -k8,8 | cut -f 4 -d ' ' | xargs -I{} echo "model.iter{}.npz" | head -n 8 | xargs` -o m-cgru/model.avg.npz

# decode
../marian/build/s2s -m m-cgru/model.avg.npz -v vocab.mt-pe.step vocab.src vocab.mt-pe.step -b 5 -w 500 -d 0 1 2 3 -i test.mt test.src \
 | perl -pe 's/<step>//g; s/  / /g' 2>/dev/null \
 | perl -pe 's/@@ //g' 2>/dev/null \
 | ../mosesdecoder/scripts/tokenizer/deescape-special-chars.perl 2>/dev/null \
 | ../mosesdecoder/scripts/recaser/detruecase.perl 2>/dev/null > test.output

../mosesdecoder/bin/evaluator --sctype TER --reference <(cut -f 1 apewmt16.test.pe+mt+src) --candidate test.output 2>/dev/null
eval/runTER.py -s test.output -r test.pe.ref
```

```bash
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/ape-explore/train/m-cgru$ cat ./validate.sh 
#!/bin/bash

# decode
../marian/build/s2s -m m-cgru/model.npz -i dev.mt dev.src -v vocab.mt-pe.step vocab.src vocab.mt-pe.step -b 5 -w 500 -d 0 1 2 3 2>/dev/null \
 | perl -pe 's/<step>//g; s/  / /g' 2>/dev/null \
 | perl -pe 's/@@ //g' 2>/dev/null \
 | ./moses-scripts/scripts/tokenizer/deescape-special-chars.perl 2>/dev/null \
 | ./moses-scripts/scripts/recaser/detruecase.perl 2>/dev/null > dev.output

../mosesdecoder/bin/evaluator --sctype TER --reference dev.pe.ref --candidate dev.output 2>/dev/null
```

```bash
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/ape-explore/train/m-cgru$ cat ./validate_test.sh 
#!/bin/bash

# decode
../marian/build/s2s -m m-cgru/model.npz -i test.mt test.src -v vocab.mt-pe.step vocab.src vocab.mt-pe.step -b 5 -w 500 -d 0 1 2 3 \
 | perl -pe 's/<step>//g; s/  / /g' 2>/dev/null \
 | perl -pe 's/@@ //g' 2>/dev/null \
 | ./moses-scripts/scripts/tokenizer/deescape-special-chars.perl 2>/dev/null \
 | ./moses-scripts/scripts/recaser/detruecase.perl 2>/dev/null > test.output

../mosesdecoder/bin/evaluator --sctype TER --reference test.pe.ref --candidate test.output 2>/dev/null
(base) ye@:/media/ye/project2/exp/braille-nmt/ape-wmt16/ape-explore/train/m-cgru$
```

```https://data.statmt.org/wmt17_systems/training/scripts.tensorflow/train.sh``` က အောက်ပါအတိုင်း...  
(ဒီ script ကတော့ PE နဲ့ မဆိုင်ဘူး, အစောပိုင်း framework ဖြစ်တဲ့ nematus ကို သုံးထားတဲ့ပုံရှိတယ်)  

```bash
#!/bin/sh
# Distributed under MIT license

script_dir=`dirname $0`
main_dir=$script_dir/../
data_dir=$main_dir/data
working_dir=$main_dir/model

#language-independent variables (toolkit locations)
. $main_dir/../vars

#language-dependent variables (source and target language)
. $main_dir/vars

CUDA_VISIBLE_DEVICES=$device python $nematus_home/nematus/train.py \
    --model $working_dir/model \
    --datasets $data_dir/corpus.bpe.$src $data_dir/corpus.bpe.$trg \
    --valid_datasets $data_dir/newstest2013.bpe.$src $data_dir/newstest2013.bpe.$trg \
    --dictionaries $data_dir/corpus.bpe.$src.json $data_dir/corpus.bpe.$trg.json \
    --valid_script $script_dir/validate.sh \
    --reload latest_checkpoint \
    --dim_word 512 \
    --dim 1024 \
    --lrate 0.0001 \
    --optimizer adam \
    --maxlen 50 \
    --batch_size 80 \
    --valid_batch_size 40 \
    --validFreq 10000 \
    --dispFreq 1000 \
    --saveFreq 30000 \
    --sampleFreq 10000 \
    --tie_decoder_embeddings \
    --layer_normalisation \
    --dec_base_recurrence_transition_depth 8 \
    --enc_recurrence_transition_depth 4

```

## Re-Explore Marian Examples

```/home/ye/tool/marian/examples/transformer``` အောက်က README.md ထဲက Google Transformer Architecture နဲ့ ပတ်သက်ပြီး ရှင်းပြထားတဲ့ တစိတ်တပိုင်းက အောက်ပါအတိုင်း...  

Files and scripts in this folder show how to train a Google-style transformer 
model ([Vaswani et al, 2017](https://arxiv.org/abs/1706.03762)) on WMT-17 (?)
English-German data.
The problem set has created following the example from the original
[tensor2tensor](https://github.com/tensorflow/tensor2tensor) repository by
Google. It uses 32,000 common BPE units for both languages. 

Assuming four GPUs are available (here 0 1 2 3), execute the command below
to run the complete example:

```
./run-me.sh 0 1 2 3
```

This starts a training run with `marian` using the following command:

```
../build/marian \
    --model model/model.npz --type transformer \
    --train-sets data/corpus.bpe.en data/corpus.bpe.de \
    --max-length 100 \
    --vocabs model/vocab.ende.yml model/vocab.ende.yml \
    --mini-batch-fit -w 10000 --maxi-batch 1000 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity translation \
    --valid-sets data/valid.bpe.en data/valid.bpe.de \
    --valid-script-path ./scripts/validate.sh \
    --valid-translation-output data/valid.bpe.en.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log model/train.log --valid-log model/valid.log \
    --enc-depth 6 --dec-depth 6 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.1 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 16000 --lr-decay-inv-sqrt 16000 --lr-report \
    --optimizer-params 0.9 0.98 1e-09 --clip-norm 5 \
    --tied-embeddings-all \
    --devices $GPUS --sync-sgd --seed 1111 \
    --exponential-smoothing
```

Example တွေ အကုန်ကို ပြန်ကြည့်ခဲ့ပေမဲ့ multi-source အတွက် configuration ဖိုင်က မပါဘူး။ အဲဒါနဲ့ multi-source POS တုန်းက လုပ်ခဲ့တဲ့ experiment ကိုပဲ ပြန်အခြေခံပြီး my-br အတွက် post-editing NMT ကို လုပ်ကြည့်ဖို့ ဆုံးဖြတ်ခဲ့တယ်။  

## Configuration File for {my,mt}-->{br}

bash script ကို အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်။  
multi-transformer-pe-mymt2br.sh ဆိုတဲ့ နာမည်နဲ့ သိမ်းခဲ့တယ်။  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Transformer MT_Braille-to-Ref_Braille
## 15 April 2022

# ဘာတွေထပ်ဖြည့်ခဲ့သလဲ ဆိုရင်
# running folder နာမည် ပြောင်းပြီး
# --type multi-transformer
# --train-sets မှာ {source,mt,target} ထား
# --vocabs မှာလည်း {source,mt,target} ပေးခဲ့
# --valid-sets မှာလည်း {source,mt,target} ပေးခဲ့
  

mkdir model.transformer-multi-mybr;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.npz --type multi-transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my /media/ye/project2/exp/braille-nmt/model.transformer/hyp.iter95000-trainingdata.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my /media/ye/project2/exp/braille-nmt/model.transformer/hyp.iter95000-devdata.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/dev.multi-mybr.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ./model.transformer-multi-mybr/train-multi-mybr.log --valid-log ./model.transformer-multi-mybr/valid-multi-mybr.log \
    --enc-depth 2 --dec-depth 2 \
    --transformer-heads 8 \
    --transformer-postprocess-emb d \
    --transformer-postprocess dan \
    --transformer-dropout 0.3 --label-smoothing 0.1 \
    --learn-rate 0.0003 --lr-warmup 0 --lr-decay-inv-sqrt 16000 --lr-report \
    --clip-norm 5 \
    --tied-embeddings \
    --devices 0 1 --sync-sgd --seed 1111 \
    --exponential-smoothing \
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/config-multi-mybr0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/config-multi-mybr0.yml  2>&1 | tee transformer-multi-mybr0.log

```

## Training {my,mt}-->{br}


Training စလုပ်ပြီး GPU usage က အောက်ပါအတိုင်း...  

<br />

<p align="center">
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/multi-source/multi-transformer-mymt2br-gpu-usage.png" alt="multi-source GPU usage" width="800"/>  
</p>  
<div align="center">
  Fig.1 GPU usage of multi-source NMT training for {my,mt} to {br} translation <br />  
</div> 

<br />

training ကြာချိန်က အောက်ပါအတိုင်း...  

```

```


