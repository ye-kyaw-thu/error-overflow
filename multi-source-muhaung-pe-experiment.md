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

### Configuration File

```

```