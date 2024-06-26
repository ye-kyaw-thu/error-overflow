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
<img src="https://github.com/ye-kyaw-thu/error-overflow/blob/master/fig/multi-source/multi-transformer-mymt2br-gpu-usage2.png" alt="multi-source GPU usage" width="600"/>  
</p>  
<div align="center">
  Fig.1 GPU usage of multi-source NMT training for {my,mt} to {br} translation <br />  
</div> 

<br />

training ကြာချိန်က အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./multi-transformer-pe-mymt2br.sh
...
...
...
[2022-04-15 22:36:41] [data] Done reading 16,415 sentences
[2022-04-15 22:36:41] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:37:27] Seen 16415 samples
[2022-04-15 22:37:27] Starting data epoch 525 in logical epoch 525
[2022-04-15 22:37:27] [data] Shuffling data
[2022-04-15 22:37:27] [data] Done reading 16,415 sentences
[2022-04-15 22:37:27] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:37:32] Ep. 525 : Up. 52500 : Sen. 2,058 : Cost 1.32761872 * 1,177,746 @ 2,941 after 123,989,361 : Time 229.56s : 5130.37 words/s : L.r. 1.6562e-04
[2022-04-15 22:38:13] Seen 16415 samples
[2022-04-15 22:38:13] Starting data epoch 526 in logical epoch 526
[2022-04-15 22:38:13] [data] Shuffling data
[2022-04-15 22:38:13] [data] Done reading 16,415 sentences
[2022-04-15 22:38:13] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:38:59] Seen 16415 samples
[2022-04-15 22:38:59] Starting data epoch 527 in logical epoch 527
[2022-04-15 22:38:59] [data] Shuffling data
[2022-04-15 22:38:59] [data] Done reading 16,415 sentences
[2022-04-15 22:38:59] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:39:46] Seen 16415 samples
[2022-04-15 22:39:46] Starting data epoch 528 in logical epoch 528
[2022-04-15 22:39:46] [data] Shuffling data
[2022-04-15 22:39:46] [data] Done reading 16,415 sentences
[2022-04-15 22:39:46] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:40:32] Seen 16415 samples
[2022-04-15 22:40:32] Starting data epoch 529 in logical epoch 529
[2022-04-15 22:40:32] [data] Shuffling data
[2022-04-15 22:40:32] [data] Done reading 16,415 sentences
[2022-04-15 22:40:32] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:41:18] Seen 16415 samples
[2022-04-15 22:41:18] Starting data epoch 530 in logical epoch 530
[2022-04-15 22:41:18] [data] Shuffling data
[2022-04-15 22:41:18] [data] Done reading 16,415 sentences
[2022-04-15 22:41:18] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:41:22] Ep. 530 : Up. 53000 : Sen. 1,048 : Cost 1.32687318 * 1,175,216 @ 1,798 after 125,164,577 : Time 229.88s : 5112.40 words/s : L.r. 1.6483e-04
[2022-04-15 22:42:04] Seen 16415 samples
[2022-04-15 22:42:04] Starting data epoch 531 in logical epoch 531
[2022-04-15 22:42:04] [data] Shuffling data
[2022-04-15 22:42:04] [data] Done reading 16,415 sentences
[2022-04-15 22:42:04] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:42:49] Seen 16415 samples
[2022-04-15 22:42:49] Starting data epoch 532 in logical epoch 532
[2022-04-15 22:42:49] [data] Shuffling data
[2022-04-15 22:42:49] [data] Done reading 16,415 sentences
[2022-04-15 22:42:50] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:43:35] Seen 16415 samples
[2022-04-15 22:43:35] Starting data epoch 533 in logical epoch 533
[2022-04-15 22:43:35] [data] Shuffling data
[2022-04-15 22:43:35] [data] Done reading 16,415 sentences
[2022-04-15 22:43:35] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:44:21] Seen 16415 samples
[2022-04-15 22:44:21] Starting data epoch 534 in logical epoch 534
[2022-04-15 22:44:21] [data] Shuffling data
[2022-04-15 22:44:21] [data] Done reading 16,415 sentences
[2022-04-15 22:44:21] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:45:08] Seen 16415 samples
[2022-04-15 22:45:08] Starting data epoch 535 in logical epoch 535
[2022-04-15 22:45:08] [data] Shuffling data
[2022-04-15 22:45:08] [data] Done reading 16,415 sentences
[2022-04-15 22:45:08] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:45:11] Ep. 535 : Up. 53500 : Sen. 1,304 : Cost 1.32661808 * 1,181,885 @ 2,911 after 126,346,462 : Time 229.29s : 5154.59 words/s : L.r. 1.6406e-04
[2022-04-15 22:45:54] Seen 16415 samples
[2022-04-15 22:45:54] Starting data epoch 536 in logical epoch 536
[2022-04-15 22:45:54] [data] Shuffling data
[2022-04-15 22:45:54] [data] Done reading 16,415 sentences
[2022-04-15 22:45:54] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:46:39] Seen 16415 samples
[2022-04-15 22:46:39] Starting data epoch 537 in logical epoch 537
[2022-04-15 22:46:39] [data] Shuffling data
[2022-04-15 22:46:39] [data] Done reading 16,415 sentences
[2022-04-15 22:46:39] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:47:25] Seen 16415 samples
[2022-04-15 22:47:25] Starting data epoch 538 in logical epoch 538
[2022-04-15 22:47:25] [data] Shuffling data
[2022-04-15 22:47:25] [data] Done reading 16,415 sentences
[2022-04-15 22:47:25] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:48:12] Seen 16415 samples
[2022-04-15 22:48:12] Starting data epoch 539 in logical epoch 539
[2022-04-15 22:48:12] [data] Shuffling data
[2022-04-15 22:48:12] [data] Done reading 16,415 sentences
[2022-04-15 22:48:12] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:48:59] Seen 16415 samples
[2022-04-15 22:48:59] Starting data epoch 540 in logical epoch 540
[2022-04-15 22:48:59] [data] Shuffling data
[2022-04-15 22:48:59] [data] Done reading 16,415 sentences
[2022-04-15 22:48:59] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:49:02] Ep. 540 : Up. 54000 : Sen. 714 : Cost 1.32687712 * 1,178,692 @ 2,544 after 127,525,154 : Time 230.90s : 5104.69 words/s : L.r. 1.6330e-04
[2022-04-15 22:49:46] Seen 16415 samples
[2022-04-15 22:49:46] Starting data epoch 541 in logical epoch 541
[2022-04-15 22:49:46] [data] Shuffling data
[2022-04-15 22:49:46] [data] Done reading 16,415 sentences
[2022-04-15 22:49:46] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:50:32] Seen 16415 samples
[2022-04-15 22:50:32] Starting data epoch 542 in logical epoch 542
[2022-04-15 22:50:32] [data] Shuffling data
[2022-04-15 22:50:32] [data] Done reading 16,415 sentences
[2022-04-15 22:50:32] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:51:17] Seen 16415 samples
[2022-04-15 22:51:17] Starting data epoch 543 in logical epoch 543
[2022-04-15 22:51:17] [data] Shuffling data
[2022-04-15 22:51:17] [data] Done reading 16,415 sentences
[2022-04-15 22:51:17] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:52:03] Seen 16415 samples
[2022-04-15 22:52:03] Starting data epoch 544 in logical epoch 544
[2022-04-15 22:52:03] [data] Shuffling data
[2022-04-15 22:52:03] [data] Done reading 16,415 sentences
[2022-04-15 22:52:03] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:52:50] Seen 16415 samples
[2022-04-15 22:52:50] Starting data epoch 545 in logical epoch 545
[2022-04-15 22:52:50] [data] Shuffling data
[2022-04-15 22:52:50] [data] Done reading 16,415 sentences
[2022-04-15 22:52:50] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:52:52] Ep. 545 : Up. 54500 : Sen. 692 : Cost 1.32661784 * 1,180,441 @ 2,315 after 128,705,595 : Time 229.76s : 5137.75 words/s : L.r. 1.6255e-04
[2022-04-15 22:53:36] Seen 16415 samples
[2022-04-15 22:53:36] Starting data epoch 546 in logical epoch 546
[2022-04-15 22:53:36] [data] Shuffling data
[2022-04-15 22:53:36] [data] Done reading 16,415 sentences
[2022-04-15 22:53:36] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:54:22] Seen 16415 samples
[2022-04-15 22:54:22] Starting data epoch 547 in logical epoch 547
[2022-04-15 22:54:22] [data] Shuffling data
[2022-04-15 22:54:22] [data] Done reading 16,415 sentences
[2022-04-15 22:54:22] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:55:08] Seen 16415 samples
[2022-04-15 22:55:08] Starting data epoch 548 in logical epoch 548
[2022-04-15 22:55:08] [data] Shuffling data
[2022-04-15 22:55:08] [data] Done reading 16,415 sentences
[2022-04-15 22:55:08] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:55:54] Seen 16415 samples
[2022-04-15 22:55:54] Starting data epoch 549 in logical epoch 549
[2022-04-15 22:55:54] [data] Shuffling data
[2022-04-15 22:55:54] [data] Done reading 16,415 sentences
[2022-04-15 22:55:54] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:56:39] Seen 16415 samples
[2022-04-15 22:56:39] Starting data epoch 550 in logical epoch 550
[2022-04-15 22:56:39] [data] Shuffling data
[2022-04-15 22:56:39] [data] Done reading 16,415 sentences
[2022-04-15 22:56:39] [data] Done shuffling 16,415 sentences to temp files
[2022-04-15 22:56:40] Ep. 550 : Up. 55000 : Sen. 182 : Cost 1.32673931 * 1,176,225 @ 1,800 after 129,881,820 : Time 228.60s : 5145.42 words/s : L.r. 1.6181e-04
[2022-04-15 22:56:40] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.npz.orig.npz
[2022-04-15 22:56:41] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.iter55000.npz
[2022-04-15 22:56:41] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.npz
[2022-04-15 22:56:43] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.npz.optimizer.npz
[2022-04-15 22:56:51] [valid] Ep. 550 : Up. 55000 : cross-entropy : 11.0185 : stalled 10 times (last best: 10.0522)
[2022-04-15 22:56:53] [valid] Ep. 550 : Up. 55000 : perplexity : 2.13672 : stalled 10 times (last best: 1.99908)
[2022-04-15 22:57:11] [valid] Ep. 550 : Up. 55000 : bleu : 86.454 : new best
[2022-04-15 22:57:11] Training finished
[2022-04-15 22:57:12] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.npz.orig.npz
[2022-04-15 22:57:13] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.npz
[2022-04-15 22:57:14] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr/model0-mtbr.npz.optimizer.npz

real	429m5.282s
user	696m1.927s
sys	0m49.689s
```

## Testing and Evaluation for {my,mt_br}-->{br}

--input option ကို နှစ်ခု ပေးမှ translation လုပ်လို့ ရလိမ့်မယ်။   

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung PE
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Transformer multi PE Model
## 15 April 2022

#model0-mtbr.iter10000.npz

for i in {5000..55000..5000}
do
   marian-decoder -m ./model0-mtbr.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter$i.br --input  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my --input ../model.transformer/hyp.iter95000.br
   echo "Evaluation on ./model0-mtbr.iter${i}.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:" >> test0-multi-PE-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br < ./hyp.iter$i.br  >> test0-multi-PE-results.txt
done
```

