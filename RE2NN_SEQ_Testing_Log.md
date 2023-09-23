# RE2NN SEQ Testing Log

## git clone

(base) ye@lst-gpu-3090:~/exp$ git clone https://github.com/jeffchy/RE2NN-SEQ
Cloning into 'RE2NN-SEQ'...
remote: Enumerating objects: 112, done.
remote: Counting objects: 100% (112/112), done.
remote: Compressing objects: 100% (92/92), done.
remote: Total 112 (delta 20), reused 90 (delta 12), pack-reused 0
Receiving objects: 100% (112/112), 1.55 MiB | 631.00 KiB/s, done.
Resolving deltas: 100% (20/20), done.
(base) ye@lst-gpu-3090:~/exp$

## Create New Conda Env

(base) ye@lst-gpu-3090:~/exp$ conda create --name re2nn_seq python=3.8
...
...
...
  wheel              pkgs/main/linux-64::wheel-0.38.4-py38h06a4308_0
  xz                 pkgs/main/linux-64::xz-5.4.2-h5eee18b_0
  zlib               pkgs/main/linux-64::zlib-1.2.13-h5eee18b_0


Proceed ([y]/n)? y


Downloading and Extracting Packages
python-3.8.18        | 25.3 MB   | ######################################################## | 100%
openssl-3.0.11       | 5.2 MB    | ######################################################## | 100%
ca-certificates-2023 | 123 KB    | ######################################################## | 100%
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate re2nn_seq
#
# To deactivate an active environment, use
#
#     $ conda deactivate

(base) ye@lst-gpu-3090:~/exp$

## Activate

(base) ye@lst-gpu-3090:~/exp$ conda activate re2nn_seq
(re2nn_seq) ye@lst-gpu-3090:~/exp$

## Check the requirements.txt