testing/evaluation ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr$ time ./tran-eval-multi.sh | tee tran-eval-multi.log
...
...
...
[2022-04-15 23:47:46] Best translation 2125 : ⠅⠣⠞⠞⠪⠏⠁ ⠗ ⠲
[2022-04-15 23:47:46] Best translation 2126 : ⠾⠋⠍⠁ ⠃⠥⠂⠗⠔ ⠏⠁ ⠞⠍ ⠹⠻⠆⠣⠨⠁ ⠞⠺ ⠇⠆ ⠩⠺⠱ ⠈⠪⠆⠿⠓⠥ ⠹⠣⠃⠻⠆ ⠙ ⠒ ⠥⠆⠃⠣⠷⠶ ⠗ ⠸⠣⠢⠂ ⠹⠣⠇⠕ ⠓⠥⠯ ⠰⠣⠣⠞⠞⠋⠆⠞⠔ ⠨⠮⠂ ⠹ ⠲
[2022-04-15 23:47:46] Best translation 2127 : ⠨⠺⠱ ⠝⠱⠅⠃⠋⠗⠺⠁ ⠨⠺⠱⠆ ⠲
[2022-04-15 23:47:46] Best translation 2128 : ⠥⠆⠊ ⠹ ⠣⠍⠣⠗⠣⠏⠥⠗⠣ ⠾⠕⠂ ⠾⠴⠯ ⠰⠣⠣ ⠏⠕⠆ ⠁⠮ ⠒ ⠡⠪ ⠁⠮ ⠚ ⠅ ⠣⠗⠶⠆⠣⠺⠮ ⠿⠥⠂ ⠹⠻⠆ ⠏⠕⠆ ⠾⠔⠆⠹⠁⠆⠯ ⠭⠗⠁ ⠏⠭⠎⠪⠆ ⠦⠎⠁ ⠟⠺⠮⠺⠣ ⠡⠋⠆⠹⠁ ⠹ ⠲
[2022-04-15 23:47:46] Best translation 2129 : ⠨⠑⠈⠭ ⠣⠘⠺⠔⠂ ⠲
[2022-04-15 23:47:46] Best translation 2130 : ⠼⠉ ⠲ ⠘⠺⠁ ⠗⠣ ⠗⠁ ⠰⠶ ⠎⠥⠂⠎⠪⠆ ⠡ ⠋ ⠩ ⠒ ⠅⠺⠮⠆ ⠿⠓⠁ ⠁⠺⠑ ⠑ ⠲
[2022-04-15 23:47:46] Best translation 2131 : ⠍⠊⠍⠊ ⠅⠕⠞⠖ ⠣⠹⠋⠝⠱⠣⠹⠋⠞⠓⠁⠆ ⠿⠓ ⠗⠥⠞⠈⠕ ⠇⠱⠂⠟⠔⠂ ⠏ ⠲
[2022-04-15 23:47:46] Best translation 2132 : ⠶ ⠨⠣ ⠶ ⠞⠭⠥⠂⠞⠥⠂ ⠸ ⠤⠤⠤⠤⠤⠤ ⠎⠪ ⠟⠁⠾⠔⠂ ⠏ ⠹ ⠲
[2022-04-15 23:47:46] Best translation 2133 : ⠷⠶⠏⠔⠹⠁⠗⠺⠁ ⠿⠓⠥⠆ ⠾⠕⠂⠝⠮ ⠼⠁ ⠉ ⠙ ⠑ ⠨⠥⠂ ⠒ ⠞⠋⠨⠥⠆ ⠇⠣⠈⠋⠆ ⠼⠁ ⠗⠑ ⠹⠥⠌⠮⠡⠔⠆ ⠗⠪⠞⠥ ⠹⠥⠌⠮⠡⠔⠆ ⠁⠋⠙ ⠅⠕⠂⠁⠆⠅⠕⠅⠕⠆ ⠎⠁⠗⠱⠆⠇⠬ ⠏ ⠹ ⠲
[2022-04-15 23:47:46] Best translation 2134 : ⠼⠓ ⠲ ⠁⠆⠹⠋ ⠰⠶ ⠋ ⠗⠣ ⠋ ⠝⠱ ⠋ ⠭ ⠋ ⠝⠱ ⠁⠆⠁⠦ ⠟⠕⠆⠏⠋⠆ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2135 : ⠿⠁⠆⠗⠪ ⠹⠁ ⠈⠶⠽⠥ ⠟⠣ ⠡⠱ ⠓ ⠈⠕⠯ ⠿⠁⠆⠗⠪ ⠅ ⠈⠶⠽⠥ ⠎ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠫ ⠣⠏⠴⠺⠣ ⠠⠣⠭ ⠘⠑ ⠅ ⠇⠢⠆⠹⠦ ⠿⠪⠆ ⠰⠣⠣ ⠝⠥⠆⠷⠋⠂ ⠹⠢⠍⠺⠱⠂ ⠸⠣⠣⠎ ⠹⠻⠆ ⠅⠋⠃⠣⠇⠁ ⠡⠪ ⠟⠕⠆ ⠅ ⠟⠭ ⠿⠪⠆⠸ ⠼ ⠅⠋⠃⠣⠇⠁ ⠟⠕⠆ ⠎⠣ ⠫ ⠿⠁⠆⠗⠪ ⠿⠓ ⠿⠁⠆⠏⠊⠞⠉⠆ ⠟⠕⠆ ⠎⠣ ⠅ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠏⠴ ⠺⠣ ⠟⠕⠆ ⠓⠶⠆ ⠎⠣ ⠞⠭⠘⠑ ⠗ ⠎⠔⠆⠌⠮ ⠿⠪⠆ ⠎⠔⠆⠌⠮ ⠿⠪⠆ ⠹⠺⠔⠆⠯ ⠞⠓⠁⠆ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠺⠣ ⠅⠣ ⠒ ⠏⠕⠆⠗⠺⠣ ⠅⠣ ⠒ ⠏⠦⠓⠶ ⠎⠁⠆⠹⠴ ⠡ ⠓⠌⠁ ⠚ ⠅ ⠣⠿⠓⠣⠞ ⠡⠪ ⠎ ⠑ ⠓⠌⠁ ⠲
[2022-04-15 23:47:47] Best translation 2136 : ⠟⠞⠚ ⠗ ⠗⠔⠆⠠⠣⠪⠆ ⠹⠻⠆ ⠣⠟⠣⠽ ⠏⠔ ⠭ ⠇⠔⠂ ⠅⠣⠎⠁⠆ ⠒ ⠟⠞⠚ ⠋⠸⠣⠣⠹⠥ ⠰⠣⠣ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠞⠚ ⠟⠪⠂⠾⠔ ⠨⠋⠎⠁⠆ ⠹⠣⠇⠕ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠶⠆ ⠿⠁⠞⠁ ⠟⠪⠆ ⠊ ⠇⠑⠈⠭ ⠰⠣⠣ ⠗⠱⠆ ⠗⠣ ⠍ ⠲
[2022-04-15 23:47:47] Best translation 2137 : ⠎⠣⠅⠁⠆⠇⠉⠆ ⠅⠣⠇⠱⠆ ⠞⠺⠱ ⠎⠪ ⠅⠁ ⠗⠮ ⠗⠥⠞⠈⠕ ⠗⠱⠆ ⠟⠪⠂ ⠍⠮ ⠲
[2022-04-15 23:47:47] Best translation 2138 : ⠍⠣⠾⠣⠗⠔ ⠚ ⠣⠷⠢⠂ ⠅⠣ ⠹⠂ ⠨⠱⠞⠄ ⠅⠣ ⠣⠏⠽⠄ ⠋ ⠏⠻ ⠹⠱⠆ ⠏ ⠣⠷⠢⠂ ⠍⠔⠆⠹⠣⠍⠪⠆⠾ ⠹ ⠏⠺⠮⠆⠨⠔⠆ ⠅ ⠏⠴ ⠶ ⠍⠊⠍⠊ ⠊ ⠏⠔⠅ ⠣⠹⠋ ⠗ ⠟⠕⠆⠎⠁⠆⠯ ⠈⠕ ⠟ ⠗⠣ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2139 : ⠰⠣⠪⠷⠋⠆⠿⠥⠂ ⠺⠥⠞⠁⠥⠂⠾ ⠒ ⠃⠁⠹⠁⠿⠋ ⠺⠥⠞⠁⠥⠂⠾ ⠭⠞⠮ ⠗⠁ ⠎⠱⠅⠁⠮⠆ ⠒ ⠌⠁⠆⠾⠭⠡⠔⠆ ⠒ ⠥⠆⠃⠣⠷⠶ ⠒ ⠅⠥⠆⠞⠕⠂ ⠒ ⠺⠁⠆⠘⠣⠞ ⠒ ⠝⠁⠆⠇⠪ ⠒ ⠗⠮⠆⠗⠮⠆⠺⠔⠝⠂⠺⠔⠂ ⠎⠣⠹ ⠚ ⠰⠣⠁ ⠁⠔⠩⠁⠆ ⠹⠻⠆ ⠺⠥⠞⠁⠥⠂⠾ ⠭ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2140 : ⠩⠱⠆⠨⠭ ⠎⠭⠹⠪ ⠞⠭ ⠥⠆ ⠊ ⠃⠣⠺⠣ ⠞⠭ ⠎⠱⠅ ⠞⠭ ⠏⠖⠆ ⠅ ⠁⠔⠓⠣⠞ ⠹⠻⠆ ⠖⠆⠡⠔⠆ ⠭ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2141 : ⠇⠱⠅⠿⠁ ⠞⠺ ⠇⠆ ⠣⠡⠁⠆ ⠹⠻⠆ ⠓⠌⠑⠾ ⠅⠹ ⠥⠆⠨⠶⠆ ⠏⠖⠆ ⠒ ⠗⠔ ⠏⠖⠆ ⠒ ⠺⠋⠆⠃⠬ ⠏⠖⠆ ⠓⠥⠯ ⠩ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2142 : ⠅⠁⠞⠥⠝⠆ ⠈⠣⠗⠁⠟⠪⠆ ⠥⠆⠃⠣⠚⠋⠆ ⠲
[2022-04-15 23:47:47] Best translation 2143 : ⠵⠣⠾⠔⠆⠈⠺⠮⠆ ⠲
[2022-04-15 23:47:47] Best translation 2144 : ⠹⠺⠱⠆⠞⠥⠍⠺⠱⠆⠞⠥ ⠝⠺⠁⠆⠾ ⠅ ⠡⠥⠾ ⠒ ⠣⠈⠔⠞⠋⠎⠓⠁⠾ ⠈⠔ ⠿⠪⠆⠸ ⠸⠣⠮⠆⠽⠔ ⠞⠺ ⠏⠋⠆⠈⠕⠆⠞⠋⠆ ⠍⠶⠆ ⠇⠱⠂ ⠩ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2145 : ⠩⠔ ⠒ ⠨⠔⠃⠽⠁ ⠓ ⠁⠥⠆ ⠰⠣ ⠽⠔⠟⠱⠆⠹ ⠲
[2022-04-15 23:47:47] Best translation 2146 : ⠼⠊ ⠉ ⠙ ⠨⠥⠂ ⠞⠺ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠎⠡⠓⠌⠁ ⠇⠑⠝⠁⠆ ⠹ ⠣⠗⠱⠆ ⠞⠺ ⠅⠁⠆ ⠍⠔⠆⠞⠽⠟⠪⠆ ⠅⠣ ⠃⠣⠷⠁⠆⠙⠣⠇⠣ ⠣⠏⠻ ⠣⠾⠑ ⠞ ⠩⠯ ⠣⠇⠶⠆⠞ ⠓⠥⠹⠻⠆ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠟⠱⠆⠗⠺⠁ ⠞⠺ ⠟⠥⠝ ⠌⠁⠆ ⠽⠴ ⠗ ⠞⠓⠁⠆ ⠞ ⠍⠥ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2147 : ⠼⠁ ⠚ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
[2022-04-15 23:47:47] Best translation 2148 : ⠍⠶⠘⠕⠆⠎⠢ ⠹ ⠵⠣⠞⠹⠣⠃⠔⠏⠔⠷⠁ ⠅ ⠣⠡⠱⠨⠋ ⠰⠣⠣ ⠎⠣⠯ ⠹⠔⠽⠥ ⠇⠱⠂⠇⠁ ⠨⠮⠂ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2149 : ⠗⠣⠞⠥⠂ ⠒ ⠞⠱⠆⠁⠣⠞ ⠚ ⠞⠺ ⠝⠋⠆ ⠍⠥ ⠝⠋⠆ ⠗⠁ ⠅ ⠞⠺⠱⠂ ⠝ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2150 : ⠪ ⠣⠨⠁ ⠌⠣⠞⠁ ⠅⠣ ⠃⠁⠳ ⠏⠁ ⠇⠆ ⠿ ⠓ ⠸⠽⠴ ⠗⠁ ⠎⠪⠆⠞ ⠅⠣ ⠝⠔ ⠰⠣⠣ ⠎⠁ ⠋ ⠞⠣⠞ ⠃⠮⠆ ⠝⠮⠂ ⠌ ⠗⠱⠆ ⠞⠮⠂ ⠎⠁ ⠞⠺⠱ ⠡⠪⠆⠍⠥⠝⠆ ⠏⠁⠸ ⠌ ⠏ ⠏⠭⠗⠣ ⠝⠱ ⠰⠣⠁ ⠏⠻⠂ ⠲
[2022-04-15 23:47:47] Best translation 2151 : ⠝⠱⠂⠞⠖⠆ ⠰⠣⠁ ⠅⠁⠆ ⠙⠶⠆⠏⠶ ⠹ ⠣⠎⠁ ⠩⠁⠯ ⠿⠋ ⠹ ⠩ ⠧ ⠈⠱⠅ ⠹⠁⠆⠌⠮ ⠚ ⠹ ⠣⠍⠊ ⠾⠑⠠⠣⠁ ⠅ ⠟⠪⠂ ⠅⠉ ⠑ ⠇⠬ ⠹⠅⠹ ⠌⠣ ⠹⠁⠆ ⠒ ⠌⠣ ⠹⠣⠍⠪⠆ ⠚ ⠹ ⠾⠱⠰⠣⠉⠂ ⠣⠇⠢⠆⠇⠢⠆ ⠅⠣⠞ ⠹⠻⠆ ⠅⠕ ⠿⠓ ⠣⠍⠊ ⠙ ⠅⠣⠞⠯ ⠱ ⠊ ⠲
[2022-04-15 23:47:47] Best translation 2152 : ⠪ ⠁⠑ ⠇⠥⠝⠯ ⠈⠋⠆⠟⠮ ⠇⠽⠴⠏⠣⠞ ⠹⠻⠆ ⠣⠽ ⠅ ⠟⠥ ⠋ ⠞⠣⠞ ⠛ ⠓ ⠈⠕ ⠊ ⠲
[2022-04-15 23:47:47] Best translation 2153 : ⠹⠥⠌⠮⠡⠔⠆ ⠏⠱⠆ ⠞⠮⠂ ⠍⠥⠞⠮ ⠣⠾⠣⠟⠕⠆⠓⠌⠁ ⠿⠪⠆ ⠿⠋ ⠗⠱⠆ ⠟ ⠗⠣⠶ ⠲
[2022-04-15 23:47:47] Best translation 2154 : ⠟⠥⠚ ⠹ ⠪ ⠍⠊⠞⠣⠈⠕⠆ ⠩⠔⠿⠥⠂ ⠅ ⠣⠇⠥⠝ ⠹⠣⠝⠁⠆ ⠎⠞⠝ ⠩ ⠇⠁ ⠟ ⠹ ⠗ ⠥⠆⠎⠋⠩⠺⠱ ⠗ ⠞⠖⠏⠔ ⠅⠁ ⠣⠸⠣⠥ ⠱⠝ ⠞⠺ ⠷⠣ ⠱⠅⠯ ⠞⠣⠞ ⠝ ⠹⠣⠓⠾⠣ ⠗⠣⠞⠞⠪ ⠈⠉⠆⠿⠓⠣⠞ ⠇⠬ ⠟ ⠃ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2155 : ⠟⠑⠥⠂ ⠿⠦ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2156 : ⠽⠨ ⠏⠔ ⠣⠈⠱⠅ ⠇⠥⠆ ⠹⠻⠆ ⠾⠁⠆ ⠿⠓ ⠏⠭ ⠹⠣⠞ ⠋⠂ ⠲
[2022-04-15 23:47:47] Best translation 2157 : ⠺⠋⠆⠹⠁⠁⠆⠗⠣ ⠒ ⠍⠣⠽⠁⠆ ⠅⠣ ⠞⠭ ⠹⠺⠮ ⠲
[2022-04-15 23:47:47] Best translation 2158 : ⠺⠱ ⠺⠱⠂ ⠺⠱⠆ ⠲
[2022-04-15 23:47:47] Best translation 2159 : ⠿⠋⠯ ⠹⠉⠆⠹⠣⠞ ⠟⠪⠂ ⠏⠁ ⠸ ⠾⠋⠍⠁ ⠃⠁⠹⠁⠎⠣⠅⠁⠆ ⠞⠺ ⠣⠗⠱⠆ ⠑⠨⠣⠗⠁ ⠩ ⠞⠓⠁⠆ ⠿⠪⠆ ⠭ ⠹⠿ ⠣⠗⠱⠆ ⠗ ⠣⠘⠣⠞ ⠓⠥⠯ ⠠⠣⠭ ⠾⠕⠆ ⠩ ⠱ ⠹ ⠲
[2022-04-15 23:47:47] Best translation 2160 : ⠺⠔⠆⠘⠋⠂ ⠇⠆ ⠋ ⠁⠖ ⠗⠣ ⠲
[2022-04-15 23:47:47] Best translation 2161 : ⠼⠁ ⠲ ⠴⠏⠁ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠚ ⠊ ⠣⠝⠑ ⠣⠙⠱⠅⠏⠮ ⠅ ⠣⠃⠊⠙⠋ ⠞⠺ ⠩⠁ ⠏ ⠲
[2022-04-15 23:47:48] Best translation 2162 : ⠹⠔⠨⠋⠆⠎⠁ ⠣⠟⠔⠆ ⠲
[2022-04-15 23:47:48] Best translation 2163 : ⠡⠭⠸⠣⠣⠎ ⠹⠻⠆ ⠹⠁⠆ ⠲
[2022-04-15 23:47:48] Best translation 2164 : ⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠇⠕⠂ ⠍⠱⠆ ⠲
[2022-04-15 23:47:48] Best translation 2165 : ⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
[2022-04-15 23:47:48] Best translation 2166 : ⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠍⠣⠹⠴⠹⠉⠆ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲
[2022-04-15 23:47:48] Total time: 65.67312s wall

real	12m29.381s
user	23m9.137s
sys	0m32.984s
```

ရလာတဲ့ BLEU score တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr$ cat ./test0-multi-PE-results.txt 
Evaluation on ./model0-mtbr.iter5000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter10000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter15000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter20000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter25000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter30000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter35000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter40000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter45000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter5000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter10000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter15000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter20000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter25000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter30000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter35000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter40000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter45000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
Evaluation on ./model0-mtbr.iter5000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 84.51, 95.1/89.8/85.0/80.4 (BP=0.967, ratio=0.968, hyp_len=27867, ref_len=28803)
Evaluation on ./model0-mtbr.iter10000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 85.40, 95.1/90.0/85.2/80.8 (BP=0.975, ratio=0.975, hyp_len=28086, ref_len=28803)
Evaluation on ./model0-mtbr.iter15000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 85.69, 95.0/90.0/85.2/80.7 (BP=0.979, ratio=0.979, hyp_len=28191, ref_len=28803)
Evaluation on ./model0-mtbr.iter20000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 85.94, 95.0/90.0/85.2/80.8 (BP=0.981, ratio=0.981, hyp_len=28264, ref_len=28803)
Evaluation on ./model0-mtbr.iter25000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.11, 95.0/89.9/85.2/80.7 (BP=0.983, ratio=0.984, hyp_len=28330, ref_len=28803)
Evaluation on ./model0-mtbr.iter30000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.26, 94.9/89.8/85.1/80.6 (BP=0.987, ratio=0.987, hyp_len=28424, ref_len=28803)
Evaluation on ./model0-mtbr.iter35000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.36, 95.0/89.8/85.0/80.5 (BP=0.988, ratio=0.988, hyp_len=28459, ref_len=28803)
Evaluation on ./model0-mtbr.iter40000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.37, 95.0/89.8/85.0/80.5 (BP=0.988, ratio=0.988, hyp_len=28459, ref_len=28803)
Evaluation on ./model0-mtbr.iter45000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.39, 95.0/89.8/85.0/80.5 (BP=0.989, ratio=0.989, hyp_len=28476, ref_len=28803)
Evaluation on ./model0-mtbr.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.42, 94.8/89.7/84.9/80.4 (BP=0.990, ratio=0.990, hyp_len=28512, ref_len=28803)
Evaluation on ./model0-mtbr.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.41, 94.9/89.7/85.0/80.5 (BP=0.989, ratio=0.989, hyp_len=28489, ref_len=28803)
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-multi-mybr$
```

Best model, best score က အောက်ပါအတိုင်း  

```
Evaluation on ./model0-mtbr.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.42, 94.8/89.7/84.9/80.4 (BP=0.990, ratio=0.990, hyp_len=28512, ref_len=28803)
```

ခုချိန်ထိ လုပ်ခဲ့တဲ့ expeirment သုံးခု ကို နှိုင်းယှဉ်ကြည့်ရင်...  

<div align="center">

Table 1. Performance comparison for Transformer, Transformer-PE_Transformer and Multisource-Transformer 
 
| Transformer | Transformer-PE_Transformer | Multisource Transformer |
|----------:|----------:|----------:|  
| 86.73 | 86.26 | 86.42 |  

 </div>
 
## Shared-multisourced for {my,mt_br}--->{br}


type option ကိုပဲ shared-multi-transformer ပေးပြီး training လုပ်ရင် အောက်ပါ Error ပေးတယ်   

```
[2022-04-16 00:48:41] Error: Requested shape shape=18364x512 size=9402368 for existing parameter 'encoder_Wemb' does not match original shape shape=18602x512 size=9524224

```

အဲဒါကြောင့် vocab ကို ပေါင်းဆောက်ခဲ့တယ်...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ cat /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my /media/ye/project2/exp/braille-nmt/model.transformer/hyp.iter95000-trainingdata.br > /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my-train.mtbr
(base) ye@:/media/ye/project2/exp/braille-nmt$ marian-vocab < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my-train.mtbr > /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.my-train.mtbr.yml
[2022-04-16 00:56:04] Creating vocabulary...
[2022-04-16 00:56:04] [data] Creating vocabulary stdout from stdin
[2022-04-16 00:56:04] Finished
(base) ye@:/media/ye/project2/exp/braille-nmt$
```

training bash script ကို အောက်ပါအတိုင်း update လုပ်ခဲ့တယ်။  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Transformer MT_Braille-to-Ref_Braille
## 16 April 2022

# ဘာတွေထပ်ဖြည့်ခဲ့သလဲ ဆိုရင်
# running folder နာမည် ပြောင်းပြီး
# --type shared-multi-transformer
# --train-sets မှာ {source,mt,target} ထား
# --vocabs မှာလည်း {source,mt,target} ပေးခဲ့
# --valid-sets မှာလည်း {source,mt,target} ပေးခဲ့
# Error: Requested shape shape=18364x512 size=9402368 for existing parameter 'Wemb' does not match original shape ... ဆိုတဲ့ error ပေးတာကြောင့်
# vocab ကို source+mt (သို့) my+mt_braille ကို ပေါင်းဆောက်ခဲ့ပြီးမှ run လို့ အဆင်ပြေတယ်။  

mkdir model.transformer-shared-multi-mybr;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.npz --type shared-multi-transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my /media/ye/project2/exp/braille-nmt/model.transformer/hyp.iter95000-trainingdata.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.my-train.mtbr.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.my-train.mtbr.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my /media/ye/project2/exp/braille-nmt/model.transformer/hyp.iter95000-devdata.br /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/dev.multi-mybr.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ./model.transformer-shared-multi-mybr/train-shared-multi-mybr.log --valid-log ./model.transformer-shared-multi-mybr/valid-shared-multi-mybr.log \
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
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/config-shared-multi-mybr0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/config-shared-multi-mybr0.yml  2>&1 | tee transformer-shared-multi-mybr0.log

```

training ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./shared-multi-transformer-pe-mymt2br.sh 
...
...
...
[2022-04-16 10:38:21] Starting data epoch 792 in logical epoch 792
[2022-04-16 10:38:21] [data] Shuffling data
[2022-04-16 10:38:21] [data] Done reading 16,415 sentences
[2022-04-16 10:38:21] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:39:04] Seen 16415 samples
[2022-04-16 10:39:04] Starting data epoch 793 in logical epoch 793
[2022-04-16 10:39:04] [data] Shuffling data
[2022-04-16 10:39:04] [data] Done reading 16,415 sentences
[2022-04-16 10:39:04] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:39:47] Seen 16415 samples
[2022-04-16 10:39:47] Starting data epoch 794 in logical epoch 794
[2022-04-16 10:39:47] [data] Shuffling data
[2022-04-16 10:39:47] [data] Done reading 16,415 sentences
[2022-04-16 10:39:47] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:40:17] Ep. 794 : Up. 79500 : Sen. 11,800 : Cost 1.32029402 * 1,178,878 @ 2,600 after 187,770,507 : Time 214.83s : 5487.43 words/s : L.r. 1.3459e-04
[2022-04-16 10:40:30] Seen 16415 samples
[2022-04-16 10:40:30] Starting data epoch 795 in logical epoch 795
[2022-04-16 10:40:30] [data] Shuffling data
[2022-04-16 10:40:30] [data] Done reading 16,415 sentences
[2022-04-16 10:40:30] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:41:13] Seen 16415 samples
[2022-04-16 10:41:13] Starting data epoch 796 in logical epoch 796
[2022-04-16 10:41:13] [data] Shuffling data
[2022-04-16 10:41:13] [data] Done reading 16,415 sentences
[2022-04-16 10:41:13] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:41:57] Seen 16415 samples
[2022-04-16 10:41:57] Starting data epoch 797 in logical epoch 797
[2022-04-16 10:41:57] [data] Shuffling data
[2022-04-16 10:41:57] [data] Done reading 16,415 sentences
[2022-04-16 10:41:57] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:42:40] Seen 16415 samples
[2022-04-16 10:42:40] Starting data epoch 798 in logical epoch 798
[2022-04-16 10:42:40] [data] Shuffling data
[2022-04-16 10:42:40] [data] Done reading 16,415 sentences
[2022-04-16 10:42:40] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:43:23] Seen 16415 samples
[2022-04-16 10:43:23] Starting data epoch 799 in logical epoch 799
[2022-04-16 10:43:23] [data] Shuffling data
[2022-04-16 10:43:23] [data] Done reading 16,415 sentences
[2022-04-16 10:43:23] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 10:43:53] Ep. 799 : Up. 80000 : Sen. 11,124 : Cost 1.32034349 * 1,178,075 @ 2,158 after 188,948,582 : Time 215.54s : 5465.82 words/s : L.r. 1.3416e-04
[2022-04-16 10:43:53] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.npz.orig.npz
[2022-04-16 10:43:54] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.iter80000.npz
[2022-04-16 10:43:54] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.npz
[2022-04-16 10:43:55] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.npz.optimizer.npz
[2022-04-16 10:43:59] [valid] Ep. 799 : Up. 80000 : cross-entropy : 9.29162 : stalled 10 times (last best: 9.24582)
[2022-04-16 10:44:02] [valid] Ep. 799 : Up. 80000 : perplexity : 1.897 : stalled 10 times (last best: 1.89103)
[2022-04-16 10:44:19] [valid] Ep. 799 : Up. 80000 : bleu : 86.7726 : stalled 4 times (last best: 86.8123)
[2022-04-16 10:44:20] Training finished
[2022-04-16 10:44:20] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.npz.orig.npz
[2022-04-16 10:44:21] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.npz
[2022-04-16 10:44:22] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr/model0-mtbr.npz.optimizer.npz

real	583m13.774s
user	968m14.858s
sys	1m1.801s

```

## Testing and Evaluation for Shared Multisource Transformer {my,mt_br}-->{br}

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung PE
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Transformer multi PE Model
## 16 April 2022
## vocab က shared-vocab ဖိုင်ကို assign လုပ်ခဲ့တယ်

for i in {5000..80000..5000}
do
   marian-decoder -m ./model0-mtbr.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.my-train.mtbr.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.my-train.mtbr.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml --devices 0 1 --output hyp.iter$i.br --input  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my --input ../model.transformer/hyp.iter95000.br
   echo "Evaluation on ./model0-mtbr.iter${i}.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:" >> test0-shared-multi-PE-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br < ./hyp.iter$i.br  >> test0-shared-multi-PE-results.txt
done
```