(re2nn_seq) ye@lst-gpu-3090:~/exp$ cd RE2NN-SEQ/
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ$ cd src_seq/
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ ls
analysis                  load_data_and_rules.py  test.py                 utils.py
baselines                 main.py                 tools                   val_ptm.py
create_logic_mat_bias.py  metrics                 train_baseline_ptm.py   val.py
data.py                   ptm                     train_baseline.py       wfa
farnn                     RE.py                   train_decompose_ptm.py
init_params.py            requirements.txt        train_decompose.py
__init__.py               rule_utils              train_onehot.py
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ cat requirements.txt
-e git+https://github.com/tensorly/tensorly@dc67ac6353e2d97dc516671dd9e64d254fa495b5#egg=tensorly
torch==1.3.1
automata-tools==2.0.1
tqdm(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

## Installation of Requirements

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ pip install -r requirements.txt
Obtaining tensorly from git+https://github.com/tensorly/tensorly@dc67ac6353e2d97dc516671dd9e64d254fa495b5#egg=tensorly (from -r requirements.txt (line 1))
  Cloning https://github.com/tensorly/tensorly (to revision dc67ac6353e2d97dc516671dd9e64d254fa495b5) to ./src/tensorly
  Running command git clone --filter=blob:none --quiet https://github.com/tensorly/tensorly /home/ye/exp/RE2NN-SEQ/src_seq/src/tensorly
  Running command git rev-parse -q --verify 'sha^dc67ac6353e2d97dc516671dd9e64d254fa495b5'
  Running command git fetch -q https://github.com/tensorly/tensorly dc67ac6353e2d97dc516671dd9e64d254fa495b5
  Running command git checkout -q dc67ac6353e2d97dc516671dd9e64d254fa495b5
  Resolved https://github.com/tensorly/tensorly to commit dc67ac6353e2d97dc516671dd9e64d254fa495b5
  Preparing metadata (setup.py) ... done
ERROR: Could not find a version that satisfies the requirement torch==1.3.1 (from versions: 1.4.0, 1.5.0, 1.5.1, 1.6.0, 1.7.0, 1.7.1, 1.8.0, 1.8.1, 1.9.0, 1.9.1, 1.10.0, 1.10.1, 1.10.2, 1.11.0, 1.12.0, 1.12.1, 1.13.0, 1.13.1, 2.0.0, 2.0.1)
ERROR: No matching distribution found for torch==1.3.1
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

Got ERROR as shown above!!

Original source က run ထားတဲ့ environment/condition နဲ့ သိပ်မကွာအောင် torch ကို 1.4.0 နဲ့ပဲ install လုပ်ကြည့်ခဲ့ ...  

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ pip install -r requirements.txt
Obtaining tensorly from git+https://github.com/tensorly/tensorly@dc67ac6353e2d97dc516671dd9e64d254fa495b5#egg=tensorly (from -r requirements.txt (line 1))
  Skipping because already up-to-date.
  Preparing metadata (setup.py) ... done
Collecting torch==1.4.0 (from -r requirements.txt (line 3))
  Downloading torch-1.4.0-cp38-cp38-manylinux1_x86_64.whl (753.4 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 753.4/753.4 MB 2.4 MB/s eta 0:00:00
Collecting automata-tools==2.0.1 (from -r requirements.txt (line 4))
  Downloading automata_tools-2.0.1-py3-none-any.whl (12 kB)
Collecting tqdm (from -r requirements.txt (line 5))
  Obtaining dependency information for tqdm from https://files.pythonhosted.org/packages/00/e5/f12a80907d0884e6dff9c16d0c0114d81b8cd07dc3ae54c5e962cc83037e/tqdm-4.66.1-py3-none-any.whl.metadata
  Using cached tqdm-4.66.1-py3-none-any.whl.metadata (57 kB)
Collecting numpy (from tensorly->-r requirements.txt (line 1))
  Obtaining dependency information for numpy from https://files.pythonhosted.org/packages/98/5d/5738903efe0ecb73e51eb44feafba32bdba2081263d40c5043568ff60faf/numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata
  Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.6 kB)
Collecting scipy (from tensorly->-r requirements.txt (line 1))
  Using cached scipy-1.10.1-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (34.5 MB)
Collecting nose (from tensorly->-r requirements.txt (line 1))
  Downloading nose-1.3.7-py3-none-any.whl (154 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 154.7/154.7 kB 3.9 MB/s eta 0:00:00
Using cached tqdm-4.66.1-py3-none-any.whl (78 kB)
Using cached numpy-1.24.4-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (17.3 MB)
Installing collected packages: nose, tqdm, torch, numpy, automata-tools, scipy, tensorly
  Running setup.py develop for tensorly
Successfully installed automata-tools-2.0.1 nose-1.3.7 numpy-1.24.4 scipy-1.10.1 tensorly-0.4.5 torch-1.4.0 tqdm-4.66.1
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

ဒီတစ်ခါတော့ requirements installation OK!!

## Download Data

C:\Users\801680>scp Downloads\data_seq.zip ye@xx.xxx.xx.xx:/home/ye/exp/RE2NN-SEQ/data
ye@10.222.41.24's password:
data_seq.zip

Check on server:  

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$ ls -lh data_seq.zip
-rw-rw-r-- 1 ye ye 138M ก.ย.  23 14:02 data_seq.zip
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$

## Unzipping

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$ unzip data_seq.zip
Archive:  data_seq.zip
   creating: ATIS-BIO/
  inflating: ATIS-BIO/atis.dicts.new.pkl
  inflating: ATIS-BIO/dataset.pkl
   creating: ATIS-BIO/automata/
  inflating: ATIS-BIO/atis.test.new.pkl
  inflating: ATIS-BIO/atis.train.new.pkl
  inflating: ATIS-BIO/bio.rules.config.parsed
  inflating: ATIS-BIO/bert_aggregate.emb
  inflating: ATIS-BIO/bert_decontext.emb
   creating: ATIS-BIO/.ipynb_checkpoints/
  inflating: ATIS-BIO/bio.rules.config
  inflating: ATIS-BIO/atis.dev.new.pkl
  inflating: ATIS-BIO/glove.300.emb
  inflating: ATIS-BIO/fasttext.300.emb
  inflating: ATIS-BIO/fasttext.100.emb
  inflating: ATIS-BIO/glove.100.emb
  inflating: ATIS-BIO/automata/IIID.automata.0122092247-1611307367.4236348.svd.2best.140states.random.3splits.100-0.5694150-0.1728200-0.079.bio.rules.v1.config.pkl
   creating: ATIS-ZH-BIO/
  inflating: ATIS-ZH-BIO/dataset.pkl
   creating: ATIS-ZH-BIO/automata/
  inflating: ATIS-ZH-BIO/bio.rules.v1.config
  inflating: ATIS-ZH-BIO/test_ZH.tsv
  inflating: ATIS-ZH-BIO/zh.atis.test.bio
  inflating: ATIS-ZH-BIO/train_ZH.tsv
  inflating: ATIS-ZH-BIO/preprocess_atis_zh.py
  inflating: ATIS-ZH-BIO/zh.atis.train.bio
   creating: ATIS-ZH-BIO/.ipynb_checkpoints/
  inflating: ATIS-ZH-BIO/fasttext.300.emb
  inflating: ATIS-ZH-BIO/fasttext.100.emb
  inflating: ATIS-ZH-BIO/bio.rules.v1.config.parsed
  inflating: ATIS-ZH-BIO/automata/IIID.automata.0308133803-1615210683.6103313.svd.2best.104states.random.3splits.100-0.1496150-0.0934200-0.0541.bio.rules.v1.config.pkl
   creating: SNIPS-BIO/
  inflating: SNIPS-BIO/dataset.pkl
  inflating: SNIPS-BIO/dev.txt
   creating: SNIPS-BIO/automata/
  inflating: SNIPS-BIO/bio.rules.v1.config
  inflating: SNIPS-BIO/train.txt
  inflating: SNIPS-BIO/bert_aggregate.emb
  inflating: SNIPS-BIO/bert_decontext.emb
  inflating: SNIPS-BIO/test.txt
   creating: SNIPS-BIO/.ipynb_checkpoints/
  inflating: SNIPS-BIO/glove.300.emb
  inflating: SNIPS-BIO/fasttext.300.emb
  inflating: SNIPS-BIO/fasttext.100.emb
  inflating: SNIPS-BIO/bio.rules.v1.config.parsed
  inflating: SNIPS-BIO/glove.100.emb
  inflating: SNIPS-BIO/automata/IIID.automata.0323152125-1616512885.4562736.svd.2best.104states.random.1splits.200-0.0025250-0.0026300-0.0022.bio.rules.v1.config.pkl
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$

## Check the folders/Files

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$ ls
ATIS-BIO  ATIS-ZH-BIO  data_seq.zip  README.md  SNIPS-BIO
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$ cd ATIS-BIO
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ ls
atis.dev.new.pkl    atis.train.new.pkl  bert_decontext.emb       dataset.pkl       glove.100.emb
atis.dicts.new.pkl  automata            bio.rules.config         fasttext.100.emb  glove.300.emb
atis.test.new.pkl   bert_aggregate.emb  bio.rules.config.parsed  fasttext.300.emb
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ tree
.
├── atis.dev.new.pkl
├── atis.dicts.new.pkl
├── atis.test.new.pkl
├── atis.train.new.pkl
├── automata
│   └── IIID.automata.0122092247-1611307367.4236348.svd.2best.140states.random.3splits.100-0.5694150-0.1728200-0.079.bio.rules.v1.config.pkl
├── bert_aggregate.emb
├── bert_decontext.emb
├── bio.rules.config
├── bio.rules.config.parsed
├── dataset.pkl
├── fasttext.100.emb
├── fasttext.300.emb
├── glove.100.emb
└── glove.300.emb

1 directory, 14 files
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$

## Check bio.rules.config file:  

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ cat bio.rules.config
//['BOS', 'i', 'would', 'like', 'a', 'nonstop', 'flight', 'from', 'new', 'york', 'to', 'las', 'vegas', 'on', 'march', 'second', 'EOS']
//['O', 'O', 'O', 'O', 'O', 'B-flight_stop', 'O', 'O', 'B-fromloc.city_name', 'I-fromloc.city_name', 'O', 'B-toloc.city_name', 'I-toloc.city_name', 'O', 'B-arrive_date.month_name', 'B-arrive_date.day_number', 'O']

// fromloc.city_name
$<:>OO * from $<:>B-fromloc.city_name $<:>I-fromloc.city_name ? to  $<:>OO *
// 32%

// grammar
// Word<:>Label

// aircraft_code
@aircraft_code@=(767|737|747|757|dc10|f28|72s)
$<:>OO * @aircraft_code<:>aircraft_code@ $<:>OO *
// $<:>OO *  (737<:>B-aircraft_code |747<:>B-aircraft_code |757<:>B-aircraft_code|dc10<:>B-aircraft_code| f28<:>B-aircraft_code| 72s<:>B-aircraft_code) $<:>OO *

// airline code
@airline_code@=(twa | dl | ua | us | hp | ea)
$<:>OO * @airline_code<:>airline_code@ $<:>OO *
// 35%

// airline name
@airline_name@=(american | united | continental | delta | us | midwest | northwest | eastern)
$<:>OO * on the ? @airline_name<:>airline_name@ (airlines<:>I-airline_name | airline<:>I-airline_name | air<:>I-airline_name | 's<:>I-airline_name)? $<:>OO *
$<:>OO * @airline_name<:>airline_name@ (airlines<:>I-airline_name | airline<:>I-airline_name | air<:>I-airline_name | 's<:>I-airline_name | flights<:>O | flight<:>O ) $<:>OO *

// airport_code
@airport_code@=(mco | ewr | ord | bur | atl | hou | lax | mia | yyz | bna )
$<:>OO * @airport_code<:>airport_code@ $<:>OO *

// airport name
$<:>OO * ( at | from | in | of ) the ? $<:>B-airport_name $<:>I-airport_name * (airport<:>I-airport_name | international<:>I-airport_name) $<:>OO *

@day_name@=(wednesday | thursday | monday | tuesday | sunday | saturday | friday | wednesdays | tuesdays)
// arrive_date.date_relative arrive_date.date_name
$<:>OO * (arrives|arrive|arriving) $<:>OO * next<:>B-arrive_date.date_relative ? @day_name<:>arrive_date.day_name@ $<:>OO *

// arrive_date.month_name
@month_name@=(january | february | march | april | may | june | july | august | september | october | november | december )
$<:>OO * (arrives | arrive | arriving ) $<:>OO *  @month_name<:>arrive_date.month_name@ $<:>OO *

// arrive_date.day_number
$<:>OO * (arrives | arrive | arriving ) $<:>OO *  @month_name<:>arrive_date.month_name@  $<:>B-arrive_date.day_number $<:>I-arrive_date.day_number ? EOS

// arrive_date.today_relative
$<:>OO * (arrives | arrive | arriving ) $<:>OO *  tomorrow<:>B-arrive_date.today_relative $<:>OO *


//16-48
// class_type
@class_type@=(first class | coach class | coach | thrift)
$<:>OO * @class_type<:>class_type@ $<:>OO *

//connect
@connect@=(direct | connecting | connections | connect | connects )
$<:>OO * @connect<:>connect@ $<:>OO *

//cost_relative
@cost_relative@=(cheapest | least expensive | less | lowest | most expensive | under | lowest cost )
$<:>OO * @cost_relative<:>cost_relative@ $<:>OO *

//days_code
$<:>OO * sa<:>B-days_code $<:>OO *

//depart_date.date_relative
$<:>OO * from $<:>OO * to $<:>OO * next<:>B-depart_date.date_relative $<:>OO *
$<:>OO * next<:>B-depart_date.date_relative $<:>OO * from $<:>OO * to $<:>OO *

//depart_date.day_name
//@day_name@is defined above
$<:>OO * (leave | depart | between $<:>OO * and | from $<:>OO * to) $<:>OO * @day_name<:>depart_date.day_name@ $<:>OO *
$<:>OO * @day_name<:>depart_date.day_name@ $<:>OO * from $<:>OO * to $<:>OO *

//depart_date.day_number
$<:>OO * @month_name<:>depart_date.month_name@ $<:>B-depart_date.day_number $<:>I-depart_date.day_number ? $<:>OO *

//depart_date.month_name
//@month_name@ is defined above
//there are few month_name, a few arrive_date.month_name and considerable depart_date.month_name, so just label all month_name as depart_date.month_name //for convenient, and similar reasons for following scenarios.
$<:>OO * @month_name<:>depart_date.month_name@ $<:>OO *

//depart_date.today_relative
@today_relative@=(tomorrow | today)
$<:>OO * @today_relative<:>depart_date.today_relative@ $<:>OO *

//depart_date.year
@year@=(1991 | 1992)
$<:>OO * @year<:>depart_date.year@ $<:>OO *

//depart_time.period_of_day
@period_of_day@=(morning | afternoon | night | evening)
$<:>OO * @period_of_day<:>depart_time.period_of_day@ $<:>OO *

//depart_time.time_relative
@time_relative@=(after | before | around)
$<:>OO * @time_relative<:>depart_time.time_relative@ $<:>OO *

//economy
@economy@=(economy | economy class )
$<:>OO * @economy<:>economy@ $<:>OO *

//fare_amount
$<:>OO * $<:>B-fare_amount dollars<:>I-fare_amount $<:>OO *

//fare_basis_code
$<:>OO * fare code $<:>B-fare_basis_code $<:>OO *

//flight_days
$<:>OO * daily<:>B-flight_days $<:>OO *

//flight_mod
$<:>OO * the $<:>B-flight_mod flight $<:>OO *

//flight_stop
@flight_stop@=(nonstop | one stop | stop )
$<:>OO * @flight_stop<:>flight_stop@ $<:>OO *

//flight_time
@flight_time@=(times | schedule | flight times | departure times | flight schedule)
$<:>OO * @flight_time<:>flight_time@ $<:>OO *

//fromloc.airport_code
@fromloc_airport_code@=(bwi | sfo | dfw | jfk )
$<:>OO * @fromloc_airport_code<:>fromloc.airport_code@ $<:>OO *

//fromloc.airport_name
$<:>OO * from the ? $<:>B-fromloc.airport_name $<:>I-fromloc.airport_name * (airport<:>I-fromloc.airport_name| international<:>I-fromloc.airport_name) to $<:>OO *


// 49 fromloc.state_code
$<:>OO * from $<:>B-fromloc.city_name $<:>I-fromloc.city_name ? dc<:>B-fromloc.state_code $<:>OO *
//ACC: 0.7765419996983863, P: 0.7392065344224037, R:0.3878888072495714, F1: 0.5087944743394105

// 50 fromloc.state_name
// $<:>OO * from $<:>B-fromloc.city_name $<:>I-fromloc.city_name ? $<:>B-fromloc.state_name $<:>I-fromloc.state_name ? $<:>OO *

// 51 meal
$<:>OO * (meal<:>B-meal|meals<:>B-meal)  $<:>OO *
//ACC: 0.7772771829286684, P: 0.7403019744483159, R:0.39027675728630906, F1: 0.5111057653756715

// 52 meal_code
//$<:>OO * meal (code | codes) $<:>B-meal_code $<:>I-meal_code ? $<:>OO *

// 53 meal_description
@meal_description@=(lunch|dinner|breakfast|supper|snack)
$<:>OO * @meal_description<:>meal_description@ $<:>OO *

// 54 mod
@mod@=(other|smallest|greatest|most|besides|least|total|more|largest|same|after|two|closest)
$<:>OO * @mod<:>mod@ (plane | seating | aircraft | arrivals) $<:>OO *

// 55 month_name

// 56 or
$<:>OO * or<:>B-or $<:>OO*

// 57 period_of_day
//$<:>OO * (morning<:>B-period_of_day | evening<:>B-period_of_day) $<:>OO*

// 58 restriction_code
$<:>OO* (ap80<:>B-restriction_code | ap57<:>B-restriction_code | ap<:>B-restriction_code) (57<:>I-restriction_code | 55<:>I-restriction_code | 80<:>I-restriction_code) ? $<:>OO*

// 59 return_date.date_relative
$<:>OO* (return | returning | back)  $<:>OO* (in | on) the (same | following | next) day<:>B-return_date.date_relative $<:>OO*

// 60 return_date.day_name

// 61 return_date.day_number  62 return_date.month_name
$<:>OO* returning $<:>OO* @month_name<:>B-return_date.month_name@ $<:>B-return_date.day_number $<:>I-return_date.day_number ? EOS<:>O

// 63 return_date.today_relative

// 64 return_time.period_mod
$<:>OO* returning in the late<:>B-return_time.period_mod evening $<:>OO *

// 65 return_time.period_of_day
//$<:>OO* returning late? in the late? evening<:>B-return_time.period_of_day $<:>OO *

// 66 round_trip
$<:>OO* (round<:>B-round_trip | one<:>B-round_trip) (trip<:>I-round_trip | trips<:>I-round_trip | way<:>I-round_trip) $<:>OO*

// 67 state_code
$<:>OO* ((ground transportation) | airports) $<:>OO* washington dc<:>B-state_code $<:>OO*

// 68 state_name

// 69 stoploc.airport_code

// 70 stoploc.airport_name

// 71 stoploc.city_name
$<:>OO* (stopover|stopovers|stop|stopping|stops) in $<:>B-stoploc.city_name $<:>OO*

// 72 stoploc.state_code

// 73 time

// 74 time_relative

// 75 today_relative

// 76 toloc.airport_code    29
@airport_code@=(dfw|bwi|jfk|sfo|atl)
$<:>OO * (to | and) @airport_code<:>toloc.airport_code@ $<:>OO *

// 77 toloc.airport_name    33
//$<:>OO*  to ((love<:>B-toloc.airport_name field<:>I-toloc.airport_name) | (general<:>B-toloc.airport_name mitchell<:>I-toloc.airport_name international<:>I-toloc.airport_name)) $<:>OO*




// 78 toloc.city_name 32
$<:>OO * from $<:>OO * to $<:>B-toloc.city_name $<:>I-toloc.city_name ? ((on|that|which|and|round) $<:>OO*) ? EOS<:>O

// 79 toloc.country_name

// 80 toloc.state_code 33
$<:>OO * from $<:>OO * to washington ? dc<:>B-toloc.state_code $<:>OO *

// 82 transport_type 35
@transport_type@=(taxi|train|limousine|air taxi operation|car|car rental|rental car|car rentals|limo|rental cars|limousines)
$<:>OO* @transport_type<:>transport_type@ $<:>OO*



// 81 toloc.state_name
//$<:>OO * from $<:>OO * to $<:>B-toloc.city_name $<:>I-toloc.city_name ? (california<:>B-toloc.state_name | washington<:>B-toloc.state_name) $<:>OO*


// 50 fromloc.state_name
// $<:>OO * from $<:>B-fromloc.city_name $<:>I-fromloc.city_name ? $<:>B-fromloc.state_name $<:>I-fromloc.state_name ? $<:>OO *



(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$

## Checked the Parsed Files

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ cat bio.rules.config.parsed
$<:>OO * from<:>O $<:>B-fromloc.city_name $<:>I-fromloc.city_name ? to<:>O $<:>OO *
$<:>OO * ( 767<:>B-aircraft_code | 737<:>B-aircraft_code | 747<:>B-aircraft_code | 757<:>B-aircraft_code | dc10<:>B-aircraft_code | f28<:>B-aircraft_code | 72s<:>B-aircraft_code ) $<:>OO *
$<:>OO * ( twa<:>B-airline_code | dl<:>B-airline_code | ua<:>B-airline_code | us<:>B-airline_code | hp<:>B-airline_code | ea<:>B-airline_code ) $<:>OO *
$<:>OO * on<:>O the<:>O ? ( american<:>B-airline_name | united<:>B-airline_name | continental<:>B-airline_name | delta<:>B-airline_name | us<:>B-airline_name | midwest<:>B-airline_name | northwest<:>B-airline_name | eastern<:>B-airline_name ) ( airlines<:>I-airline_name | airline<:>I-airline_name | air<:>I-airline_name | 's<:>I-airline_name )? $<:>OO *
$<:>OO * ( american<:>B-airline_name | united<:>B-airline_name | continental<:>B-airline_name | delta<:>B-airline_name | us<:>B-airline_name | midwest<:>B-airline_name | northwest<:>B-airline_name | eastern<:>B-airline_name ) ( airlines<:>I-airline_name | airline<:>I-airline_name | air<:>I-airline_name | 's<:>I-airline_name | flights<:>O | flight<:>O ) $<:>OO *
$<:>OO * ( mco<:>B-airport_code | ewr<:>B-airport_code | ord<:>B-airport_code | bur<:>B-airport_code | atl<:>B-airport_code | hou<:>B-airport_code | lax<:>B-airport_code | mia<:>B-airport_code | yyz<:>B-airport_code | bna<:>B-airport_code ) $<:>OO *
$<:>OO * ( at<:>O | from<:>O | in<:>O | of<:>O ) the<:>O ? $<:>B-airport_name $<:>I-airport_name * ( airport<:>I-airport_name | international<:>I-airport_name ) $<:>OO *
$<:>OO * ( arrives<:>O | arrive<:>O | arriving<:>O ) $<:>OO * next<:>B-arrive_date.date_relative ? ( wednesday<:>B-arrive_date.day_name | thursday<:>B-arrive_date.day_name | monday<:>B-arrive_date.day_name | tuesday<:>B-arrive_date.day_name | sunday<:>B-arrive_date.day_name | saturday<:>B-arrive_date.day_name | friday<:>B-arrive_date.day_name | wednesdays<:>B-arrive_date.day_name | tuesdays<:>B-arrive_date.day_name ) $<:>OO *
$<:>OO * ( arrives<:>O | arrive<:>O | arriving<:>O ) $<:>OO * ( january<:>B-arrive_date.month_name | february<:>B-arrive_date.month_name | march<:>B-arrive_date.month_name | april<:>B-arrive_date.month_name | may<:>B-arrive_date.month_name | june<:>B-arrive_date.month_name | july<:>B-arrive_date.month_name | august<:>B-arrive_date.month_name | september<:>B-arrive_date.month_name | october<:>B-arrive_date.month_name | november<:>B-arrive_date.month_name | december<:>B-arrive_date.month_name ) $<:>OO *
$<:>OO * ( arrives<:>O | arrive<:>O | arriving<:>O ) $<:>OO * ( january<:>B-arrive_date.month_name | february<:>B-arrive_date.month_name | march<:>B-arrive_date.month_name | april<:>B-arrive_date.month_name | may<:>B-arrive_date.month_name | june<:>B-arrive_date.month_name | july<:>B-arrive_date.month_name | august<:>B-arrive_date.month_name | september<:>B-arrive_date.month_name | october<:>B-arrive_date.month_name | november<:>B-arrive_date.month_name | december<:>B-arrive_date.month_name ) $<:>B-arrive_date.day_number $<:>I-arrive_date.day_number ? EOS<:>O
$<:>OO * ( arrives<:>O | arrive<:>O | arriving<:>O ) $<:>OO * tomorrow<:>B-arrive_date.today_relative $<:>OO *
$<:>OO * ( first<:>B-class_type class<:>I-class_type | coach<:>B-class_type class<:>I-class_type | coach<:>B-class_type | thrift<:>B-class_type ) $<:>OO *
$<:>OO * ( direct<:>B-connect | connecting<:>B-connect | connections<:>B-connect | connect<:>B-connect | connects<:>B-connect ) $<:>OO *
$<:>OO * ( cheapest<:>B-cost_relative | least<:>B-cost_relative expensive<:>I-cost_relative | less<:>B-cost_relative | lowest<:>B-cost_relative | most<:>B-cost_relative expensive<:>I-cost_relative | under<:>B-cost_relative | lowest<:>B-cost_relative cost<:>I-cost_relative ) $<:>OO *
$<:>OO * sa<:>B-days_code $<:>OO *
$<:>OO * from<:>O $<:>OO * to<:>O $<:>OO * next<:>B-depart_date.date_relative $<:>OO *
$<:>OO * next<:>B-depart_date.date_relative $<:>OO * from<:>O $<:>OO * to<:>O $<:>OO *
$<:>OO * ( leave<:>O | depart<:>O | between<:>O $<:>OO * and<:>O | from<:>O $<:>OO * to<:>O ) $<:>OO * ( wednesday<:>B-depart_date.day_name | thursday<:>B-depart_date.day_name | monday<:>B-depart_date.day_name | tuesday<:>B-depart_date.day_name | sunday<:>B-depart_date.day_name | saturday<:>B-depart_date.day_name | friday<:>B-depart_date.day_name | wednesdays<:>B-depart_date.day_name | tuesdays<:>B-depart_date.day_name ) $<:>OO *
$<:>OO * ( wednesday<:>B-depart_date.day_name | thursday<:>B-depart_date.day_name | monday<:>B-depart_date.day_name | tuesday<:>B-depart_date.day_name | sunday<:>B-depart_date.day_name | saturday<:>B-depart_date.day_name | friday<:>B-depart_date.day_name | wednesdays<:>B-depart_date.day_name | tuesdays<:>B-depart_date.day_name ) $<:>OO * from<:>O $<:>OO * to<:>O $<:>OO *
$<:>OO * ( january<:>B-depart_date.month_name | february<:>B-depart_date.month_name | march<:>B-depart_date.month_name | april<:>B-depart_date.month_name | may<:>B-depart_date.month_name | june<:>B-depart_date.month_name | july<:>B-depart_date.month_name | august<:>B-depart_date.month_name | september<:>B-depart_date.month_name | october<:>B-depart_date.month_name | november<:>B-depart_date.month_name | december<:>B-depart_date.month_name ) $<:>B-depart_date.day_number $<:>I-depart_date.day_number ? $<:>OO *
$<:>OO * ( january<:>B-depart_date.month_name | february<:>B-depart_date.month_name | march<:>B-depart_date.month_name | april<:>B-depart_date.month_name | may<:>B-depart_date.month_name | june<:>B-depart_date.month_name | july<:>B-depart_date.month_name | august<:>B-depart_date.month_name | september<:>B-depart_date.month_name | october<:>B-depart_date.month_name | november<:>B-depart_date.month_name | december<:>B-depart_date.month_name ) $<:>OO *
$<:>OO * ( tomorrow<:>B-depart_date.today_relative | today<:>B-depart_date.today_relative ) $<:>OO *
$<:>OO * ( 1991<:>B-depart_date.year | 1992<:>B-depart_date.year ) $<:>OO *
$<:>OO * ( morning<:>B-depart_time.period_of_day | afternoon<:>B-depart_time.period_of_day | night<:>B-depart_time.period_of_day | evening<:>B-depart_time.period_of_day ) $<:>OO *
$<:>OO * ( after<:>B-depart_time.time_relative | before<:>B-depart_time.time_relative | around<:>B-depart_time.time_relative ) $<:>OO *
$<:>OO * ( economy<:>B-economy | economy<:>B-economy class<:>I-economy ) $<:>OO *
$<:>OO * $<:>B-fare_amount dollars<:>I-fare_amount $<:>OO *
$<:>OO * fare<:>O code<:>O $<:>B-fare_basis_code $<:>OO *
$<:>OO * daily<:>B-flight_days $<:>OO *
$<:>OO * the<:>O $<:>B-flight_mod flight<:>O $<:>OO *
$<:>OO * ( nonstop<:>B-flight_stop | one<:>B-flight_stop stop<:>I-flight_stop | stop<:>B-flight_stop ) $<:>OO *
$<:>OO * ( times<:>B-flight_time | schedule<:>B-flight_time | flight<:>B-flight_time times<:>I-flight_time | departure<:>B-flight_time times<:>I-flight_time | flight<:>B-flight_time schedule<:>I-flight_time ) $<:>OO *
$<:>OO * ( bwi<:>B-fromloc.airport_code | sfo<:>B-fromloc.airport_code | dfw<:>B-fromloc.airport_code | jfk<:>B-fromloc.airport_code ) $<:>OO *
$<:>OO * from<:>O the<:>O ? $<:>B-fromloc.airport_name $<:>I-fromloc.airport_name * ( airport<:>I-fromloc.airport_name | international<:>I-fromloc.airport_name ) to<:>O $<:>OO *
$<:>OO * from<:>O $<:>B-fromloc.city_name $<:>I-fromloc.city_name ? dc<:>B-fromloc.state_code $<:>OO *
$<:>OO * ( meal<:>B-meal | meals<:>B-meal ) $<:>OO *
$<:>OO * ( lunch<:>B-meal_description | dinner<:>B-meal_description | breakfast<:>B-meal_description | supper<:>B-meal_description | snack<:>B-meal_description ) $<:>OO *
$<:>OO * ( other<:>B-mod | smallest<:>B-mod | greatest<:>B-mod | most<:>B-mod | besides<:>B-mod | least<:>B-mod | total<:>B-mod | more<:>B-mod | largest<:>B-mod | same<:>B-mod | after<:>B-mod | two<:>B-mod | closest<:>B-mod ) ( plane<:>O | seating<:>O | aircraft<:>O | arrivals<:>O ) $<:>OO *
$<:>OO * or<:>B-or $<:>OO *
$<:>OO * ( ap80<:>B-restriction_code | ap57<:>B-restriction_code | ap<:>B-restriction_code ) ( 57<:>I-restriction_code | 55<:>I-restriction_code | 80<:>I-restriction_code ) ? $<:>OO *
$<:>OO * ( return<:>O | returning<:>O | back<:>O ) $<:>OO * ( in<:>O | on<:>O ) the<:>O ( same<:>O | following<:>O | next<:>O ) day<:>B-return_date.date_relative $<:>OO *
$<:>OO * returning<:>O $<:>OO * ( january<:>B-return_date.month_name | february<:>B-return_date.month_name | march<:>B-return_date.month_name | april<:>B-return_date.month_name | may<:>B-return_date.month_name | june<:>B-return_date.month_name | july<:>B-return_date.month_name | august<:>B-return_date.month_name | september<:>B-return_date.month_name | october<:>B-return_date.month_name | november<:>B-return_date.month_name | december<:>B-return_date.month_name ) $<:>B-return_date.day_number $<:>I-return_date.day_number ? EOS<:>O
$<:>OO * returning<:>O in<:>O the<:>O late<:>B-return_time.period_mod evening<:>O $<:>OO *
$<:>OO * ( round<:>B-round_trip | one<:>B-round_trip ) ( trip<:>I-round_trip | trips<:>I-round_trip | way<:>I-round_trip ) $<:>OO *
$<:>OO * (( ground<:>O transportation<:>O ) | airports<:>O ) $<:>OO * washington<:>O dc<:>B-state_code $<:>OO *
$<:>OO * ( stopover<:>O | stopovers<:>O | stop<:>O | stopping<:>O | stops<:>O ) in<:>O $<:>B-stoploc.city_name $<:>OO *
$<:>OO * ( to<:>O | and<:>O ) ( dfw<:>B-toloc.airport_code | bwi<:>B-toloc.airport_code | jfk<:>B-toloc.airport_code | sfo<:>B-toloc.airport_code | atl<:>B-toloc.airport_code ) $<:>OO *
$<:>OO * from<:>O $<:>OO * to<:>O $<:>B-toloc.city_name $<:>I-toloc.city_name ? (( on<:>O | that<:>O | which<:>O | and<:>O | round<:>O ) $<:>OO *) ? EOS<:>O
$<:>OO * from<:>O $<:>OO * to<:>O washington<:>O ? dc<:>B-toloc.state_code $<:>OO *
$<:>OO * ( taxi<:>B-transport_type | train<:>B-transport_type | limousine<:>B-transport_type | air<:>B-transport_type taxi<:>I-transport_type operation<:>I-transport_type | car<:>B-transport_type | car<:>B-transport_type rental<:>I-transport_type | rental<:>B-transport_type car<:>I-transport_type | car<:>B-transport_type rentals<:>I-transport_type | limo<:>B-transport_type | rental<:>B-transport_type cars<:>I-transport_type | limousines<:>B-transport_type ) $<:>OO *
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$

## Check SNIPS-BIO Folder

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$ tree SNIPS-BIO/
SNIPS-BIO/
├── automata
│   └── IIID.automata.0323152125-1616512885.4562736.svd.2best.104states.random.1splits.200-0.0025250-0.0026300-0.0022.bio.rules.v1.config.pkl
├── bert_aggregate.emb
├── bert_decontext.emb
├── bio.rules.v1.config
├── bio.rules.v1.config.parsed
├── dataset.pkl
├── dev.txt
├── fasttext.100.emb
├── fasttext.300.emb
├── glove.100.emb
├── glove.300.emb
├── test.txt
└── train.txt

1 directory, 13 files
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data$

## Check the  bio.rules.v1.config File

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$ cat bio.rules.v1.config
// object_type

@object_type@=(book | novel | movie schedule | album | movie schedules | movie times | essay | textbook | tv show | saga | trailer | photograph | picture | television show | game | painting | tv series | soundtrack | song | movie)
@rate_value@=(0|1|2|3|4|5|zero|one|two|three|four|five)
@rating_unit@=(stars|points)
@object_select@=(this|current)
@series_type@=(saga|series|chronicle)
@best_rating@=(6)
@music_item@=(song | album | track | tune | artist | soundtrack)

$<:>OO * (find|looking for|show|download|get) me (a|the) @object_type<:>object_type@ called $<:>B-object_name $<:>I-object_name *

$<:>OO * (@rate_value<:>rating_value@ @rating_unit<:>rating_unit@ | at @rate_value<:>rating_value@ | a rating of @rate_value<:>rating_value@ | @rate_value<:>rating_value@ out ? of @best_rating<:>best_rating@) $<:>OO *

$<:>OO * @rating_unit<:>rating_unit@ $<:>OO *

$<:>OO * @object_select<:>object_select@ (@object_type<:>object_type@ | @series_type<:>object_part_of_series_type@ ) $<:>OO *

$<:>OO * (add|put) $<:>OO * to my<:>B-playlist_owner ($<:>B-playlist $<:>I-playlist * playlist | $<:>B-playlist $<:>I-playlist $<:>I-playlist ?)
$<:>OO * play playlist $<:>B-playlist $<:>I-playlist ?
$<:>OO * my<:>B-playlist_owner $<:>OO * playlist $<:>OO *

$<:>OO * @music_item<:>music_item@ $<:>OO *

$<:>OO * in<:>b-timerange $<:>i-timerange + (minutes<:>i-timerange|seconds<:>i-timerange|days<:>i-timerange|months<:>i-timerange) $<:>OO *
$<:>OO * at $<:>b-timerange (am<:>i-timerange|pm<:>i-timerange|a<:>i-timerange m<:>i-timerange|p<:>i-timerange m<:>i-timerange|o<:>i-timerange clock<:>i-timerange) $<:>OO *

$<:>OO * @music_item<:>music_item@ by $<:>b-artist $<:>i-artist ?

$<:>OO * (weather|sunny|forecasted|forecast) $<:>OO * in $<:>b-city $<:>i-city ?

@res_type@=(restaurant | bar | brasserie | pub | taverna | food truck | cafeteria )
$<:>OO * @res_type<:>restaurant_type@ $<:>OO *

@spatial_relation@=(nearest | closest | nearby | close by | in the neighborhood | in the area)
$<:>OO * @spatial_relation<:>spatial_relation@ $<:>OO *

$<:>OO * (table|seats|reservation|restaurant|spot) $<:>OO * for $<:>b-party_size_number people ? $<:>OO *

@object_location_type@=(movie house | cinema | movie theatre)
$<:>OO * @object_location_type<:>object_location_type@ $<:>OO *

$<:>OO * (when is| what time is|find me|where is|is|see|watch) $<:>b-movie_name $<:>i-movie_name * (playing|showing) $<:>OO *

@service@=(netflix | itunes | groove shark | google music | deezer | spotify | zvooq | youtube | lastfm | pandora | slacker | iheart | vimeo | last fm )
$<:>OO * @service<:>service@ $<:>OO *

@movie_type@=(animated movies | films | film)
$<:>OO * @movie_type<:>movie_type@ $<:>OO *

@year@=(twenties | fourties | eighties | thirties | sixties | fifties | seventies | nineties |1958 | 2011 | 2003 | 2016)
$<:>OO * @year<:>year@ $<:>OO *


@location_name@=(entertainment|theatres|corporation|cinemas)
$<:>OO * (for|at) $<:>b-location_name @location_name<:>I-location_name@ $<:>OO *

@sort@=(highly rated | best | popular | top-rated | top )
$<:>OO * @sort<:>sort@ $<:>OO *

@condition_temperature@=(colder | chilly | warm | hot | freezing | hotter | cold | warmer )
$<:>OO * @condition_temperature<:>condition_temperature@ $<:>OO *

@cond@=(blizzard | rain | cloudy | windy | hail | snowstorm)
$<:>OO * @cond<:>condition_description@ $<:>OO *

@current_location@=(here | current position | current location | current place | current spot)
$<:>OO * @current_location<:>current_location@ $<:>OO *
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$

## Check Raw Text Files

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$ wc train.txt
 143868  248484 1748639 train.txt
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$ wc test.txt
 7754 13408 93957 test.txt
 
Check the train file format:  
 
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$ head -n 30 train.txt
listen O
to O
westbam B-artist
alumb O
allergic B-album
on O
google B-service
music I-service
PlayMusic

add O
step B-entity_name
to I-entity_name
me I-entity_name
to O
the O
50 B-playlist
clásicos I-playlist
playlist O
AddToPlaylist

i O
give O
this O
current B-object_select
textbook B-object_type
a O
rating O
value O
of O
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$

Check the test file format:  

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$ head -n 30 test.txt
add O
sabrina B-artist
salerno I-artist
to O
the O
grime B-playlist
instrumentals I-playlist
playlist O
AddToPlaylist

i O
want O
to O
bring O
four B-party_size_number
people O
to O
a O
place O
that O
s O
close B-spatial_relation
to O
downtown B-poi
that O
serves O
churrascaria B-restaurant_type
cuisine O
BookRestaurant

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/SNIPS-BIO$

## Check ATIS-BIO .pkl File

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ python -mpickle ./dataset.pkl > ./dataset.txt


(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ head ./dataset.txt
{'i2s': {0: 'b-aircraft_code',
         1: 'b-airline_code',
         2: 'b-airline_name',
         3: 'b-airport_code',
         4: 'b-airport_name',
         5: 'b-arrive_date.date_relative',
         6: 'b-arrive_date.day_name',
         7: 'b-arrive_date.day_number',
         8: 'b-arrive_date.month_name',
         9: 'b-arrive_date.today_relative',
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ tail ./dataset.txt
         'y': 933,
         'year': 934,
         'yes': 935,
         'yn': 936,
         'york': 937,
         'you': 938,
         'your': 939,
         'yx': 940,
         'yyz': 941,
         'zone': 942}}
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ python ./open_pkl.py ./atis.train.new.pkl | head -n 30
(array([array([178, 770, 581, 827, 429, 444, 789, 677, 851, 856, 826, 236, 388,
              482, 827, 606, 179])                                            ,
       array([178, 916, 498, 827, 387, 428, 444, 266, 851, 739, 440, 826, 758,
              180, 582, 179])                                                 ,
       array([178, 479, 932, 545, 851, 423, 180, 428, 444, 511, 301, 851, 736,
              521, 301, 654, 350, 215, 238, 240, 185, 158, 642, 482, 827, 402,
              329, 938, 688, 818, 581, 827, 196, 215, 827, 428, 638, 824, 938,
              179])                                                           ,
       ...,
       array([178, 916, 429, 228, 831, 444, 339, 851, 682, 654, 601, 606, 179]),
       array([178, 479, 932, 545, 851, 431, 444, 736, 521, 301, 246, 851, 789,
              677, 654, 908, 179])                                            ,
       array([178, 916, 498, 827, 566, 414, 887, 293, 259, 266, 215, 739, 440,
              179])                                                           ],
      dtype=object), array([[14],
       [14],
       [14],
       ...,
       [14],
       [14],
       [ 3]]), array([array([128, 128, 128, 128, 128, 128,  48, 110, 128,  78, 128, 128,  11,
              128, 128,  12, 128])                                            ,
       array([128, 128, 128, 128,  42, 128, 128,  48, 128,  78, 125, 128, 128,
              128,  51, 128])                                                 ,
       array([128, 128, 128, 128, 128, 128, 128, 128, 128,  48, 110, 128,  78,
              125, 125, 128,   2, 128, 128, 128,  15,  14,  89, 128, 128,  12,
              128, 128, 128, 128, 128, 128, 128, 128, 128, 128, 128, 128, 128,
              128])                                                           ,
       ...,
       array([128, 128, 128, 128, 128, 128,  48, 128,  78, 128,  26,  33, 128]),
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/data/ATIS-BIO$ python ./open_pkl.py ./atis.dicts.new.pkl | head -n 30
...
...
...
'B-return_time.period_of_day': 65, 'B-round_trip': 66, 'B-state_code': 67, 'B-state_name': 68, 'B-stoploc.airport_code': 69, 'B-stoploc.airport_name': 70, 'B-stoploc.city_name': 71, 'B-stoploc.state_code': 72, 'B-time': 73, 'B-time_relative': 74, 'B-today_relative': 75, 'B-toloc.airport_code': 76, 'B-toloc.airport_name': 77, 'B-toloc.city_name': 78, 'B-toloc.country_name': 79, 'B-toloc.state_code': 80, 'B-toloc.state_name': 81, 'B-transport_type': 82, 'I-airline_name': 83, 'I-airport_name': 84, 'I-arrive_date.day_number': 85, 'I-arrive_time.end_time': 86, 'I-arrive_time.period_of_day': 87, 'I-arrive_time.start_time': 88, 'I-arrive_time.time': 89, 'I-arrive_time.time_relative': 90, 'I-city_name': 91, 'I-class_type': 92, 'I-cost_relative': 93, 'I-depart_date.day_name': 94, 'I-depart_date.day_number': 95, 'I-depart_date.today_relative': 96, 'I-depart_time.end_time': 97, 'I-depart_time.period_of_day': 98, 'I-depart_time.start_time': 99, 'I-depart_time.time': 100, 'I-depart_time.time_relative': 101, 'I-economy': 102, 'I-fare_amount': 103, 'I-fare_basis_code': 104, 'I-flight_mod': 105, 'I-flight_number': 106, 'I-flight_stop': 107, 'I-flight_time': 108, 'I-fromloc.airport_name': 109, 'I-fromloc.city_name': 110, 'I-fromloc.state_name': 111, 'I-meal_code': 112, 'I-meal_description': 113, 'I-mod': 114, 'I-restriction_code': 115, 'I-return_date.date_relative': 116, 'I-return_date.day_number': 117, 'I-return_date.today_relative': 118, 'I-round_trip': 119, 'I-state_name': 120, 'I-stoploc.city_name': 121, 'I-time': 122, 'I-today_relative': 123, 'I-toloc.airport_name': 124, 'I-toloc.city_name': 125, 'I-toloc.state_name': 126, 'I-transport_type': 127, 'O': 128}, 'intent_ids': {'abbreviation': 0, 'aircraft': 1, 'aircraft+flight+flight_no': 2, 'airfare': 3, 'airfare+flight': 4, 'airfare+flight_time': 5, 'airline': 6, 'airline+flight_no': 7, 'airport': 8, 'capacity': 9, 'cheapest': 10, 'city': 11, 'day_name': 12, 'distance': 13, 'flight': 14, 'flight+airfare': 15, 'flight+airline': 16, 'flight_no': 17, 'flight_no+airline': 18, 'flight_time': 19, 'ground_fare': 20, 'ground_service': 21, 'ground_service+ground_fare': 22, 'meal': 23, 'quantity': 24, 'restriction': 25}})

## Pandas Library Required

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ pip install pandas
Collecting pandas
  Obtaining dependency information for pandas from https://files.pythonhosted.org/packages/f8/7f/5b047effafbdd34e52c9e2d7e44f729a0655efafb22198c45cf692cdc157/pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata
  Downloading pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (18 kB)
Collecting python-dateutil>=2.8.2 (from pandas)
  Using cached python_dateutil-2.8.2-py2.py3-none-any.whl (247 kB)
Collecting pytz>=2020.1 (from pandas)
  Obtaining dependency information for pytz>=2020.1 from https://files.pythonhosted.org/packages/32/4d/aaf7eff5deb402fd9a24a1449a8119f00d74ae9c2efa79f8ef9994261fc2/pytz-2023.3.post1-py2.py3-none-any.whl.metadata
  Downloading pytz-2023.3.post1-py2.py3-none-any.whl.metadata (22 kB)
Collecting tzdata>=2022.1 (from pandas)
  Using cached tzdata-2023.3-py2.py3-none-any.whl (341 kB)
Requirement already satisfied: numpy>=1.20.3 in /home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages (from pandas) (1.24.4)
Collecting six>=1.5 (from python-dateutil>=2.8.2->pandas)
  Using cached six-1.16.0-py2.py3-none-any.whl (11 kB)
Using cached pandas-2.0.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (12.4 MB)
Downloading pytz-2023.3.post1-py2.py3-none-any.whl (502 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 502.5/502.5 kB 3.7 MB/s eta 0:00:00
Installing collected packages: pytz, tzdata, six, python-dateutil, pandas
Successfully installed pandas-2.0.3 python-dateutil-2.8.2 pytz-2023.3.post1 six-1.16.0 tzdata-2023.3
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

## pydash also Required

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ time python main.py --args_path ../model_seq/config_file_path.res
Traceback (most recent call last):
  File "main.py", line 5, in <module>
    from src_seq.train_onehot import train_slot_onehot
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/train_onehot.py", line 3, in <module>
    from src_seq.data import load_slot_dataset, SlotBatchDataset
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/data.py", line 8, in <module>
    from src_seq.load_data_and_rules import *
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/load_data_and_rules.py", line 9, in <module>
    from pydash import flow
ModuleNotFoundError: No module named 'pydash'

real    0m0.289s
user    0m0.442s
sys     0m0.792s
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ pip install pydash
Collecting pydash
  Obtaining dependency information for pydash from https://files.pythonhosted.org/packages/1b/8c/b0b1c3ed6eff8ef50e396084a0d0d8e82eeae44027c18cff9aef705f8eb0/pydash-7.0.6-py3-none-any.whl.metadata
  Downloading pydash-7.0.6-py3-none-any.whl.metadata (45 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 45.5/45.5 kB 470.2 kB/s eta 0:00:00
Collecting typing-extensions!=4.6.0,>=3.10 (from pydash)
  Obtaining dependency information for typing-extensions!=4.6.0,>=3.10 from https://files.pythonhosted.org/packages/24/21/7d397a4b7934ff4028987914ac1044d3b7d52712f30e2ac7a2ae5bc86dd0/typing_extensions-4.8.0-py3-none-any.whl.metadata
  Downloading typing_extensions-4.8.0-py3-none-any.whl.metadata (3.0 kB)
Downloading pydash-7.0.6-py3-none-any.whl (110 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 110.1/110.1 kB 1.1 MB/s eta 0:00:00
Downloading typing_extensions-4.8.0-py3-none-any.whl (31 kB)
Installing collected packages: typing-extensions, pydash
Successfully installed pydash-7.0.6 typing-extensions-4.8.0
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

## FastText Installation

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ time python main.py --args_path ../model_seq/config_file_path.res
Traceback (most recent call last):
  File "main.py", line 5, in <module>
    from src_seq.train_onehot import train_slot_onehot
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/train_onehot.py", line 3, in <module>
    from src_seq.data import load_slot_dataset, SlotBatchDataset
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/data.py", line 17, in <module>
    import fasttext.util
ModuleNotFoundError: No module named 'fasttext'

real    0m0.301s
user    0m0.549s
sys     0m0.657s
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ pip install fasttext
Collecting fasttext
  Using cached fasttext-0.9.2-cp38-cp38-linux_x86_64.whl
Collecting pybind11>=2.2 (from fasttext)
  Obtaining dependency information for pybind11>=2.2 from https://files.pythonhosted.org/packages/06/55/9f73c32dda93fa4f539fafa268f9504e83c489f460c380371d94296126cd/pybind11-2.11.1-py3-none-any.whl.metadata
  Using cached pybind11-2.11.1-py3-none-any.whl.metadata (9.5 kB)
Requirement already satisfied: setuptools>=0.7.0 in /home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages (from fasttext) (68.0.0)
Requirement already satisfied: numpy in /home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages (from fasttext) (1.24.4)
Using cached pybind11-2.11.1-py3-none-any.whl (227 kB)
Installing collected packages: pybind11, fasttext
Successfully installed fasttext-0.9.2 pybind11-2.11.1
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

## Transformer Required

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ time python main.py --args_path ../model_seq/config_file_path.res
Traceback (most recent call last):
  File "main.py", line 5, in <module>
    from src_seq.train_onehot import train_slot_onehot
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/train_onehot.py", line 3, in <module>
    from src_seq.data import load_slot_dataset, SlotBatchDataset
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/data.py", line 19, in <module>
    from src_seq.ptm.bert_utils import bert_preprocess
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/ptm/bert_utils.py", line 1, in <module>
    from transformers import BertConfig, BertTokenizer, BertModel
ModuleNotFoundError: No module named 'transformers'

real    0m0.317s
user    0m0.517s
sys     0m0.736s
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$


(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ pip install transformers
...
...
Downloading filelock-3.12.4-py3-none-any.whl (11 kB)
Using cached requests-2.31.0-py3-none-any.whl (62 kB)
Using cached certifi-2023.7.22-py3-none-any.whl (158 kB)
Using cached charset_normalizer-3.2.0-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (199 kB)
Downloading urllib3-2.0.5-py3-none-any.whl (123 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 123.8/123.8 kB 3.0 MB/s eta 0:00:00
Downloading fsspec-2023.9.2-py3-none-any.whl (173 kB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 173.4/173.4 kB 2.5 MB/s eta 0:00:00
Installing collected packages: tokenizers, safetensors, urllib3, regex, pyyaml, packaging, idna, fsspec, filelock, charset-normalizer, certifi, requests, huggingface-hub, transformers
Successfully installed certifi-2023.7.22 charset-normalizer-3.2.0 filelock-3.12.4 fsspec-2023.9.2 huggingface-hub-0.17.2 idna-3.4 packaging-23.1 pyyaml-6.0.1 regex-2023.8.8 requests-2.31.0 safetensors-0.3.3 tokenizers-0.13.3 transformers-4.33.2 urllib3-2.0.5
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$


## Try Again

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ time python main.py --args_path ../model_seq/config_file_path.res
...
...
...
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/transformers/utils/import_utils.py", line 1175, in __getattr__
    value = getattr(module, name)
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/transformers/utils/import_utils.py", line 1174, in __getattr__
    module = self._get_module(self._class_to_module[name])
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/transformers/utils/import_utils.py", line 1186, in _get_module
    raise RuntimeError(
RuntimeError: Failed to import transformers.models.bert.modeling_bert because of the following error (look up to see its traceback):
No module named 'torch.utils._pytree'

real    0m0.389s
user    0m0.555s
sys     0m0.702s

## Upgrading Torch

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ pip install torch --upgrade
...
...
...
  Downloading mpmath-1.3.0-py3-none-any.whl (536 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 536.2/536.2 kB 13.1 MB/s eta 0:00:00
Using cached MarkupSafe-2.1.3-cp38-cp38-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (25 kB)
Using cached cmake-3.27.5-py2.py3-none-manylinux2014_x86_64.manylinux_2_17_x86_64.whl (26.1 MB)
Building wheels for collected packages: lit
  Building wheel for lit (pyproject.toml) ... done
  Created wheel for lit: filename=lit-16.0.6-py3-none-any.whl size=93584 sha256=1691e690a42075c79aef2d986c59305fdeb3e1e65e560a2e4e432afd7201ab91
  Stored in directory: /home/ye/.cache/pip/wheels/05/ab/f1/0102fea49a41c753f0e79a1a4012417d5d7ef0f93224694472
Successfully built lit
Installing collected packages: mpmath, lit, cmake, sympy, nvidia-nvtx-cu11, nvidia-nccl-cu11, nvidia-cusparse-cu11, nvidia-curand-cu11, nvidia-cufft-cu11, nvidia-cuda-runtime-cu11, nvidia-cuda-nvrtc-cu11, nvidia-cuda-cupti-cu11, nvidia-cublas-cu11, networkx, MarkupSafe, nvidia-cusolver-cu11, nvidia-cudnn-cu11, jinja2, triton, torch
  Attempting uninstall: torch
    Found existing installation: torch 1.4.0
    Uninstalling torch-1.4.0:
      Successfully uninstalled torch-1.4.0
Successfully installed MarkupSafe-2.1.3 cmake-3.27.5 jinja2-3.1.2 lit-16.0.6 mpmath-1.3.0 networkx-3.1 nvidia-cublas-cu11-11.10.3.66 nvidia-cuda-cupti-cu11-11.7.101 nvidia-cuda-nvrtc-cu11-11.7.99 nvidia-cuda-runtime-cu11-11.7.99 nvidia-cudnn-cu11-8.5.0.96 nvidia-cufft-cu11-10.9.0.58 nvidia-curand-cu11-10.2.10.91 nvidia-cusolver-cu11-11.4.0.1 nvidia-cusparse-cu11-11.7.4.91 nvidia-nccl-cu11-2.14.3 nvidia-nvtx-cu11-11.7.91 sympy-1.12 torch-2.0.1 triton-2.0.0
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$

## Try Again

(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ python main.py --help
usage: main.py [-h] [--dataset DATASET] [--seq_max_len SEQ_MAX_LEN] [--bz BZ]
               [--embed_dim EMBED_DIM] [--embed_type EMBED_TYPE] [--epoch EPOCH]
               [--train_portion TRAIN_PORTION] [--automata_path AUTOMATA_PATH] [--seed SEED]
               [--run RUN] [--random_embed RANDOM_EMBED] [--optimizer OPTIMIZER] [--lr LR]
               [--train_mode TRAIN_MODE] [--local_loss_func LOCAL_LOSS_FUNC]
               [--rand_constant RAND_CONSTANT] [--threshold THRESHOLD] [--margin MARGIN]
               [--select_level SELECT_LEVEL] [--method METHOD] [--data_type DATA_TYPE]
               [--train_word_embed TRAIN_WORD_EMBED] [--rnn_hidden_dim RNN_HIDDEN_DIM]
               [--rnn RNN] [--bidirection BIDIRECTION] [--marryup_type MARRYUP_TYPE]
               [--re_tag_dim RE_TAG_DIM] [--c1_kdpr C1_KDPR] [--c2_kdpr C2_KDPR] [--c3_pr C3_PR]
               [--normalize_automata NORMALIZE_AUTOMATA] [--train_V_embed TRAIN_V_EMBED]
               [--beta BETA] [--rank RANK] [--rank_wildcard RANK_WILDCARD]
               [--additional_nonlinear ADDITIONAL_NONLINEAR]
               [--additional_states ADDITIONAL_STATES] [--use_priority USE_PRIORITY]
               [--train_wildcard TRAIN_WILDCARD]
               [--train_wildcard_wildcard TRAIN_WILDCARD_WILDCARD]
               [--train_c_output TRAIN_C_OUTPUT] [--train_h0 TRAIN_H0] [--train_hT TRAIN_HT]
               [--train_beta TRAIN_BETA] [--random RANDOM] [--random_pad_func RANDOM_PAD_FUNC]
               [--save_model SAVE_MODEL] [--independent INDEPENDENT] [--use_unlabel USE_UNLABEL]
               [--farnn FARNN] [--xavier XAVIER] [--bias_init BIAS_INIT]
               [--sigmoid_exponent SIGMOID_EXPONENT] [--use_crf USE_CRF]
               [--update_nonlinear UPDATE_NONLINEAR] [--args_path ARGS_PATH]
               [--bert_finetune BERT_FINETUNE] [--use_bert USE_BERT] [--warm_up WARM_UP]
               [--bert_lr_down_factor BERT_LR_DOWN_FACTOR] [--bert_init_embed BERT_INIT_EMBED]

optional arguments:
  -h, --help            show this help message and exit
  --dataset DATASET     dataset dir
  --seq_max_len SEQ_MAX_LEN
                        Max seq length
  --bz BZ               batch size
  --embed_dim EMBED_DIM
                        embed dim
  --embed_type EMBED_TYPE
                        embedding type should be in [glove, fasttext]
  --epoch EPOCH         max state of each FSARNN
  --train_portion TRAIN_PORTION
                        train portion
  --automata_path AUTOMATA_PATH
                        automata path
  --seed SEED           random seed
  --run RUN             run string
  --random_embed RANDOM_EMBED
                        0 false 1 true
  --optimizer OPTIMIZER
                        optimizer
  --lr LR               learning rate of optimizer
  --train_mode TRAIN_MODE
                        global train mode, should be in [max, sum]
  --local_loss_func LOCAL_LOSS_FUNC
                        loss function in local mode, should be in [CE, NNLL, HL]
  --rand_constant RAND_CONSTANT
                        random noise
  --threshold THRESHOLD
                        the threshold used in the hinge loss option in local training
  --margin MARGIN       the margin used in the hinge loss option in local training
  --select_level SELECT_LEVEL
                        should be in entity-level or token-level
  --method METHOD       method should be in [onehot, decompose, baseline]
  --data_type DATA_TYPE
                        data type we use, should be in [all, re, n_re]
  --train_word_embed TRAIN_WORD_EMBED
                        if we train word embed or not, fix as default (0)
  --rnn_hidden_dim RNN_HIDDEN_DIM
                        rnn / farnn_random hidden dim
  --rnn RNN             should be in RNN, LSTM, GRU
  --bidirection BIDIRECTION
                        1 means bidirectional, 0 otherwise
  --marryup_type MARRYUP_TYPE
                        marryup type, [input, output, all, kd, pr]
  --re_tag_dim RE_TAG_DIM
                        re tag embedding dim for marryup methods
  --c1_kdpr C1_KDPR     regularization param for PR, the bigger the harder, or the temperature in
                        KD
  --c2_kdpr C2_KDPR     balancing weights for KD PR loss and original loss, [0, 1], 1 means use
                        original loss (CE)
  --c3_pr C3_PR         annealing speed for pr
  --normalize_automata NORMALIZE_AUTOMATA
                        if we normalize the decomposed automata params, only used when use
                        decomposed method [none, l1, l2]
  --train_V_embed TRAIN_V_EMBED
                        0 means do not train V_embed
  --beta BETA           interpolation weight for word embedding and rule embedding
  --rank RANK           rank of decomposed tensor
  --rank_wildcard RANK_WILDCARD
                        rank of wildcard decomposed tensor, should be in [30, 50, 70, 100, 150]
  --additional_nonlinear ADDITIONAL_NONLINEAR
                        additional nonlinear for word embedding to rule dim
  --additional_states ADDITIONAL_STATES
                        additional states with very small random values
  --use_priority USE_PRIORITY
                        0, or 1, 1 means use priority
  --train_wildcard TRAIN_WILDCARD
                        if we train wildcard tensor CxSxS
  --train_wildcard_wildcard TRAIN_WILDCARD_WILDCARD
                        if we train wildcard_wildcard matrix SxS
  --train_c_output TRAIN_C_OUTPUT
                        if we train C related params in single
  --train_h0 TRAIN_H0   if we train h0
  --train_hT TRAIN_HT   if we train hT
  --train_beta TRAIN_BETA
                        if we train beta
  --random RANDOM       if we use random initialization
  --random_pad_func RANDOM_PAD_FUNC
                        which padding function we use, should be in normal, uniform, and xavier
  --save_model SAVE_MODEL
                        if we save model
  --independent INDEPENDENT
                        if we use independent decomposed model
  --use_unlabel USE_UNLABEL
                        if we use unlabel data
  --farnn FARNN         0 for rnn, 1 for only update, 2 for update + reset
  --xavier XAVIER       0 for not using xavier for farnn, only work when farnn > 1
  --bias_init BIAS_INIT
                        0 for not using xavier for farnn, only work when farnn > 1
  --sigmoid_exponent SIGMOID_EXPONENT
                        sigmoidal function exponent
  --use_crf USE_CRF     if we use crf
  --update_nonlinear UPDATE_NONLINEAR
                        whe nonlinear used when update
  --args_path ARGS_PATH
                        arguments path, if is not none, load and train
  --bert_finetune BERT_FINETUNE
                        if we finetune bert
  --use_bert USE_BERT   if we use bert
  --warm_up WARM_UP     if we use warm up
  --bert_lr_down_factor BERT_LR_DOWN_FACTOR
                        the down factor for the (bert_lr = lr/down_factor)
  --bert_init_embed BERT_INIT_EMBED
                        embed used to initializing G, [random, aggregate, decontext]
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$



(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$ python main.py --args_path ../model_seq/example/ATIS-ZH.FSTRNN.10%.crf.8313.res
{'dataset': 'ATIS-ZH-BIO', 'seq_max_len': 30, 'bz': 300, 'embed_dim': 300, 'embed_type': 'fasttext', 'epoch': 60, 'train_portion': 0.1, 'automata_path': '../data/ATIS-ZH-BIO/automata/IIID.automata.0308133803-1615210683.6103313.svd.2best.104states.random.3splits.100-0.1496150-0.0934200-0.0541.bio.rules.v1.config.pkl', 'seed': 1, 'run': 'final_222', 'random_embed': 0, 'optimizer': 'ADAM', 'lr': 0.005, 'train_mode': 'sum', 'local_loss_func': 'CE1', 'rand_constant': 1e-05, 'threshold': 0.1, 'margin': 0.5, 'select_level': 'entity-level', 'method': 'decompose', 'data_type': 'all', 'train_word_embed': 0, 'rnn_hidden_dim': 100, 'rnn': 'RNN', 'bidirection': 0, 'marryup_type': 'none', 're_tag_dim': 20, 'c1_kdpr': 1, 'c2_kdpr': 1, 'c3_pr': 1.0, 'normalize_automata': 'l2-rank', 'train_V_embed': 0, 'beta': 0.5, 'rank': 150, 'rank_wildcard': 100, 'additional_nonlinear': 'none', 'additional_states': 0, 'use_priority': 0, 'train_wildcard': 1, 'train_wildcard_wildcard': 1, 'train_c_output': 1, 'train_h0': 0, 'train_hT': 1, 'train_beta': 1, 'random': 0, 'random_pad_func': 'xavier', 'save_model': 0, 'independent': 2, 'use_unlabel': 0, 'farnn': 2, 'xavier': 1, 'bias_init': 1, 'sigmoid_exponent': 1, 'use_crf': 0, 'update_nonlinear': 'tanh', 'args_path': 'none', 'bert_finetune': 0, 'use_bert': 0, 'warm_up': 0, 'bert_lr_down_factor': 1, 'bert_init_embed': 'aggregate'}
max_len: 42, avg_len: 10.959819186338523
max_len: 37, avg_len: 10.97289156626506
max_len: 39, avg_len: 10.052631578947368
max_len: 42, avg_len: 10.959819186338523
max_len: 37, avg_len: 10.97289156626506
max_len: 39, avg_len: 10.052631578947368
Train Samples:  3982
../data/ATIS-ZH-BIO/automata/IIID.automata.0308133803-1615210683.6103313.svd.2best.104states.random.3splits.100-0.1496150-0.0934200-0.0541.bio.rules.v1.config.pkl
AUTOMATA STATES NUM: 104
LANGUAGE SET SIZE: 170
  0%|                                                                       | 0/14 [00:00<?, ?it/s]
Traceback (most recent call last):
  File "main.py", line 194, in <module>
    train_slot_decompose(args)
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/train_decompose.py", line 51, in train_slot_decompose
    slot_data_train = SlotBatchDataset(train_query, train_lengths, slot_train, args, s2i,
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/data.py", line 164, in __init__
    train_pred, dev_pred, test_pred, train_score, dev_score, test_score = predict_by_RE(args)
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/RE.py", line 184, in predict_by_RE
    results_train, score_train = get_RE_prediction(slot_dataloader_train, model, args_bak, s2i['o'], i2s) # N x L x C
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/RE.py", line 23, in get_RE_prediction
    for batch in data:
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/tqdm/std.py", line 1182, in __iter__
    for obj in iterable:
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/torch/utils/data/dataloader.py", line 633, in __next__
    data = self._next_data()
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/torch/utils/data/dataloader.py", line 677, in _next_data
    data = self._dataset_fetcher.fetch(index)  # may raise StopIteration
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/torch/utils/data/_utils/fetch.py", line 51, in fetch
    data = [self.dataset[idx] for idx in possibly_batched_index]
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/torch/utils/data/_utils/fetch.py", line 51, in <listcomp>
    data = [self.dataset[idx] for idx in possibly_batched_index]
  File "/home/ye/exp/RE2NN-SEQ/src_seq/../src_seq/data.py", line 148, in __getitem__
    'x': np.array(self.dataset[idx], dtype=np.int),
  File "/home/ye/anaconda3/envs/re2nn_seq/lib/python3.8/site-packages/numpy/__init__.py", line 305, in __getattr__
    raise AttributeError(__former_attrs__[attr])
AttributeError: module 'numpy' has no attribute 'int'.
`np.int` was a deprecated alias for the builtin `int`. To avoid this error in existing code, use `int` by itself. Doing this will not modify any behavior and is safe. When replacing `np.int`, you may wish to use e.g. `np.int64` or `np.int32` to specify the precision. If you wish to review your current use, check the release note link for additional information.
The aliases was originally deprecated in NumPy 1.20; for more details and guidance see the original release note at:
    https://numpy.org/devdocs/release/1.20.0-notes.html#deprecations
(re2nn_seq) ye@lst-gpu-3090:~/exp/RE2NN-SEQ/src_seq$



## Reference

1. https://github.com/jeffchy/RE2NN-SEQ
2. https://github.com/jeffchy/RE2RNN