testing ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr$ time ./tran-eval-shared-multi.sh | tee tran-eval-shared-multi.log
...
...
...
[2022-04-16 12:17:34] Best translation 2131 : ⠍⠊⠍⠊ ⠅⠕⠞⠖ ⠣⠹⠋⠝⠱⠣⠹⠋⠞⠓⠁⠆ ⠿⠓ ⠗⠥⠞⠈⠕ ⠇⠱⠂⠟⠔⠂ ⠏ ⠲
[2022-04-16 12:17:34] Best translation 2132 : ⠶ ⠨⠣ ⠶ ⠞⠭⠥⠂⠞⠥⠂ ⠸ ⠤⠤⠤⠤⠤⠤ ⠎⠪ ⠟⠁⠾⠔⠂ ⠏ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2133 : ⠷⠶⠏⠔⠹⠁⠗⠺⠁ ⠿⠓⠥⠆ ⠾⠕⠂⠝⠮ ⠼⠁ ⠉ ⠙ ⠑ ⠨⠥⠂ ⠒ ⠞⠋⠨⠥⠆ ⠇⠣⠈⠋⠆ ⠼⠁ ⠗⠑ ⠹⠥⠌⠮⠡⠔⠆ ⠗⠪⠞⠥ ⠹⠥⠌⠮⠡⠔⠆ ⠁⠋⠙ ⠅⠕⠂⠁⠆⠅⠕⠅⠕⠆ ⠎⠁⠗⠱⠆⠇⠬ ⠏ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2134 : ⠼⠓ ⠲ ⠁⠆⠹⠋ ⠰⠶ ⠋ ⠗⠣ ⠋ ⠝⠱ ⠋ ⠭ ⠋ ⠝⠱ ⠁⠆⠁⠦ ⠟⠕⠆⠏⠋⠆ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2135 : ⠿⠁⠆⠗⠪ ⠹⠁ ⠈⠶⠽⠥ ⠟⠣ ⠡⠱ ⠓ ⠈⠕⠯ ⠿⠁⠆⠗⠪ ⠅ ⠈⠶⠽⠥ ⠎ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠫ ⠣⠏⠴⠺⠣ ⠠⠣⠭ ⠘⠑ ⠅ ⠇⠢⠆⠹⠦ ⠿⠪⠆ ⠰⠣⠣ ⠝⠥⠆⠷⠋⠂ ⠹⠢⠍⠺⠱⠂ ⠸⠣⠣⠎ ⠹⠻⠆ ⠅⠋⠃⠣⠇⠁ ⠡⠪ ⠟⠕⠆ ⠅ ⠟⠭ ⠿⠪⠆⠸ ⠼ ⠅⠋⠃⠣⠇⠁ ⠟⠕⠆ ⠎⠣ ⠫ ⠿⠁⠆⠗⠪ ⠿⠓ ⠩⠺⠱⠰⠣⠋⠅⠔⠆ ⠟⠕⠆ ⠎⠣ ⠅ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠏⠴ ⠺⠣ ⠟⠕⠆ ⠎⠣ ⠞⠭⠘⠑ ⠗ ⠞⠱⠂ ⠿⠪⠆ ⠎⠔⠆⠌⠮ ⠿⠪⠆ ⠎⠔⠆⠌⠮ ⠹⠺⠔⠆⠯ ⠞⠓⠁⠆ ⠿⠪⠆ ⠧ ⠏⠣⠞⠞⠣⠾⠁⠆ ⠺⠣ ⠅⠣ ⠏⠥⠂⠗⠺⠑ ⠒ ⠏⠕⠆⠗⠺⠣ ⠒ ⠏⠕⠆⠗⠺⠣ ⠒ ⠶⠕⠅ ⠅ ⠎⠁⠆⠹⠴ ⠎ ⠡ ⠓⠌⠁ ⠝⠱⠗⠁ ⠒ ⠝⠱⠗⠁ ⠚ ⠅ ⠏⠥⠂⠗⠺⠑ ⠑ ⠝⠱⠗⠁ ⠚ ⠅ ⠏⠥⠂⠗⠺⠑ ⠑ ⠝⠱⠗⠁ ⠫ ⠞⠓⠁⠆ ⠊ ⠲
[2022-04-16 12:17:34] Best translation 2136 : ⠟⠞⠚ ⠗ ⠗⠔⠆⠠⠣⠪⠆ ⠹⠻⠆ ⠣⠟⠣⠽ ⠏⠔ ⠭ ⠇⠔⠂ ⠅⠣⠎⠁⠆ ⠒ ⠟⠞⠚ ⠋⠸⠣⠣⠹⠥ ⠰⠣⠣ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠞⠚ ⠟⠪⠂⠾⠔ ⠨⠋⠎⠁⠆ ⠹⠣⠇⠕ ⠋ ⠗⠱⠆ ⠗⠣ ⠒ ⠟⠶⠆ ⠿⠁⠞⠁ ⠟⠪⠆ ⠊ ⠇⠑⠈⠭ ⠰⠣⠣ ⠗⠱⠆ ⠗⠣ ⠍ ⠲
[2022-04-16 12:17:34] Best translation 2137 : ⠎⠣⠅⠁⠆⠇⠉⠆ ⠅⠣⠇⠱⠆ ⠞⠺⠱ ⠎⠪ ⠅⠁ ⠗⠮ ⠗⠥⠞⠈⠕ ⠗⠱⠆ ⠟⠪⠂ ⠍⠮ ⠲
[2022-04-16 12:17:34] Best translation 2138 : ⠍⠣⠾⠣⠗⠔ ⠚ ⠣⠷⠢⠂ ⠅⠣ ⠹⠂ ⠨⠱⠞⠄ ⠅⠣ ⠣⠏⠽⠄ ⠋ ⠏⠻ ⠹⠱⠆ ⠏ ⠣⠷⠢⠂ ⠍⠔⠆⠹⠣⠍⠪⠆⠾ ⠹ ⠏⠺⠮⠆⠨⠔⠆ ⠅ ⠏⠴ ⠶ ⠍⠊⠍⠊ ⠊ ⠏⠔⠅ ⠣⠹⠋ ⠗ ⠟⠕⠆⠎⠁⠆⠯ ⠈⠕ ⠟ ⠗⠣ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2139 : ⠰⠣⠪⠷⠋⠆⠿⠥⠂ ⠺⠥⠞⠁⠥⠂⠾ ⠒ ⠃⠁⠹⠁⠿⠋ ⠺⠥⠞⠁⠥⠂⠾ ⠭⠞⠮ ⠗⠁ ⠎⠱⠅⠁⠮⠆ ⠒ ⠌⠁⠆⠾⠭⠡⠔⠆ ⠒ ⠥⠆⠃⠣⠷⠶ ⠒ ⠅⠥⠆⠞⠕⠂ ⠒ ⠺⠁⠆⠘⠣⠞ ⠒ ⠝⠁⠆⠇⠪ ⠒ ⠗⠮⠆⠗⠮⠆⠺⠔⠝⠂⠺⠔⠂ ⠎⠣⠹ ⠚ ⠰⠣⠁ ⠁⠔⠩⠁⠆ ⠹⠻⠆ ⠰⠣⠪⠷⠋⠆⠿⠥⠂ ⠺⠥⠞⠁⠥⠂⠾ ⠭ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2140 : ⠩⠱⠆⠨⠭ ⠎⠭⠹⠪ ⠞⠭ ⠥⠆ ⠊ ⠃⠣⠺⠣ ⠞⠭ ⠎⠱⠅ ⠞⠭ ⠏⠖⠆ ⠅ ⠁⠔⠓⠣⠞ ⠹⠻⠆ ⠖⠆⠡⠔⠆ ⠭ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2141 : ⠇⠱⠅⠿⠁ ⠞⠺ ⠇⠆ ⠣⠡⠁⠆ ⠹⠻⠆ ⠓⠌⠑⠾ ⠅⠹ ⠥⠆⠨⠶⠆ ⠏⠖⠆ ⠒ ⠗⠔ ⠏⠖⠆ ⠒ ⠺⠋⠆⠃⠬ ⠏⠖⠆ ⠓⠥⠯ ⠩ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2142 : ⠅⠁⠞⠥⠝⠆ ⠈⠣⠗⠁⠟⠪⠆ ⠥⠆⠃⠣⠚⠋⠆ ⠲
[2022-04-16 12:17:34] Best translation 2143 : ⠵⠣⠾⠔⠆⠈⠺⠮⠆ ⠲
[2022-04-16 12:17:34] Best translation 2144 : ⠹⠺⠱⠆⠞⠥⠍⠺⠱⠆⠞⠥ ⠝⠺⠁⠆⠾ ⠅ ⠡⠥⠾ ⠒ ⠣⠈⠔⠞⠋⠎⠓⠁⠾ ⠈⠔ ⠿⠪⠆⠸ ⠸⠣⠮⠆⠽⠔ ⠞⠺ ⠏⠋⠆⠈⠕⠆⠞⠋⠆ ⠍⠶⠆ ⠇⠱⠂ ⠩ ⠹ ⠲
[2022-04-16 12:17:34] Best translation 2145 : ⠩⠔ ⠒ ⠨⠔⠃⠽⠁ ⠓ ⠁⠥⠆ ⠰⠣ ⠽⠔⠟⠱⠆⠹ ⠲
[2022-04-16 12:17:35] Best translation 2146 : ⠼⠊ ⠉ ⠙ ⠨⠥⠂ ⠞⠺ ⠏⠻⠏⠴ ⠨⠮⠂ ⠹⠻⠆ ⠎⠡⠓⠌⠁ ⠇⠑⠝⠁⠆ ⠹ ⠣⠗⠱⠆ ⠞⠺ ⠅⠁⠆ ⠍⠔⠆⠞⠽⠟⠪⠆ ⠅⠣ ⠃⠣⠷⠁⠆⠙⠣⠇⠣ ⠣⠏⠻ ⠣⠾⠑ ⠞ ⠩⠯ ⠣⠇⠶⠆⠞ ⠓⠥⠹⠻⠆ ⠽⠕⠆⠙⠣⠽⠁⠆ ⠟⠱⠆⠗⠺⠁ ⠞⠺ ⠟⠥⠝ ⠌⠁⠆ ⠽⠴ ⠗ ⠞⠓⠁⠆ ⠞ ⠍⠥ ⠹ ⠲
[2022-04-16 12:17:35] Best translation 2147 : ⠼⠁ ⠚ ⠲ ⠺⠁⠹⠣⠝⠁ ⠰⠶ ⠎⠺⠮⠆⠾⠮⠆ ⠝⠱ ⠹⠻⠆ ⠣⠇⠱⠂⠣⠟⠔⠂ ⠲
[2022-04-16 12:17:35] Best translation 2148 : ⠍⠶⠘⠕⠆⠎⠢ ⠹ ⠵⠣⠞⠹⠣⠃⠔⠏⠔⠷⠁ ⠅ ⠣⠡⠱⠨⠋ ⠰⠣⠣ ⠎⠣⠯ ⠹⠔⠽⠥ ⠇⠱⠂⠇⠁ ⠨⠮⠂ ⠹ ⠲
[2022-04-16 12:17:35] Best translation 2149 : ⠗⠣⠞⠥⠂ ⠒ ⠞⠱⠆⠁⠣⠞ ⠚ ⠞⠺ ⠝⠋⠆ ⠍⠥ ⠝⠋⠆ ⠗⠁ ⠅ ⠞⠺⠱⠂ ⠝ ⠹ ⠲
[2022-04-16 12:17:35] Best translation 2150 : ⠪ ⠣⠨⠁ ⠌⠣⠞⠁ ⠅⠣ ⠃⠁⠳ ⠏⠁ ⠇⠆ ⠿ ⠓ ⠸⠽⠴ ⠗⠁ ⠎⠪⠆⠞ ⠅⠣ ⠝⠔ ⠰⠣⠣ ⠎⠁ ⠋ ⠞⠣⠞ ⠃⠮⠆ ⠝⠮⠂ ⠌ ⠗⠱⠆ ⠞⠮⠂ ⠎⠁ ⠞⠺⠱ ⠡⠪⠆⠍⠥⠝⠆ ⠏⠁⠸ ⠌ ⠏ ⠏⠭⠗⠣ ⠝⠱ ⠰⠣⠁ ⠏⠻⠂ ⠲
[2022-04-16 12:17:35] Best translation 2151 : ⠝⠱⠂⠞⠖⠆ ⠰⠣⠁ ⠅⠁⠆ ⠙⠶⠆⠏⠶ ⠹ ⠣⠎⠁ ⠩⠁⠯ ⠿⠋ ⠹ ⠩ ⠧ ⠈⠱⠅ ⠹⠁⠆⠌⠮ ⠚ ⠹ ⠣⠍⠊ ⠾⠑⠠⠣⠁ ⠅ ⠟⠪⠂ ⠅⠉ ⠑ ⠇⠬ ⠹⠅⠹ ⠌⠣ ⠹⠁⠆ ⠒ ⠌⠣ ⠹⠣⠍⠪⠆ ⠚ ⠹ ⠾⠱⠰⠣⠉⠂ ⠣⠇⠢⠆⠇⠢⠆ ⠅⠣⠞ ⠹⠻⠆ ⠅⠕ ⠿⠓ ⠣⠍⠊ ⠙ ⠅⠣⠞⠯ ⠱ ⠊ ⠲
[2022-04-16 12:17:35] Best translation 2152 : ⠪ ⠁⠑ ⠇⠥⠝⠯ ⠈⠋⠆⠟⠮ ⠇⠽⠴⠏⠣⠞ ⠹⠻⠆ ⠣⠽ ⠅ ⠟⠥ ⠋ ⠞⠣⠞ ⠛ ⠓ ⠈⠕ ⠊ ⠲
[2022-04-16 12:17:35] Best translation 2153 : ⠹⠥⠌⠮⠡⠔⠆ ⠏⠱⠆ ⠞⠮⠂ ⠍⠥⠞⠮ ⠣⠾⠣⠟⠕⠆⠓⠌⠁ ⠿⠪⠆ ⠿⠋ ⠗⠱⠆ ⠟ ⠗⠣⠶ ⠲
[2022-04-16 12:17:35] Best translation 2154 : ⠟⠥⠚ ⠹ ⠪ ⠍⠊⠞⠣⠈⠕⠆ ⠩⠔⠿⠥⠂ ⠅ ⠣⠇⠥⠝ ⠹⠣⠝⠁⠆ ⠎⠞⠝ ⠩ ⠇⠁ ⠟ ⠹ ⠗ ⠥⠆⠎⠋⠩⠺⠱ ⠗ ⠞⠖⠏⠔ ⠅⠁ ⠣⠸⠣⠥ ⠱⠝ ⠞⠺ ⠷⠣ ⠱⠅⠯ ⠞⠣⠞ ⠝ ⠹⠣⠓⠾⠣ ⠗⠣⠞⠞⠪ ⠈⠉⠆⠿⠓⠣⠞ ⠇⠬ ⠟ ⠃ ⠹ ⠲
[2022-04-16 12:17:35] Best translation 2155 : ⠟⠑⠥⠂ ⠿⠦ ⠹ ⠲
[2022-04-16 12:17:35] Best translation 2156 : ⠽⠨ ⠏⠔ ⠣⠈⠱⠅ ⠇⠥⠆ ⠹⠻⠆ ⠾⠁⠆ ⠿⠓ ⠏⠭ ⠹⠣⠞ ⠋⠂ ⠲
[2022-04-16 12:17:35] Best translation 2157 : ⠺⠋⠆⠹⠁⠁⠆⠗⠣ ⠒ ⠍⠣⠽⠁⠆ ⠅⠣ ⠞⠭ ⠹⠺⠮ ⠲
[2022-04-16 12:17:35] Best translation 2158 : ⠺⠱ ⠺⠱⠂ ⠺⠱⠆ ⠲
[2022-04-16 12:17:35] Best translation 2159 : ⠿⠋⠯ ⠹⠉⠆⠹⠣⠞ ⠟⠪⠂ ⠏⠁ ⠸ ⠾⠋⠍⠁ ⠃⠁⠹⠁⠎⠣⠅⠁⠆ ⠞⠺ ⠣⠗⠱⠆ ⠑⠨⠣⠗⠁ ⠩ ⠞⠓⠁⠆ ⠿⠪⠆ ⠭ ⠹⠿ ⠣⠗⠱⠆ ⠗ ⠣⠘⠣⠞ ⠓⠥⠯ ⠠⠣⠭ ⠾⠕⠆ ⠩ ⠱ ⠹ ⠲
[2022-04-16 12:17:35] Best translation 2160 : ⠺⠔⠆⠘⠋⠂ ⠇⠆ ⠋ ⠁⠖ ⠗⠣ ⠲
[2022-04-16 12:17:35] Best translation 2161 : ⠼⠁ ⠲ ⠴⠏⠁ ⠎⠣⠅⠁⠆⠇⠉⠆ ⠚ ⠊ ⠣⠝⠑ ⠣⠙⠱⠅⠏⠮ ⠅ ⠣⠃⠊⠙⠋ ⠞⠺ ⠩⠁ ⠏ ⠲
[2022-04-16 12:17:35] Best translation 2162 : ⠹⠔⠨⠋⠆⠎⠁ ⠣⠟⠔⠆ ⠲
[2022-04-16 12:17:35] Best translation 2163 : ⠡⠭⠸⠣⠣⠎ ⠹⠻⠆ ⠹⠁⠆ ⠲
[2022-04-16 12:17:35] Best translation 2164 : ⠓⠕ ⠩⠱⠂ ⠅⠣ ⠈⠥⠷⠋ ⠈⠥⠷⠋ ⠒ ⠃⠁ ⠹⠋ ⠇⠕⠂ ⠍⠱⠆ ⠲
[2022-04-16 12:17:35] Best translation 2165 : ⠍⠔⠛⠣⠇⠁⠏⠁ ⠲
[2022-04-16 12:17:35] Best translation 2166 : ⠍⠊⠍⠊ ⠞⠪ ⠹⠻⠆ ⠿ ⠍⠣⠹⠴⠹⠉⠆ ⠒ ⠸⠣⠥ ⠨⠮⠂ ⠹⠻⠆ ⠟⠥⠝ ⠗ ⠺⠥⠞⠁⠥⠂ ⠏⠭⠎⠪⠆ ⠣⠎⠥⠂⠎⠥⠂ ⠅ ⠠⠣⠶⠆⠇⠥ ⠚ ⠿⠓⠑⠈⠪⠆ ⠠⠣⠱⠅⠎⠑ ⠍⠂ ⠗⠋ ⠰⠣⠣ ⠅⠁⠅⠺⠮ ⠇⠕ ⠡ ⠭ ⠹ ⠲
[2022-04-16 12:17:35] Total time: 64.75555s wall

real	17m25.141s
user	33m29.227s
sys	0m43.057s
```

BLEU score တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-mybr$ cat test0-shared-multi-PE-results.txt 
Evaluation on ./model0-mtbr.iter5000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 15.6/0.4/0.0/0.0 (BP=0.865, ratio=0.873, hyp_len=25151, ref_len=28803)
Evaluation on ./model0-mtbr.iter10000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 14.2/0.3/0.0/0.0 (BP=0.805, ratio=0.822, hyp_len=23678, ref_len=28803)
Evaluation on ./model0-mtbr.iter15000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 15.5/0.2/0.0/0.0 (BP=0.715, ratio=0.749, hyp_len=21569, ref_len=28803)
Evaluation on ./model0-mtbr.iter20000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 15.0/0.2/0.0/0.0 (BP=0.743, ratio=0.771, hyp_len=22211, ref_len=28803)
Evaluation on ./model0-mtbr.iter25000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 14.2/0.2/0.0/0.0 (BP=0.759, ratio=0.784, hyp_len=22581, ref_len=28803)
Evaluation on ./model0-mtbr.iter30000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 14.0/0.2/0.0/0.0 (BP=0.711, ratio=0.746, hyp_len=21475, ref_len=28803)
Evaluation on ./model0-mtbr.iter35000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.7/0.1/0.0/0.0 (BP=0.743, ratio=0.771, hyp_len=22202, ref_len=28803)
Evaluation on ./model0-mtbr.iter40000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.8/0.2/0.0/0.0 (BP=0.760, ratio=0.785, hyp_len=22596, ref_len=28803)
Evaluation on ./model0-mtbr.iter45000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 14.1/0.1/0.0/0.0 (BP=0.770, ratio=0.793, hyp_len=22839, ref_len=28803)
Evaluation on ./model0-mtbr.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.9/0.1/0.0/0.0 (BP=0.797, ratio=0.815, hyp_len=23470, ref_len=28803)
Evaluation on ./model0-mtbr.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.5/0.1/0.0/0.0 (BP=0.831, ratio=0.844, hyp_len=24296, ref_len=28803)
Evaluation on ./model0-mtbr.iter60000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.2/0.1/0.0/0.0 (BP=0.818, ratio=0.833, hyp_len=23980, ref_len=28803)
Evaluation on ./model0-mtbr.iter65000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.4/0.1/0.0/0.0 (BP=0.843, ratio=0.854, hyp_len=24589, ref_len=28803)
Evaluation on ./model0-mtbr.iter70000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.2/0.1/0.0/0.0 (BP=0.855, ratio=0.865, hyp_len=24913, ref_len=28803)
Evaluation on ./model0-mtbr.iter75000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.1/0.1/0.0/0.0 (BP=0.858, ratio=0.867, hyp_len=24986, ref_len=28803)
Evaluation on ./model0-mtbr.iter80000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 0.00, 13.3/0.2/0.0/0.0 (BP=0.870, ratio=0.878, hyp_len=25287, ref_len=28803)
Evaluation on ./model0-mtbr.iter5000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 85.27, 94.6/89.3/84.4/79.9 (BP=0.981, ratio=0.982, hyp_len=28272, ref_len=28803)
Evaluation on ./model0-mtbr.iter10000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 85.99, 95.1/90.0/85.2/80.7 (BP=0.982, ratio=0.982, hyp_len=28281, ref_len=28803)
Evaluation on ./model0-mtbr.iter15000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 85.97, 95.1/90.0/85.3/80.9 (BP=0.980, ratio=0.981, hyp_len=28245, ref_len=28803)
Evaluation on ./model0-mtbr.iter20000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.22, 95.1/90.0/85.3/80.9 (BP=0.983, ratio=0.984, hyp_len=28331, ref_len=28803)
Evaluation on ./model0-mtbr.iter25000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.41, 95.1/90.0/85.3/80.8 (BP=0.986, ratio=0.986, hyp_len=28410, ref_len=28803)
Evaluation on ./model0-mtbr.iter30000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.51, 95.1/90.0/85.4/80.9 (BP=0.986, ratio=0.986, hyp_len=28413, ref_len=28803)
Evaluation on ./model0-mtbr.iter35000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.53, 95.1/90.0/85.4/81.0 (BP=0.987, ratio=0.987, hyp_len=28417, ref_len=28803)
Evaluation on ./model0-mtbr.iter40000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.69, 95.1/90.0/85.3/80.8 (BP=0.989, ratio=0.989, hyp_len=28499, ref_len=28803)
Evaluation on ./model0-mtbr.iter45000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.70, 95.1/90.0/85.3/80.8 (BP=0.989, ratio=0.989, hyp_len=28498, ref_len=28803)
Evaluation on ./model0-mtbr.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.70, 95.1/90.0/85.3/80.9 (BP=0.989, ratio=0.989, hyp_len=28495, ref_len=28803)
Evaluation on ./model0-mtbr.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.70, 95.1/90.0/85.3/80.8 (BP=0.989, ratio=0.989, hyp_len=28496, ref_len=28803)
Evaluation on ./model0-mtbr.iter60000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.69, 95.1/90.0/85.3/80.8 (BP=0.989, ratio=0.989, hyp_len=28493, ref_len=28803)
Evaluation on ./model0-mtbr.iter65000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.70, 95.0/90.0/85.3/80.8 (BP=0.989, ratio=0.990, hyp_len=28502, ref_len=28803)
Evaluation on ./model0-mtbr.iter70000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.70, 95.0/89.9/85.3/80.8 (BP=0.990, ratio=0.990, hyp_len=28511, ref_len=28803)
Evaluation on ./model0-mtbr.iter75000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.71, 95.0/89.9/85.3/80.8 (BP=0.990, ratio=0.990, hyp_len=28513, ref_len=28803)
Evaluation on ./model0-mtbr.iter80000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.72, 95.0/90.0/85.3/80.8 (BP=0.990, ratio=0.990, hyp_len=28512, ref_len=28803)
```

Best model နဲ့ best score ကတော့ အောက်ပါအတိုင်း...  

```
Evaluation on ./model0-mtbr.iter80000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my ../model.transformer-brmy/hyp.iteriter80000.my, Transformer multi-source PE Model:
BLEU = 86.72, 95.0/90.0/85.3/80.8 (BP=0.990, ratio=0.990, hyp_len=28512, ref_len=28803)
```

ခုချိန်ထိ လုပ်ခဲ့တဲ့ expeirment အားလုံးကို နှိုင်းယှဉ်ကြည့်ရင်...  

<div align="center">

Table 1. Performance comparison for Transformer, Transformer-PE_Transformer, Multisource-Transformer and Shared Multisource Transformer
 
| Transformer | Transformer-PE_Transformer | Multisource Transformer | Shared Multisource Transformer |
|----------:|----------:|----------:|----------:|   
| 86.73 | 86.26 | 86.42 | 86.72 | 

 </div>
 
## Training for Multisource Transformer, {br,mt_my}--->{my}

ဒီတစ်ခါတော့ reverse direction ဖြစ်တဲ့ {br, mt_my}--->{my} အတွက် စပြင်မယ်။  
အရင်ဆုံး Multi-source အတွက် configuration file ကို ပြင်ရမယ်။  
update လုပ်ခဲ့တဲ့ bash script (multi-transformer-pe-brmt2my.sh) က အောက်ပါအတိုင်း...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for Transformer MT_Braille-to-Ref_Braille
## 16 April 2022

# ဘာတွေထပ်ဖြည့်ခဲ့သလဲ ဆိုရင်
# running folder နာမည် ပြောင်းပြီး
# --type multi-transformer
# --train-sets မှာ {source,mt,target} ထား
# --vocabs မှာလည်း {source,mt,target} ပေးခဲ့
# --valid-sets မှာလည်း {source,mt,target} ပေးခဲ့
  

mkdir model.transformer-multi-brmy;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.npz --type multi-transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000-trainingdata.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000-devdata.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/dev.multi-brmy.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ./model.transformer-multi-brmy/train-multi-brmy.log --valid-log ./model.transformer-multi-brmy/valid-multi-brmy.log \
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
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/config-multi-brmy0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/config-multi-brmy0.yml  2>&1 | tee transformer-multi-brmy0.log

```

training စလုပ်...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./multi-transformer-pe-brmt2my.sh 
...
...
...
[2022-04-16 20:08:20] Starting data epoch 539 in logical epoch 539
[2022-04-16 20:08:20] [data] Shuffling data
[2022-04-16 20:08:20] [data] Done reading 16,415 sentences
[2022-04-16 20:08:20] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:09:05] Seen 16415 samples
[2022-04-16 20:09:05] Starting data epoch 540 in logical epoch 540
[2022-04-16 20:09:05] [data] Shuffling data
[2022-04-16 20:09:05] [data] Done reading 16,415 sentences
[2022-04-16 20:09:05] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:09:50] Seen 16415 samples
[2022-04-16 20:09:50] Starting data epoch 541 in logical epoch 541
[2022-04-16 20:09:50] [data] Shuffling data
[2022-04-16 20:09:50] [data] Done reading 16,415 sentences
[2022-04-16 20:09:50] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:10:35] Seen 16415 samples
[2022-04-16 20:10:35] Starting data epoch 542 in logical epoch 542
[2022-04-16 20:10:35] [data] Shuffling data
[2022-04-16 20:10:35] [data] Done reading 16,415 sentences
[2022-04-16 20:10:35] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:11:20] Seen 16415 samples
[2022-04-16 20:11:20] Starting data epoch 543 in logical epoch 543
[2022-04-16 20:11:20] [data] Shuffling data
[2022-04-16 20:11:20] [data] Done reading 16,415 sentences
[2022-04-16 20:11:21] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:11:56] Ep. 543 : Up. 54500 : Sen. 12,800 : Cost 1.32841587 * 1,179,705 @ 2,544 after 128,406,484 : Time 225.83s : 5223.94 words/s : L.r. 1.6255e-04
[2022-04-16 20:12:07] Seen 16415 samples
[2022-04-16 20:12:07] Starting data epoch 544 in logical epoch 544
[2022-04-16 20:12:07] [data] Shuffling data
[2022-04-16 20:12:07] [data] Done reading 16,415 sentences
[2022-04-16 20:12:07] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:12:52] Seen 16415 samples
[2022-04-16 20:12:52] Starting data epoch 545 in logical epoch 545
[2022-04-16 20:12:52] [data] Shuffling data
[2022-04-16 20:12:52] [data] Done reading 16,415 sentences
[2022-04-16 20:12:52] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:13:38] Seen 16415 samples
[2022-04-16 20:13:38] Starting data epoch 546 in logical epoch 546
[2022-04-16 20:13:38] [data] Shuffling data
[2022-04-16 20:13:38] [data] Done reading 16,415 sentences
[2022-04-16 20:13:38] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:14:23] Seen 16415 samples
[2022-04-16 20:14:23] Starting data epoch 547 in logical epoch 547
[2022-04-16 20:14:23] [data] Shuffling data
[2022-04-16 20:14:23] [data] Done reading 16,415 sentences
[2022-04-16 20:14:23] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:15:08] Seen 16415 samples
[2022-04-16 20:15:08] Starting data epoch 548 in logical epoch 548
[2022-04-16 20:15:08] [data] Shuffling data
[2022-04-16 20:15:08] [data] Done reading 16,415 sentences
[2022-04-16 20:15:09] [data] Done shuffling 16,415 sentences to temp files
[2022-04-16 20:15:43] Ep. 548 : Up. 55000 : Sen. 12,640 : Cost 1.32756233 * 1,177,019 @ 2,488 after 129,583,503 : Time 226.34s : 5200.15 words/s : L.r. 1.6181e-04
[2022-04-16 20:15:43] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.npz.orig.npz
[2022-04-16 20:15:44] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.iter55000.npz
[2022-04-16 20:15:44] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.npz
[2022-04-16 20:15:45] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.npz.optimizer.npz
[2022-04-16 20:15:50] [valid] Ep. 548 : Up. 55000 : cross-entropy : 10.7242 : stalled 10 times (last best: 9.8527)
[2022-04-16 20:15:53] [valid] Ep. 548 : Up. 55000 : perplexity : 2.09382 : stalled 10 times (last best: 1.97178)
[2022-04-16 20:16:11] [valid] Ep. 548 : Up. 55000 : bleu : 87.0626 : new best
[2022-04-16 20:16:11] Training finished
[2022-04-16 20:16:12] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.npz.orig.npz
[2022-04-16 20:16:13] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.npz
[2022-04-16 20:16:14] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy/model0-brmt2my.npz.optimizer.npz

real	423m28.423s
user	692m44.713s
sys	0m50.495s
```

output model တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy$ ls *.npz | sort -V
model0-brmt2my.iter5000.npz
model0-brmt2my.iter10000.npz
model0-brmt2my.iter15000.npz
model0-brmt2my.iter20000.npz
model0-brmt2my.iter25000.npz
model0-brmt2my.iter30000.npz
model0-brmt2my.iter35000.npz
model0-brmt2my.iter40000.npz
model0-brmt2my.iter45000.npz
model0-brmt2my.iter50000.npz
model0-brmt2my.iter55000.npz
model0-brmt2my.npz
model0-brmt2my.npz.optimizer.npz
model0-brmt2my.npz.orig.npz
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy$
```

## Testing/Evaluation for Multisource Transdformer, {br,mt_my}--->{my}

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung PE
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Multisource Transformer multi PE Model, {br,mt_my}--->{my}
## 16 April 2022

#model0-brmt2my.iter5000.npz

for i in {5000..55000..5000}
do
   marian-decoder -m ./model0-brmt2my.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.br.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --devices 0 1 --output hyp.iter$i.my --input  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br --input /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my
   echo "Evaluation on ./model0-brmt2my.iter${i}.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:" >> test0-multi-PE-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my < ./hyp.iter$i.my  >> test0-multi-PE-results.txt
done
```

start testing/evaluation ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy$ time ./tran-eval-multi-brmy.sh 
...
...
...
2022-04-16 20:49:00] Best translation 2125 : ကတ္တီပါ နှင့် ။
[2022-04-16 20:49:00] Best translation 2126 : မြန်မာ ဘုရင် ပါ တော်မူ သောအခါ တွင် လည်း ရွှေ ဆီးဖြူ သဘော သို့ ၊ သိမ်ဖွဲ့သေးနုပ် နှင့် လှိမ့် သလို ဟူ၍ မှတ်တမ်းတင် ခဲ့ သည် ။
[2022-04-16 20:49:00] Best translation 2127 : ခွေ ဋ် ခွေး ။
[2022-04-16 20:49:00] Best translation 2128 : ဦးအိ သည် အမရပူရ မြို့ ဖြင်း မှ ပိုး ထည် ၊ ချည် ထည် တို့ ကို အရောင်းအဝယ် ပြု သော ပိုး ကင်ခ်ျ့ ဖြစ်ရာ ပစ္စည်း ဥစ္စာ ကြွယ်ဝ ချမ်းသာ သည် ။
[2022-04-16 20:49:00] Best translation 2129 : ခက်ဆစ် အဖွင့် ။
[2022-04-16 20:49:00] Best translation 2130 : ၃ ။ ဖွာ ရ ရာ = စုစည်း ခြင်း မ ရှိ ၊ ကွဲ ဖျာ ထွက် လျက် ။
[2022-04-16 20:49:00] Best translation 2131 : မိမိ ကိုယ်တိုင် အသံနေအသံထား ဖြင့် ရွတ်ဆို လေ့ကျင့် ပါ ။
[2022-04-16 20:49:00] Best translation 2132 : ( ခ ) တစ်ဥတု လျှင် ------ စီ ကြာမြင့် ပါ သည် ။
[2022-04-16 20:49:00] Best translation 2133 : ညောင်ပင်သာရွာ ဖြူး မြို့နယ် ၁ ၃ ၄ ၅ ခု ၊ တန်ခူး လဆန်း ၁ ရက် သူငယ်ချင်း ဦးဘဇော် သူငယ်ချင်း ထံသို့ ကင်ခ်ျ့ ကင်ခ်ျ့ ပါ သည် ။
[2022-04-16 20:49:00] Best translation 2134 : ၈ ။ အားသန် = မ ရ မ နေ မ ဖြစ် မ နေ အားထုတ် ကြိုးပမ်း သည် ။
[2022-04-16 20:49:00] Best translation 2135 : ပျားရည် သာ ဆောင်ယူ ကြ ချေ ဟု ဆို၍ ပျားရည် ကို ဆောင်ယူ စေ ပြီး သော် ပတ္တမြား ၌ အပေါက်ဝ နှစ် ဖက် ကို လိမ်းသုတ် ပြီး မှ နူးညံ့ သိမ်မွေ့ လှစွာ သော ကမ္ဗလာ ချည် ကြိုး ကို ကျစ် ပြီးလျှင် ထို ကမ္ဗလာ ကြိုး စ ၌ ပျားရည် ဖြင့် ပျားပိတုန်း ကြိုး စ ကို ပတ္တမြား ပေါက် ဝ ကြိုး ဟောင်း စ တစ်ဖက် နှင့် တေ့ ပြီး စဉ်းငယ် ပြီး စဉ်းငယ် ထား ပြီး သော် ပတ္တမြား ဝ က ၊ ပုရွက် စားသောက် စေ ၏ ။
[2022-04-16 20:49:00] Best translation 2136 : ကျွန်တော်တို့ နှင့် ရင်းနှီး သော အကြောင်းအရာ ပင် ဖြစ် လင့် ကစား ၊ ကျွန်တော်တို့ ခေါက်ထည်ကြမ်း မှ မ ရေး ရ ၊ ကျွန်တော်တို့ ကြည့်မြင် ခံစား သလို မ ရေး ရ ၊ ကျောင်း ပြာတာ ကြီး ၏ လာ မှ ရေး ရ မည် ။
[2022-04-16 20:49:00] Best translation 2137 : စကားလုံး ကလေး တွေ စီ ကာ ရယ် ရွတ်ဆို ရေး ကြည့် မယ် ။
[2022-04-16 20:49:00] Best translation 2138 : မမြရင် တို့ အငြိမ့် က သည့် ခေတ် က အုန်းမောင်း မ ပေါ် သေး ပါ အငြိမ့် မင်းသမီးများ သည် ပွဲခင်း ကို ပေါက် အောင် မိမိ ၏ ပင်ကို အသံ နှင့် ကြိုးစား၍ ဆို ကြ ရ သည် ။
[2022-04-16 20:49:00] Best translation 2139 : မှီငြမ်းပြု ဝတ္ထုများ ၊ ဘာသာပြန် ဝတ္ထုများ ဖေဖေါ်ဝါရီ ရာ ပျိုးနုတ်၍ ၊ ဦးစော ၊ ဘူးသီးခြောက် ၊ ရွှေရင်ကြား ၊ ဦးဘဉာဏ် ၊ ဦးငွေကိုင် ၊ သင်ချေ စသည် တို့ မှာ ထင်ရှား သော မှီငြမ်းပြု ဝတ္ထုများ ဖြစ် သည် ။
[2022-04-16 20:49:00] Best translation 2140 : ရှေးခေတ် စစ်သည် တစ် ဦး ၏ ဘဝ တစ် စိတ် တစ် ပိုင်း ကို ထင်ဟပ် သော အိုင်းချင်း ဖြစ် သည် ။
[2022-04-16 20:49:00] Best translation 2141 : လိပ်ပြာ တွင် လည်း အခြား သော ဥပေါသထ ကဲ့သို့ ဦးခေါင်း ပိုင်း ၊ ရင် ပိုင်း ၊ ဝမ်းဗိုက် ပိုင်း ဟူ၍ ရှိ သည် ။
[2022-04-16 20:49:00] Best translation 2142 : ကာတွန်း ဆရာကြီး ဦးဘဂျမ်း ။
[2022-04-16 20:49:00] Best translation 2143 : ဈမျဉ်းဆွဲ ။
[2022-04-16 20:49:00] Best translation 2144 : သွေးတူမွေးတူ နွားများ ကို ချူများ ၊ အဆင်တန်ဆာများ ဆင် ပြီးလျှင် လှည်းယဉ် တွင် ခင်မ မောင်း လေ့ ရှိ သည် ။
[2022-04-16 20:49:00] Best translation 2145 : ရှင် ၊ ခင်ဗျာ ဟု ထူး မှ ယဉ်ကျေးသည် ။
[2022-04-16 20:49:01] Best translation 2146 : ၉ ၃ ၄ ခု တွင် ပေါ်ပေါက် ခဲ့ သော အသားရောင် သည် အရေး တွင် အရေး တွင် ကား မင်းတရားကြီး က ဗညားဒလ အပေါ် တော် ရှိ၍ ချောင်းဦး တွင် ကျေးရွာ တွင် ကျွန် ငါး ယောက် နှင့် ထား တော် မူ သည် ။
[2022-04-16 20:49:01] Best translation 2147 : ၁ ၀ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-16 20:49:01] Best translation 2148 : မောင်ဖိုးစိန် သည် ဇာတ်သဘင်ပညာ ကို အခြေခံ မှ စ၍ သင်ယူ လေ့လာ ခဲ့ သည် ။
[2022-04-16 20:49:01] Best translation 2149 : ရတု ၊ တေးထပ် တို့ တွင် နန်း မူ နန်း ရာ ကို တွေ့ နိုင် သည် ။
[2022-04-16 20:49:01] Best translation 2150 : ဤ အခါ ငတာ က ဘာကြောင့် ပါ လည်း ဘုရား ဟု လျှောက် ရာ ငယ်ထိပ် က နင် မှ စာ မ တတ် ဘဲ နဲ့ ငါ ရေး တဲ့ စာ တွေ ချီးမွမ်း ပါလျှင် ငါ ပါ ပစ်ရ နေ မှာ ပေါ့ ။
[2022-04-16 20:49:01] Best translation 2151 : နေ့တိုင်း မှာ ကား ပုတ်သင်ညို သည် အစာ ရှာ၍ ပြန် သည် ရှိ သော် ဆိတ် သားငယ် တို့ သည် အမိ မျက်နှာ ကို ကြည့် ကုန် လျက် လိုက် သကဲ့သို့ ငါ့ သား ၊ ငါ့ သမီး တို့ သည် မြေမှုန့် အလိမ်းလိမ်း ကပ် သော ကိုယ် ဖြင့် အမိ သို့ ကပ်၍ နေ ၏ ။
[2022-04-16 20:49:01] Best translation 2152 : ဤ ထက် လွန်၍ ဆန်းကြယ် လျောက်ပတ် သော အရာ ကို ကျွန်ုပ် မ တတ် ပြီ ဟု ဆို ၏ ။
[2022-04-16 20:49:01] Best translation 2153 : သူငယ်ချင်း ပေး တဲ့ ပုတ်သင်ညို မူတည် ပြီး ပြန် ရေး ကြ ရအောင် ။
[2022-04-16 20:49:01] Best translation 2154 : ကျွန်ုပ်တို့ သည် ဤ မိတဆိုး ရှင်ပြု ကို အလွန် သနား စေတနာ ရှိ လာ ကြ သည် နှင့် ဦးစံရွှေ နှင့် တိုင်ပင် ကာ အလှူ အိမ် တွင် ည အိပ်၍ တတ် နိုင် သမျှ ကုပ်ကုပ် ဆုံးဖြတ် လိုက် ကြ လေ သည် ။
[2022-04-16 20:49:01] Best translation 2155 : ကြက်ဥ ပြုတ် သည် ။
[2022-04-16 20:49:01] Best translation 2156 : ယခု ပင် အဆိပ် လူး သော မြား ဖြင့် ပစ် သတ် အံ့ ။
[2022-04-16 20:49:01] Best translation 2157 : ဝမ်းသာအားရ ၊ မယား က တစ် သွယ် ။
[2022-04-16 20:49:01] Best translation 2158 : ဝေ ဝေ့ ဝေး ။
[2022-04-16 20:49:01] Best translation 2159 : ပြန်၍ သုံးသပ် ကြည့် ပါ လျှင် မြန်မာ ဘာသာစကား တွင် အရေး အက္ခရာ ရှိ ထား ပြီး ဖြစ် သဖြင့် အရေး နှင့် အဖတ် ဟူ၍ နှစ် မျိုး ရှိ နေ သည် ။
[2022-04-16 20:49:01] Best translation 2160 : ဂြောင် လည်း မ ထိုင် ရ ။
[2022-04-16 20:49:01] Best translation 2161 : ၁ ။ အောက်ပါ စကားလုံး တို့ ၏ အနက် အဓိပ္ပာယ် ကို အဘိဓာန် တွင် ရှာ ပါ ။
[2022-04-16 20:49:01] Best translation 2162 : သင်ခန်းစာ အကျဉ်း ။
[2022-04-16 20:49:01] Best translation 2163 : ချစ်လှစွာ သော သား ။
[2022-04-16 20:49:01] Best translation 2164 : ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
[2022-04-16 20:49:01] Best translation 2165 : ဒူးရင်းသီး ။
[2022-04-16 20:49:01] Best translation 2166 : မိမိ တည် သော ဘုရား ကလအုတ် ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
[2022-04-16 20:49:01] Total time: 65.64190s wall

real	12m40.039s
user	23m17.168s
sys	0m33.355s
```

ရတဲ့ BLEU score တွေကတော့ အောက်ပါအတိုင်းပါ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-multi-brmy$ cat test0-multi-PE-results.txt 
Evaluation on ./model0-brmt2my.iter5000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 85.42, 95.2/90.0/85.4/81.1 (BP=0.973, ratio=0.973, hyp_len=28036, ref_len=28803)
Evaluation on ./model0-brmt2my.iter10000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.27, 95.2/90.3/85.9/81.7 (BP=0.979, ratio=0.979, hyp_len=28204, ref_len=28803)
Evaluation on ./model0-brmt2my.iter15000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.23, 95.2/90.4/86.0/81.9 (BP=0.978, ratio=0.978, hyp_len=28165, ref_len=28803)
Evaluation on ./model0-brmt2my.iter20000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.33, 95.2/90.4/86.0/81.9 (BP=0.978, ratio=0.978, hyp_len=28179, ref_len=28803)
Evaluation on ./model0-brmt2my.iter25000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.40, 95.2/90.3/86.0/81.8 (BP=0.980, ratio=0.980, hyp_len=28227, ref_len=28803)
Evaluation on ./model0-brmt2my.iter30000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.81, 95.2/90.3/85.9/81.8 (BP=0.985, ratio=0.985, hyp_len=28364, ref_len=28803)
Evaluation on ./model0-brmt2my.iter35000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.80, 95.2/90.4/86.0/81.8 (BP=0.984, ratio=0.984, hyp_len=28349, ref_len=28803)
Evaluation on ./model0-brmt2my.iter40000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.77, 95.2/90.3/85.9/81.8 (BP=0.985, ratio=0.985, hyp_len=28364, ref_len=28803)
Evaluation on ./model0-brmt2my.iter45000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 86.76, 95.2/90.3/85.9/81.8 (BP=0.984, ratio=0.984, hyp_len=28356, ref_len=28803)
Evaluation on ./model0-brmt2my.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 87.14, 94.6/89.5/85.0/80.9 (BP=0.998, ratio=0.998, hyp_len=28733, ref_len=28803)
Evaluation on ./model0-brmt2my.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 87.19, 94.6/89.6/85.1/81.0 (BP=0.997, ratio=0.997, hyp_len=28721, ref_len=28803)
```

Best model နဲ့ best BLEU score က အောက်ပါအတိုင်းပါ...  

```
Evaluation on ./model0-brmt2my.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Multisource Transformer multi-source PE Model:
BLEU = 87.19, 94.6/89.6/85.1/81.0 (BP=0.997, ratio=0.997, hyp_len=28721, ref_len=28803)
```

ခုချိန်ထိ လုပ်ပြီးသလောက် PE experiment တွေကို နှိုင်းယှဉ်ကြည့်ရင် အောက်ပါအတိုင်း...  

<div align="center">  
 
Table 2. Performance comparison between Transformer, Transformer-PE_Transformer and Multisource Transformer  

| Transformer | Post-Editing | Multisource Transformer |
|----------:|----------:|----------:|
| 87.54 | 87.25 | 87.19 |

 </div>  
 
## Training Shared Multisource Transformer {br,mt_my}--->{my}

shared multisource architecture နဲ့ training လုပ်ဖို့အတွက်က အရင်ဆုံး vocab ကို ပေါင်းပြီး ဆောက်ရမယ်။  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ cat /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000-trainingdata.my > /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br-train.mtmy
(base) ye@:/media/ye/project2/exp/braille-nmt$ marian-vocab < /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br-train.mtmy > /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.br-train.mtmy.yml
[2022-04-16 21:01:59] Creating vocabulary...
[2022-04-16 21:01:59] [data] Creating vocabulary stdout from stdin
[2022-04-16 21:01:59] Finished
(base) ye@:/media/ye/project2/exp/braille-nmt$
```

shared multisource transformer မော်ဒယ်နဲ့ training လုပ်ဖို့အတွက် bash shell script (shared-multi-transformer-pe-brmt2my.sh) ကို အောက်ပါအတိုင်း ပြင်ဆင်ခဲ့...  

```bash
#!/bin/bash

## Written by Ye Kyaw Thu, LST, NECTEC, Thailand
## Experiments for shared multisource Transformer {br,mt_my}--->{my}
## 16 April 2022

# ဘာတွေထပ်ဖြည့်ခဲ့သလဲ ဆိုရင်
# running folder နာမည် ပြောင်းပြီး
# --type shared-multi-transformer
# --train-sets မှာ {source,mt,target} ထား
# --vocabs မှာလည်း {source,mt,target} ပေးခဲ့
# --valid-sets မှာလည်း {source,mt,target} ပေးခဲ့
# Error: Requested shape shape=18364x512 size=9402368 for existing parameter 'Wemb' does not match original shape ... ဆိုတဲ့ error ပေးတာကြောင့်
# vocab ကို source+mt (သို့) br+mt_my ကို ပေါင်းဆောက်ခဲ့ပြီးမှ run လို့ အဆင်ပြေတယ်။  

mkdir model.transformer-shared-multi-brmy;

marian \
    --model  /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.npz --type shared-multi-transformer \
    --train-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000-trainingdata.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my \
    --max-length 200 \
    --vocabs /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.br-train.mtmy.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.br-train.mtmy.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml \
    --mini-batch-fit -w 1000 --maxi-batch 100 \
    --early-stopping 10 \
    --valid-freq 5000 --save-freq 5000 --disp-freq 500 \
    --valid-metrics cross-entropy perplexity bleu \
    --valid-sets /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000-devdata.my /media/ye/project2/exp/braille-nmt/data/for-nmt/0/dev.my \
    --valid-translation-output /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/dev.multi-brmy.output --quiet-translation \
    --valid-mini-batch 64 \
    --beam-size 6 --normalize 0.6 \
    --log ./model.transformer-shared-multi-brmy/train-shared-multi-brmy.log --valid-log ./model.transformer-shared-multi-brmy/valid-shared-multi-brmy.log \
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
    --dump-config > /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/config-shared-multi-brmy0.yml
    
time marian -c /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/config-shared-multi-brmy0.yml  2>&1 | tee transformer-shared-multi-brmy0.log
```

training လုပ်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt$ ./shared-multi-transformer-pe-brmt2my.sh 
...
...
...
[2022-04-17 06:21:11] [data] Shuffling data
[2022-04-17 06:21:11] [data] Done reading 16,415 sentences
[2022-04-17 06:21:11] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:21:54] Seen 16415 samples
[2022-04-17 06:21:54] Starting data epoch 735 in logical epoch 735
[2022-04-17 06:21:54] [data] Shuffling data
[2022-04-17 06:21:54] [data] Done reading 16,415 sentences
[2022-04-17 06:21:54] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:22:37] Seen 16415 samples
[2022-04-17 06:22:37] Starting data epoch 736 in logical epoch 736
[2022-04-17 06:22:37] [data] Shuffling data
[2022-04-17 06:22:37] [data] Done reading 16,415 sentences
[2022-04-17 06:22:37] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:23:21] Seen 16415 samples
[2022-04-17 06:23:21] Starting data epoch 737 in logical epoch 737
[2022-04-17 06:23:21] [data] Shuffling data
[2022-04-17 06:23:21] [data] Done reading 16,415 sentences
[2022-04-17 06:23:21] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:24:04] Seen 16415 samples
[2022-04-17 06:24:04] Starting data epoch 738 in logical epoch 738
[2022-04-17 06:24:04] [data] Shuffling data
[2022-04-17 06:24:04] [data] Done reading 16,415 sentences
[2022-04-17 06:24:04] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:24:05] Ep. 738 : Up. 74000 : Sen. 352 : Cost 1.32262504 * 1,174,385 @ 3,204 after 174,358,440 : Time 214.76s : 5468.39 words/s : L.r. 1.3950e-04
[2022-04-17 06:24:47] Seen 16415 samples
[2022-04-17 06:24:47] Starting data epoch 739 in logical epoch 739
[2022-04-17 06:24:47] [data] Shuffling data
[2022-04-17 06:24:47] [data] Done reading 16,415 sentences
[2022-04-17 06:24:47] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:25:30] Seen 16415 samples
[2022-04-17 06:25:30] Starting data epoch 740 in logical epoch 740
[2022-04-17 06:25:30] [data] Shuffling data
[2022-04-17 06:25:30] [data] Done reading 16,415 sentences
[2022-04-17 06:25:30] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:26:13] Seen 16415 samples
[2022-04-17 06:26:13] Starting data epoch 741 in logical epoch 741
[2022-04-17 06:26:13] [data] Shuffling data
[2022-04-17 06:26:13] [data] Done reading 16,415 sentences
[2022-04-17 06:26:13] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:26:56] Seen 16415 samples
[2022-04-17 06:26:56] Starting data epoch 742 in logical epoch 742
[2022-04-17 06:26:56] [data] Shuffling data
[2022-04-17 06:26:56] [data] Done reading 16,415 sentences
[2022-04-17 06:26:56] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:27:39] Ep. 742 : Up. 74500 : Sen. 16,415 : Cost 1.32238007 * 1,177,984 @ 2,962 after 175,536,424 : Time 214.35s : 5495.64 words/s : L.r. 1.3903e-04
[2022-04-17 06:27:39] Seen 16415 samples
[2022-04-17 06:27:39] Starting data epoch 743 in logical epoch 743
[2022-04-17 06:27:39] [data] Shuffling data
[2022-04-17 06:27:39] [data] Done reading 16,415 sentences
[2022-04-17 06:27:39] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:28:22] Seen 16415 samples
[2022-04-17 06:28:22] Starting data epoch 744 in logical epoch 744
[2022-04-17 06:28:22] [data] Shuffling data
[2022-04-17 06:28:22] [data] Done reading 16,415 sentences
[2022-04-17 06:28:22] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:29:05] Seen 16415 samples
[2022-04-17 06:29:05] Starting data epoch 745 in logical epoch 745
[2022-04-17 06:29:05] [data] Shuffling data
[2022-04-17 06:29:05] [data] Done reading 16,415 sentences
[2022-04-17 06:29:05] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:29:48] Seen 16415 samples
[2022-04-17 06:29:48] Starting data epoch 746 in logical epoch 746
[2022-04-17 06:29:48] [data] Shuffling data
[2022-04-17 06:29:48] [data] Done reading 16,415 sentences
[2022-04-17 06:29:48] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:30:32] Seen 16415 samples
[2022-04-17 06:30:32] Starting data epoch 747 in logical epoch 747
[2022-04-17 06:30:32] [data] Shuffling data
[2022-04-17 06:30:32] [data] Done reading 16,415 sentences
[2022-04-17 06:30:32] [data] Done shuffling 16,415 sentences to temp files
[2022-04-17 06:31:13] Ep. 747 : Up. 75000 : Sen. 16,227 : Cost 1.32205176 * 1,177,497 @ 1,427 after 176,713,921 : Time 214.23s : 5496.44 words/s : L.r. 1.3856e-04
[2022-04-17 06:31:13] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.npz.orig.npz
[2022-04-17 06:31:14] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.iter75000.npz
[2022-04-17 06:31:14] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.npz
[2022-04-17 06:31:16] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.npz.optimizer.npz
[2022-04-17 06:31:23] [valid] Ep. 747 : Up. 75000 : cross-entropy : 9.26205 : stalled 10 times (last best: 9.16809)
[2022-04-17 06:31:26] [valid] Ep. 747 : Up. 75000 : perplexity : 1.89314 : stalled 10 times (last best: 1.88092)
[2022-04-17 06:31:43] [valid] Ep. 747 : Up. 75000 : bleu : 87.3114 : new best
[2022-04-17 06:31:44] Training finished
[2022-04-17 06:31:44] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.npz.orig.npz
[2022-04-17 06:31:45] Saving model weights and runtime parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.npz
[2022-04-17 06:31:46] Saving Adam parameters to /media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy/model0-mtmy.npz.optimizer.npz

real	550m42.315s
user	914m16.723s
sys	1m3.831s
```

## Testing/Evaluation Shared Multisource Transformer {br,mt_my}--->{my}

bash script (tran-eval-shared-multi-brmy.sh) က အောက်ပါအတိုင်း...  

```bash
#!/bin/bash

## Preparation for Myanmar-MuHaung PE
## Written by Ye, LST, NECTEC, Thailand
## Translation and Evaluation with Marian, Shared Multisource Transformer PE Model, {br,mt_my}--->{my}
## 17 April 2022

#model0-mtmy.iter5000.npz

for i in {5000..75000..5000}
do
   marian-decoder -m ./model0-mtmy.iter$i.npz -v /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.br-train.mtmy.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/train.br-train.mtmy.yml /media/ye/project2/exp/braille-nmt/data/for-nmt/0/vocab/vocab.my.yml --devices 0 1 --output hyp.iter$i.my --input  /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br --input /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my
   echo "Evaluation on ./model0-mtmy.iter${i}.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:" >> test0-shared-multi-PE-results.txt
   perl ~/tool/mosesbin/ubuntu-17.04/moses/scripts/generic/multi-bleu.perl /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.my < ./hyp.iter$i.my  >> test0-shared-multi-PE-results.txt
done
```

testing and evaluation ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy$ time ./tran-eval-shared-multi-brmy.sh | tee ./tran-eval.log
...
...
...
[2022-04-17 11:47:27] Best translation 2140 : ရှေးခေတ် စစ်သည် တစ် ဦး ၏ ဘဝ တစ် စိတ် တစ် ပိုင်း ကို ထင်ဟပ် သော အိုင်းချင်း ဖြစ် သည် ။
[2022-04-17 11:47:27] Best translation 2141 : လိပ်ပြာ တွင် လည်း အခြား သော ဥပေါသထ ကဲ့သို့ ဦးခေါင်း ပိုင်း ၊ ရင် ပိုင်း ၊ ဝမ်းဗိုက် ပိုင်း ဟူ၍ ရှိ သည် ။
[2022-04-17 11:47:27] Best translation 2142 : ကာတွန်း ဆရာကြီး ဦးဘဂျမ်း ။
[2022-04-17 11:47:27] Best translation 2143 : ဈမျဉ်းဆွဲ ။
[2022-04-17 11:47:27] Best translation 2144 : သွေးတူမွေးတူ နွားများ ကို ချူများ ၊ အဆင်တန်ဆာများ ဆင် ပြီးလျှင် လှည်းယဉ် တွင် ခင်မ မောင်း လေ့ ရှိ သည် ။
[2022-04-17 11:47:27] Best translation 2145 : ရှင် ၊ ခင်ဗျာ ဟု ထူး မှ ယဉ်ကျေးသည် ။
[2022-04-17 11:47:28] Best translation 2146 : ၉ ၃ ၄ ခု တွင် ပေါ်ပေါက် ခဲ့ သော အသားရောင် သည် အရေး တွင် အရေး တွင် မင်းတရားကြီး က ဗညားဒလ အပေါ် အမျက် တော် ရှိ၍ တော် ရှိ၍ ယိုးဒယား ကျေးရွာ တွင် ကျွန် ငါး ယောက် နှင့် ထား တော် မူ သည် ။
[2022-04-17 11:47:28] Best translation 2147 : ၁ ၀ ။ ဝါသနာ = စွဲမြဲ နေ သော အလေ့အကျင့် ။
[2022-04-17 11:47:28] Best translation 2148 : မောင်ဖိုးစိန် သည် ဇာတ်သဘင်ပညာ ကို အခြေခံ မှ စ၍ သင်ယူ လေ့လာ ခဲ့ သည် ။
[2022-04-17 11:47:28] Best translation 2149 : ရတု ၊ တေးထပ် တို့ တွင် နန်း မူ နန်း ရာ ကို တွေ့ နိုင် သည် ။
[2022-04-17 11:47:28] Best translation 2150 : ဤ အခါ ငတာ က ဘာကြောင့် ပါ လည်း ဘုရား ဟု လျှောက် ရာ ငယ်ထိပ် က နင် မှ စာ မ တတ် ဘဲ နဲ့ ငါ ရေး တဲ့ စာ တွေ ချီးမွမ်း ပါလျှင် ငါ ပါ ပစ်ရ နေ မှာ ပေါ့ ။
[2022-04-17 11:47:28] Best translation 2151 : နေ့တိုင်း မှာ ကား ပုတ်သင်ညို သည် အစာ ရှာ၍ ပြန် သည် ရှိ သော် ဆိတ် သားငယ် တို့ သည် အမိ မျက်နှာ ကို ကြည့် ကုန် လျက် လိုက် သကဲ့သို့ ငါ့ သား ၊ ငါ့ သမီး တို့ သည် မြေမှုန့် အလိမ်းလိမ်း ကပ် သော ကိုယ် ဖြင့် အမိ သို့ ကပ်၍ နေ ၏ ။
[2022-04-17 11:47:28] Best translation 2152 : ဤ ထက် လွန်၍ ဆန်းကြယ် လျောက်ပတ် သော အရာ ကို ကျွန်ုပ် မ တတ် ပြီ ဟု ဆို ၏ ။
[2022-04-17 11:47:28] Best translation 2153 : သူငယ်ချင်း ပေး တဲ့ ပုတ်သင်ညို မူတည် ပြီး ပြန် ရေး ကြ ရအောင် ။
[2022-04-17 11:47:28] Best translation 2154 : ကျွန်ုပ်တို့ သည် ဤ မိတဆိုး ရှင်ပြု ကို အလွန် သနား စေတနာ ရှိ လာ ကြ သည် နှင့် ဦးစံရွှေ နှင့် တိုင်ပင် ကာ အလှူ အိမ် တွင် ည အိပ်၍ တတ် နိုင် သမျှ ကုပ်ကုပ် ဆုံးဖြတ် လိုက် ကြ လေ သည် ။
[2022-04-17 11:47:28] Best translation 2155 : ကြက်ဥ ပြုတ် သည် ။
[2022-04-17 11:47:28] Best translation 2156 : ယခု ပင် အဆိပ် လူး သော မြား ဖြင့် ပစ် သတ် အံ့ ။
[2022-04-17 11:47:28] Best translation 2157 : ဝမ်းသာအားရ ၊ မယား က တစ် သွယ် ။
[2022-04-17 11:47:28] Best translation 2158 : ဝေ ဝေ့ ဝေး ။
[2022-04-17 11:47:28] Best translation 2159 : ပြန်၍ သုံးသပ် ကြည့် ပါ လျှင် မြန်မာ ဘာသာစကား တွင် အရေး အက္ခရာ ရှိ ထား ပြီး ဖြစ် သဖြင့် အရေး နှင့် အဖတ် ဟူ၍ နှစ် မျိုး ရှိ နေ သည် ။
[2022-04-17 11:47:28] Best translation 2160 : ဂြောင် လည်း မ ထိုင် ရ ။
[2022-04-17 11:47:28] Best translation 2161 : ၁ ။ အောက်ပါ စကားလုံး တို့ ၏ အနက် အဓိပ္ပာယ် ကို အဘိဓာန် တွင် ရှာ ပါ ။
[2022-04-17 11:47:28] Best translation 2162 : သင်ခန်းစာ အကျဉ်း ။
[2022-04-17 11:47:28] Best translation 2163 : ချစ်လှစွာ သော သား ။
[2022-04-17 11:47:28] Best translation 2164 : ဟို ရှေ့ က ဆူညံ ဆူညံ ၊ ဘာ သံ လို့ မေး ။
[2022-04-17 11:47:28] Best translation 2165 : ဒူးရင်းသီး ။
[2022-04-17 11:47:28] Best translation 2166 : မိမိ တည် သော ဘုရား ကလအုတ် ၊ လှူ ခဲ့ သော ကျွန် နှင့် ဝတ္ထု ပစ္စည်း အစုစု ကို နှောင်းလူ တို့ ဖျက်ဆီး နှိပ်စက် မည့် ရန် မှ ကာကွယ် လို ခြင်း ဖြစ် သည် ။
[2022-04-17 11:47:28] Total time: 65.96936s wall

real	17m23.519s
user	32m7.712s
sys	0m44.331s
```

train လုပ်ထားတဲ့ မော်ဒယ်တွေအတွက် BLEU score တွေက အောက်ပါအတိုင်း...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy$ cat test0-shared-multi-PE-results.txt 
Evaluation on ./model0-mtmy.iter5000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 85.50, 95.0/90.1/85.7/81.5 (BP=0.973, ratio=0.973, hyp_len=28023, ref_len=28803)
Evaluation on ./model0-mtmy.iter10000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 85.84, 95.3/90.5/86.2/82.1 (BP=0.971, ratio=0.972, hyp_len=27989, ref_len=28803)
Evaluation on ./model0-mtmy.iter15000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 86.19, 95.4/90.7/86.4/82.3 (BP=0.973, ratio=0.974, hyp_len=28045, ref_len=28803)
Evaluation on ./model0-mtmy.iter20000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 86.55, 95.3/90.5/86.2/82.1 (BP=0.979, ratio=0.980, hyp_len=28214, ref_len=28803)
Evaluation on ./model0-mtmy.iter25000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 86.57, 95.3/90.5/86.2/82.1 (BP=0.979, ratio=0.980, hyp_len=28218, ref_len=28803)
Evaluation on ./model0-mtmy.iter30000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 86.57, 95.3/90.5/86.2/82.1 (BP=0.980, ratio=0.980, hyp_len=28221, ref_len=28803)
Evaluation on ./model0-mtmy.iter35000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 86.56, 95.3/90.5/86.2/82.1 (BP=0.979, ratio=0.979, hyp_len=28211, ref_len=28803)
Evaluation on ./model0-mtmy.iter40000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 86.74, 95.2/90.4/86.0/81.9 (BP=0.983, ratio=0.983, hyp_len=28311, ref_len=28803)
Evaluation on ./model0-mtmy.iter45000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 86.58, 95.3/90.5/86.2/82.1 (BP=0.980, ratio=0.980, hyp_len=28231, ref_len=28803)
Evaluation on ./model0-mtmy.iter50000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 87.42, 95.2/90.2/85.8/81.7 (BP=0.993, ratio=0.993, hyp_len=28590, ref_len=28803)
Evaluation on ./model0-mtmy.iter55000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 87.43, 95.2/90.3/85.9/81.7 (BP=0.992, ratio=0.992, hyp_len=28585, ref_len=28803)
Evaluation on ./model0-mtmy.iter60000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 87.45, 95.1/90.2/85.8/81.6 (BP=0.993, ratio=0.993, hyp_len=28604, ref_len=28803)
Evaluation on ./model0-mtmy.iter65000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 87.45, 95.1/90.2/85.8/81.7 (BP=0.993, ratio=0.993, hyp_len=28596, ref_len=28803)
Evaluation on ./model0-mtmy.iter70000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 87.48, 95.1/90.2/85.9/81.7 (BP=0.993, ratio=0.993, hyp_len=28598, ref_len=28803)
Evaluation on ./model0-mtmy.iter75000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 87.50, 95.1/90.2/85.8/81.7 (BP=0.994, ratio=0.994, hyp_len=28625, ref_len=28803)
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy$
```

Best model နဲ့ best score က အောက်ပါအတိုင်း...  

```
Evaluation on ./model0-mtmy.iter75000.npz with /media/ye/project2/exp/braille-nmt/data/for-nmt/0/test.br /media/ye/project2/exp/braille-nmt/model.transformer-brmy/hyp.iter80000.my, Shared Multisource Transformer PE Model:
BLEU = 87.50, 95.1/90.2/85.8/81.7 (BP=0.994, ratio=0.994, hyp_len=28625, ref_len=28803)
```

ခုချိန်ထိလုပ်ခဲ့တဲ့ မြန်မာကနေ မူဟောင်း၊ မူဟောင်းကနေ မြန်မာစာ ဘာသာပြန်တဲ့ expeirment တွေအားလုံးကို နှိုင်းယှဉ်ကြည့်ရင်...  

<div align="center">

Table 1. Performance comparison for Transformer, Transformer-PE_Transformer, Multisource-Transformer and Shared Multisource Transformer
 
|src-trg| Transformer | Transformer-PE_Transformer | Multisource Transformer | Shared Multisource Transformer |
|----------:|----------:|----------:|----------:|----------:|   
| my-br | 86.73 | 86.26 | 86.42 | 86.72 | 
| br-my | 87.54 | 87.25 | 87.19 | 87.50 | 

 </div>

PE experiment ရလဒ်တွေအားလုံးက comparable ပဲ ရတယ်။ Transformer baseline ကို မကျော်နိုင်ဘူး ဖြစ်နေသေးတယ်။  

## To Do

လက်ရှိ word segmentation က အောက်ပါအတိုင်း word level unit နဲ့ပဲသွားထားတာမို့ ...  

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy$ head /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.my
၄ ။ အောက်ပါ မေးခွန်းများ ကို ဖြေဆို ပါ ။
အဲဒီ မှာ ကိုရွှေ ဗျည်း တို့ မသရ တို့ ရှိ ကြ တယ် လေ ။
စစ် မှာ ယွန်းမ ။
ဆ ။
တံခွန်တိုင် ရွှေကုက္ကား နဲ့ ဘုရား ကို မြင် ။
ဥ ကုန် သော် ဟင်္သာ ငယ် တို့ ကို နောက် ဟင်္သာ အို တို့ ကို အစဉ် အတိုင်း စား ကြ လေ ၏ ။
ဦးပေါင်း ကျား နှင့် မြင်းကျား ရှင် ။
သူငယ် အမိ လည်း ငါ့ သား ကို ယူ၍ အဘယ် သို့ သွား မည်နည်း ဟု လိုက် လျက် ဘီလူးမ ကို ကိုင် ဆွဲ ၏ ။
ရွှေ အိမ် နန်း နှင့် ကြငှန်း လည်း ခံ မတ် ပေါင်းရံ လျက် ပျော်စံ ရိပ်ငြိမ် စည်းစိမ် မကွာ ။
မြန်မာ ဘာသာ ကား အိမ် ထန်းပင် ဟု ခေါ်ဝေါ် ကုန် ၏ ။
```

```
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy$ head /media/ye/project2/exp/braille-nmt/data/for-nmt/0/train.br
⠼⠙ ⠲ ⠴⠏ ⠍⠱⠆⠨⠥⠝⠆⠾ ⠅ ⠿⠓⠱⠈⠕ ⠏ ⠲
⠮⠆⠙⠪ ⠰⠣⠁ ⠅⠕⠩⠺⠱ ⠃⠽⠪⠆ ⠚ ⠍⠣⠹⠣⠗⠣ ⠚ ⠩ ⠟ ⠞⠮ ⠇⠱ ⠲
⠎⠭ ⠰⠣⠁ ⠽⠥⠝⠆⠍⠣ ⠲
⠈⠣ ⠲
⠞⠋⠨⠥⠝⠞⠖ ⠩⠺⠱⠅⠦⠅⠁⠆ ⠝⠮⠂ ⠿ ⠅ ⠾⠔ ⠲
⠥⠂ ⠅⠉ ⠧ ⠓⠔⠹⠁ ⠌⠮ ⠚ ⠅ ⠱⠴ ⠓⠔⠹⠁ ⠕ ⠚ ⠅ ⠣⠎ ⠣⠞⠖⠆ ⠎⠁⠆ ⠟ ⠃ ⠊ ⠲
⠥⠆⠏⠶⠆ ⠟⠁⠆ ⠗ ⠾⠔⠆⠟⠁⠆ ⠩⠔ ⠲
⠹⠥⠌⠮ ⠣⠍⠊ ⠇⠆ ⠌⠣ ⠹⠁⠆ ⠅ ⠽⠥⠯ ⠣⠃⠮ ⠙ ⠹⠺⠁⠆ ⠍⠝ ⠓ ⠇⠬ ⠑ ⠃⠪⠇⠥⠆⠍⠣ ⠅ ⠅⠖ ⠈⠺⠮⠆ ⠊ ⠲
⠩⠺⠱ ⠱⠝ ⠝⠋⠆ ⠗ ⠟⠣⠓⠌⠋⠆ ⠇⠆ ⠨⠋ ⠍⠣⠞ ⠏⠶⠆⠗⠋ ⠑ ⠿⠻⠎⠋ ⠗⠱⠅⠷⠢ ⠎⠪⠆⠎⠢ ⠍⠣⠅⠺⠁ ⠲
⠾⠋⠍⠁ ⠃⠁⠹⠁ ⠅⠁⠆ ⠱⠝ ⠁⠋⠆⠏⠔ ⠓ ⠨⠻⠺⠻ ⠅⠉ ⠊ ⠲
(base) ye@:/media/ye/project2/exp/braille-nmt/model.transformer-shared-multi-brmy$
```

- syllable level unit နဲ့ ပြောင်းပြီး NMT လုပ်ရင် အပြောင်းအလဲတော့ ရှိလာနိုင်တယ်
- sequence2sequence model တွေကို training လုပ်ကြည့်ရန်
- model ensemble approach နဲ့ performance ကို တိုးမလား experiment ဆက်လုပ်ရန်

