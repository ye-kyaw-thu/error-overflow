# pcrf (Python Conditional Random Fields) Progam Installation and Testing Log

တောက်လျှောက်လိုလို CRF++, CRFSuite toolkit တွေကိုပဲ statistical sequence-to-sequence learning experiment တွေလုပ်တဲ့အခါမှာ သုံးဖြစ်ခဲ့ပါတယ်။  
ဒီ pcrf ကတော့ CRF ကိုပဲ python version အနေနဲ့ စမ်းရေးထားတဲ့ ပရိုဂရမ်လို့ ယူဆပါတယ်။  
link: [https://github.com/hitwsl/pcrf](https://github.com/hitwsl/pcrf)  

ကျောင်းသား တစ်ယောက်က CRF++, CRFSuite နဲ့ training လုပ်တာ memory insufficient error ဖြစ်နေတယ်ဆိုလို့ ဒီ pcrf က မြန်တာနဲ့ memory managment လုပ်ပေးတာ ကောင်းတယ်ဆိုလို့ စမ်းသုံးကြည့်ရင်း မှတ်ထားတဲ့ installation, training, testing log ဖိုင်ပါ။  

ဒီ pcrf tool က Python 2.7 version ကို သုံးထားတာမို့ အကောင်းဆုံးကတော့ Python 2.7 environment ကို ကိုယ့်စက်ထဲမှာ ပြင်ဆင်ပြီးတော့ pcrf ကို သုံးတာက အကောင်းဆုံးပါပဲ။ 2to3 tool (Python 2 ပရိုဂရမ်တွေကို 3 version ပြောင်းဖို့) ကို သုံးပြီး pcrf ကို Python 3 version အဖြစ် ပြောင်းလို့ရပေမဲ့ သူက ခေါ်သုံးထားတဲ့ library ကလည်း အားလုံး match ဖြစ်ဖို့ လိုအပ်တာကြောင့် ကျွန်တော်ကတော့ py2.7 environment အသစ်ကို လုပ်ပြီးတော့ စမ်းကြည့်ခဲ့ပါတယ်။ enviornment control လုပ်တာကတော့ Anaconda ကို သုံးပြီးတော့ လုပ်ပါတယ်။    

အရင်ဆုံး ကိုယ့်စက်ထဲမှာ python 2.7 env က ရှိမရှိကို check လုပ်ကြည့်ရအောင်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/pcrf$ conda info --envs
# conda environments:
#
base                  *  /home/ye/tool/anaconda3
conda3.6                 /home/ye/tool/anaconda3/envs/conda3.6
persephone               /home/ye/tool/anaconda3/envs/persephone
tensorflow               /home/ye/tool/anaconda3/envs/tensorflow
```

"conda" command နဲ့ environment အသစ် ကို "py2.7" ဆိုတဲ့ နာမည်နဲ့ ဖန်တီးရင်းနဲ့ python ကိုလည်း ကိုယ်လိုချင်တဲ့ ဗားရှင်း 2.7 အတိအကျ သတ်မှတ်ပြီး သွားကြရအောင်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/pcrf$ conda create -n py2.7 python=2.7
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: done


==> WARNING: A newer version of conda exists. <==
  current version: 4.8.2
  latest version: 4.8.3

Please update conda by running

    $ conda update -n base -c defaults conda



## Package Plan ##

  environment location: /home/ye/tool/anaconda3/envs/py2.7

  added / updated specs:
    - python=2.7


The following packages will be downloaded:

    package                    |            build
    ---------------------------|-----------------
    ca-certificates-2020.6.24  |                0         125 KB
    certifi-2019.11.28         |           py27_0         153 KB
    libedit-3.1.20191231       |       h7b6447c_0         167 KB
    libffi-3.3                 |       he6710b0_2          50 KB
    pip-19.3.1                 |           py27_0         1.7 MB
    python-2.7.18              |       h15b4118_1         9.9 MB
    setuptools-44.0.0          |           py27_0         512 KB
    sqlite-3.32.3              |       h62c20be_0         1.1 MB
    tk-8.6.10                  |       hbc83047_0         3.0 MB
    wheel-0.33.6               |           py27_0          42 KB
    ------------------------------------------------------------
                                           Total:        16.6 MB

The following NEW packages will be INSTALLED:

  _libgcc_mutex      pkgs/main/linux-64::_libgcc_mutex-0.1-main
  ca-certificates    pkgs/main/linux-64::ca-certificates-2020.6.24-0
  certifi            pkgs/main/linux-64::certifi-2019.11.28-py27_0
  libedit            pkgs/main/linux-64::libedit-3.1.20191231-h7b6447c_0
  libffi             pkgs/main/linux-64::libffi-3.3-he6710b0_2
  libgcc-ng          pkgs/main/linux-64::libgcc-ng-9.1.0-hdf63c60_0
  libstdcxx-ng       pkgs/main/linux-64::libstdcxx-ng-9.1.0-hdf63c60_0
  ncurses            pkgs/main/linux-64::ncurses-6.2-he6710b0_1
  pip                pkgs/main/linux-64::pip-19.3.1-py27_0
  python             pkgs/main/linux-64::python-2.7.18-h15b4118_1
  readline           pkgs/main/linux-64::readline-8.0-h7b6447c_0
  setuptools         pkgs/main/linux-64::setuptools-44.0.0-py27_0
  sqlite             pkgs/main/linux-64::sqlite-3.32.3-h62c20be_0
  tk                 pkgs/main/linux-64::tk-8.6.10-hbc83047_0
  wheel              pkgs/main/linux-64::wheel-0.33.6-py27_0
  zlib               pkgs/main/linux-64::zlib-1.2.11-h7b6447c_3


Proceed ([y]/n)? y


Downloading and Extracting Packages
libedit-3.1.20191231 | 167 KB    | ########################################################################################## | 100% 
libffi-3.3           | 50 KB     | ########################################################################################## | 100% 
wheel-0.33.6         | 42 KB     | ########################################################################################## | 100% 
tk-8.6.10            | 3.0 MB    | ########################################################################################## | 100% 
pip-19.3.1           | 1.7 MB    | ########################################################################################## | 100% 
certifi-2019.11.28   | 153 KB    | ########################################################################################## | 100% 
ca-certificates-2020 | 125 KB    | ########################################################################################## | 100% 
python-2.7.18        | 9.9 MB    | ########################################################################################## | 100% 
sqlite-3.32.3        | 1.1 MB    | ########################################################################################## | 100% 
setuptools-44.0.0    | 512 KB    | ########################################################################################## | 100% 
Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate py2.7
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```

"conda activate" command နဲ့ အသစ် create လုပ်ခဲ့တဲ့ py2.7 enviornment အောက်ကို ဝင်ရအောင်။  

```
(base) ye@ykt-pro:/media/ye/project1/tool/pcrf$ conda activate py2.7
```

pcrf ကို git clone လုပ်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool$ git clone https://github.com/hitwsl/pcrf
Cloning into 'pcrf'...
remote: Enumerating objects: 34, done.
remote: Total 34 (delta 0), reused 0 (delta 0), pack-reused 34
Unpacking objects: 100% (34/34), done.
```

pcrf ဖိုလ်ဒါအောက်ကို ဝင်ပြီး ဖိုင်တွေကို ကြည့်ရအောင်။  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool$ cd pcrf
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ ls
LinearCRF2.py  pcrf-train.py  templatechunk       testchunk.data  trainchunk.data
pcrf-test.py   README.md      templatesimple.txt  train1.txt      trainsimple.data
```

pcrf-train command ကို ရိုက်ထည့်ပြီး help screen ကြည့်လို့ ရပြီလား confirm လုပ်ရအောင်  


```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ python ./pcrf-train.py 
Traceback (most recent call last):
  File "./pcrf-train.py", line 12, in <module>
    import LinearCRF2 
  File "/media/ye/project1/tool/pcrf/LinearCRF2.py", line 19, in <module>
    from scipy.misc import logsumexp
ImportError: No module named scipy.misc
```

scipy လိုတာမို့ scipy ကို install လုပ်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ pip install scipy
DEPRECATION: Python 2.7 will reach the end of its life on January 1st, 2020. Please upgrade your Python as Python 2.7 won't be maintained after that date. A future version of pip will drop support for Python 2.7. More details about Python 2 support in pip, can be found at https://pip.pypa.io/en/latest/development/release-process/#python-2-support
Collecting scipy
  Downloading https://files.pythonhosted.org/packages/24/40/11b12af7f322c1e20446c037c47344d89bab4922b8859419d82cf56d796d/scipy-1.2.3-cp27-cp27mu-manylinux1_x86_64.whl (24.8MB)
     |████████████████████████████████| 24.8MB 557kB/s 
Requirement already satisfied: numpy>=1.8.2 in /home/ye/.local/lib/python2.7/site-packages (from scipy) (1.16.6)
Installing collected packages: scipy
Successfully installed scipy-1.2.3
```

pcrf-train.py ကို run ပြီး help screen ကြည့်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ python ./pcrf-train.py 
usage: pcrf-train.py [-h] [-r {0,1,2}] [-s SIGMA] [-m {0,1}] [-f FD]
                     datafile templatefile modelfile
pcrf-train.py: error: too few arguments
```

## Train simple model

template ဖိုင် format က CRF++ နဲ့ အတူတူပါပဲ။  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ cat templatesimple.txt 
# Unigram

U00:%x[0,0]
U01:%x[0,1]

# Bigram
#B00:%x[0,0]/%x[0,1]
```

pcrf က ကိုယ့်စက်ထဲမှာ run လို့ ရမရ simple model data ကိုနဲ့ train လုပ်ကြည့်ရအောင်။  
အရင်ဆုံး trainsimple.data ကို ကြည့်ကြည့်ရအောင်။  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ head trainsimple.data 
1 1 A
2 1 B
1 2 O
1 1 A
2 1 B
2 2 O
```

training လုပ်တာ အိုကေတယ်။ အောက်ပါအတိုင်းပါ  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ time python pcrf-train.py trainsimple.data templatesimple.txt simple-crf-model | tee simple-model-train.log
Valid Template Line Number: 3
number of labels: 3
Linear CRF in Python.. ver 0.1 
B features: 9 U features: 12 total num: 21
training sequence number: 1
start to calculate ON feature.  elapsed time: 0.000795841217041 seconds. 
 
start to calculate data distribuition. elapsed time: 0.0026159286499 seconds. 
 
start to translate ON Feature list to Array.  elapsed time: 0.00270199775696 seconds. 
 
start to learn distribuition. elapsed time: 0.00276803970337 seconds. 
 
 This problem is unconstrained.
Training finished in  0.110992908478 seconds. 
 
RUNNING THE L-BFGS-B CODE

           * * *

Machine precision = 2.220D-16
 N =           21     M =           10

At X0         0 variables are exactly at the bounds

At iterate    0    f=  1.81903D+01    |proj g|=  2.33333D+00

At iterate    1    f=  1.26906D+01    |proj g|=  1.71428D+00

At iterate    2    f=  4.06041D+00    |proj g|=  4.55241D-01

At iterate    3    f=  3.88184D+00    |proj g|=  5.78248D-01

At iterate    4    f=  3.68840D+00    |proj g|=  6.51124D-02

At iterate    5    f=  3.68337D+00    |proj g|=  2.65868D-02

At iterate    6    f=  3.68267D+00    |proj g|=  2.34244D-03

           * * *

Tit   = total number of iterations
Tnf   = total number of function evaluations
Tnint = total number of segments explored during Cauchy searches
Skip  = number of BFGS updates skipped
Nact  = number of active bounds at final generalized Cauchy point
Projg = norm of the final projected gradient
F     = final function value

           * * *

   N    Tit     Tnf  Tnint  Skip  Nact     Projg        F
   21      6      7      1     0     0   2.342D-03   3.683D+00
  F =   3.6826677816082776     

CONVERGENCE: REL_REDUCTION_OF_F_<=_FACTR*EPSMCH             

 Cauchy                time 0.000E+00 seconds.
 Subspace minimization time 0.000E+00 seconds.
 Line search           time 0.000E+00 seconds.

 Total User time 0.000E+00 seconds.


real	0m0.341s
user	0m0.423s
sys	0m0.458s
```

## Testing with simple model


train လုပ်ခဲ့ simple-crf-model ကို testing လုပ်ကြည့်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ python pcrf-test.py trainsimple.data simple-crf-model result.txt
number of labels: 3
Linear CRF in Python.. ver 0.1 
B features: 9 U features: 12 total num: 21
Prediction sequence number: 1
Note: If Y is useless, correct rate is also useless.
correct: 7 error: 0  correct rate: 1.0
Write max(y) to file: result.txt
Test finished in  0.00246095657349 seconds. 
```

Result ဖိုင်ကို ကြည့်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ cat result.txt 
1 1 A A
2 1 B B
1 2 O O
1 1 A A
2 1 B B
2 2 O O
2 2 O O
```

training data နဲ့ Confirmation လုပ်ကြည့်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ cat trainsimple.data 
1 1 A
2 1 B
1 2 O
1 1 A
2 1 B
2 2 O
```

## Chunking Training

Note: You should know ... Chunking = Segmentation  


### Check the chunking training data  

chunking မော်ဒယ် ဆောက်တဲ့အခါမှာ သုံးထားတဲ့ training data ဖိုင်ကို ကြည့်ရအောင်  
well known ဒေတာဖြစ်တဲ့ CoNLL shared task ဒေတာဖြစ်တာကို အောက်ပါအတိုင်း တွေ့ရပါလိမ့်မယ်။  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ head -n 30 trainchunk.data 
Rockwell NNP B-NP
International NNP I-NP
Corp. NNP I-NP
's POS B-NP
Tulsa NNP I-NP
unit NN I-NP
said VBD B-VP
it PRP B-NP
signed VBD B-VP
a DT B-NP
tentative JJ I-NP
agreement NN I-NP
extending VBG B-VP
its PRP$ B-NP
contract NN I-NP
with IN B-PP
Boeing NNP B-NP
Co. NNP I-NP
to TO B-VP
provide VB I-VP
structural JJ B-NP
parts NNS I-NP
for IN B-PP
Boeing NNP B-NP
's POS B-NP
747 CD I-NP
jetliners NNS I-NP
. . O

Rockwell NNP B-NP
```

### Check the template

Note: Template is important and you should defined the template at first!  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ cat templatechunk 
# Unigram
U00:%x[-2,0]
U01:%x[-1,0]
U02:%x[0,0]
U03:%x[1,0]
U04:%x[2,0]
U05:%x[-1,0]/%x[0,0]
U06:%x[0,0]/%x[1,0]

U10:%x[-2,1]
U11:%x[-1,1]
U12:%x[0,1]
U13:%x[1,1]
U14:%x[2,1]
U15:%x[-2,1]/%x[-1,1]
U16:%x[-1,1]/%x[0,1]
U17:%x[0,1]/%x[1,1]
U18:%x[1,1]/%x[2,1]

U20:%x[-2,1]/%x[-1,1]/%x[0,1]
U21:%x[-1,1]/%x[0,1]/%x[1,1]
U22:%x[0,1]/%x[1,1]/%x[2,1]

# Bigram
B
```

### Start chunking training

model တစ်ခုခု training လုပ်တဲ့အခါမှာ အချိန်ကို time command နဲ့ မှတ်ပါ။  
log ဖိုင်ကို tee command ကို သုံးပြီး log လုပ်ပါ။  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ time python pcrf-train.py trainchunk.data templatechunk chunk-model | tee chunk-train.log
Valid Template Line Number: 20
read  10000  lines.
number of labels: 17
Linear CRF in Python.. ver 0.1 
B features: 289 U features: 1075420 total num: 1075709
training sequence number: 823
start to calculate ON feature.  elapsed time: 1.16383886337 seconds. 
 
start to calculate data distribuition. elapsed time: 2.55806398392 seconds. 
 
start to translate ON Feature list to Array.  elapsed time: 2.707477808 seconds. 
 
start to learn distribuition. elapsed time: 2.78054189682 seconds. 
 
 This problem is unconstrained.
Training finished in  249.339183807 seconds. 
 
RUNNING THE L-BFGS-B CODE

           * * *

Machine precision = 2.220D-16
 N =      1075709     M =           10

At X0         0 variables are exactly at the bounds

At iterate    0    f=  5.92173D+05    |proj g|=  3.40110D+03

At iterate    1    f=  5.58652D+05    |proj g|=  9.13437D+02

At iterate    2    f=  5.50099D+05    |proj g|=  5.83557D+02

At iterate    3    f=  5.43316D+05    |proj g|=  5.73924D+02

At iterate    4    f=  5.38117D+05    |proj g|=  3.95405D+02

At iterate    5    f=  5.27336D+05    |proj g|=  2.91940D+02

At iterate    6    f=  4.83173D+05    |proj g|=  6.08900D+02

At iterate    7    f=  2.53210D+05    |proj g|=  2.89616D+02

At iterate    8    f=  2.24518D+05    |proj g|=  6.05618D+02

At iterate    9    f=  2.04211D+05    |proj g|=  2.17400D+02

At iterate   10    f=  1.94187D+05    |proj g|=  1.88309D+02

At iterate   11    f=  1.54187D+05    |proj g|=  3.51276D+02

At iterate   12    f=  1.22164D+05    |proj g|=  7.73884D+02

At iterate   13    f=  9.22271D+04    |proj g|=  1.14029D+02

At iterate   14    f=  6.84268D+04    |proj g|=  1.91973D+02

At iterate   15    f=  5.36072D+04    |proj g|=  1.31116D+02

At iterate   16    f=  3.67457D+04    |proj g|=  2.25346D+02

At iterate   17    f=  3.26626D+04    |proj g|=  9.50991D+02

At iterate   18    f=  2.88809D+04    |proj g|=  8.76689D+01

At iterate   19    f=  2.38827D+04    |proj g|=  1.32767D+02

At iterate   20    f=  2.04486D+04    |proj g|=  2.18558D+02

At iterate   21    f=  1.73049D+04    |proj g|=  7.18082D+01

At iterate   22    f=  1.35755D+04    |proj g|=  6.76905D+01

At iterate   23    f=  1.10811D+04    |proj g|=  6.96432D+01

At iterate   24    f=  8.80753D+03    |proj g|=  3.33175D+02

At iterate   25    f=  7.65205D+03    |proj g|=  7.56090D+01

At iterate   26    f=  7.22493D+03    |proj g|=  4.14806D+01

At iterate   27    f=  6.24169D+03    |proj g|=  1.28398D+02

At iterate   28    f=  5.16555D+03    |proj g|=  6.24375D+01

At iterate   29    f=  4.44144D+03    |proj g|=  5.38560D+01

At iterate   30    f=  3.88163D+03    |proj g|=  6.43275D+01

At iterate   31    f=  3.51811D+03    |proj g|=  5.22784D+01

At iterate   32    f=  3.11205D+03    |proj g|=  2.86363D+01

At iterate   33    f=  2.73050D+03    |proj g|=  5.15683D+01

At iterate   34    f=  2.33633D+03    |proj g|=  8.34775D+01

At iterate   35    f=  2.10830D+03    |proj g|=  5.64670D+01

At iterate   36    f=  1.96106D+03    |proj g|=  1.19437D+01

At iterate   37    f=  1.77445D+03    |proj g|=  1.61362D+01

At iterate   38    f=  1.59217D+03    |proj g|=  3.99509D+01

At iterate   39    f=  1.46075D+03    |proj g|=  2.23011D+01

At iterate   40    f=  1.40919D+03    |proj g|=  9.04398D+00

At iterate   41    f=  1.34807D+03    |proj g|=  9.05384D+00

At iterate   42    f=  1.27981D+03    |proj g|=  3.58240D+01

At iterate   43    f=  1.26156D+03    |proj g|=  2.60162D+01

At iterate   44    f=  1.24498D+03    |proj g|=  2.15540D+01

At iterate   45    f=  1.21631D+03    |proj g|=  5.04052D+00

At iterate   46    f=  1.19813D+03    |proj g|=  4.31169D+00

At iterate   47    f=  1.19267D+03    |proj g|=  4.36466D+01

At iterate   48    f=  1.17752D+03    |proj g|=  6.66392D+00

At iterate   49    f=  1.17298D+03    |proj g|=  4.58076D+00

At iterate   50    f=  1.16742D+03    |proj g|=  1.09453D+01

At iterate   51    f=  1.16059D+03    |proj g|=  9.88177D+00

At iterate   52    f=  1.15349D+03    |proj g|=  1.37096D+01

At iterate   53    f=  1.15054D+03    |proj g|=  4.47652D+00

At iterate   54    f=  1.14890D+03    |proj g|=  2.46576D+00

At iterate   55    f=  1.14761D+03    |proj g|=  1.39717D+01

At iterate   56    f=  1.14642D+03    |proj g|=  3.82246D+00

At iterate   57    f=  1.14546D+03    |proj g|=  1.56835D+00

At iterate   58    f=  1.14436D+03    |proj g|=  3.93254D+00

At iterate   59    f=  1.14355D+03    |proj g|=  2.06342D+00

At iterate   60    f=  1.14296D+03    |proj g|=  6.14356D+00

At iterate   61    f=  1.14233D+03    |proj g|=  6.15748D-01

At iterate   62    f=  1.14213D+03    |proj g|=  9.20881D-01

           * * *

Tit   = total number of iterations
Tnf   = total number of function evaluations
Tnint = total number of segments explored during Cauchy searches
Skip  = number of BFGS updates skipped
Nact  = number of active bounds at final generalized Cauchy point
Projg = norm of the final projected gradient
F     = final function value

           * * *

   N    Tit     Tnf  Tnint  Skip  Nact     Projg        F
*****     62     72      1     0     0   9.209D-01   1.142D+03
  F =   1142.1341715318472     

CONVERGENCE: REL_REDUCTION_OF_F_<=_FACTR*EPSMCH             

 Cauchy                time 0.000E+00 seconds.
 Subspace minimization time 0.000E+00 seconds.
 Line search           time 0.000E+00 seconds.

 Total User time 0.000E+00 seconds.


real	4m9.594s
user	13m39.250s
sys	0m42.963s
```

### Check the test data

test data ကို ကြည့်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ head -30 ./testchunk.data 
Confidence NN B-NP
in IN B-PP
the DT B-NP
pound NN I-NP
is VBZ B-VP
widely RB I-VP
expected VBN I-VP
to TO I-VP
take VB I-VP
another DT B-NP
sharp JJ I-NP
dive NN I-NP
if IN B-SBAR
trade NN B-NP
figures NNS I-NP
for IN B-PP
September NNP B-NP
, , O
due JJ B-ADJP
for IN B-PP
release NN B-NP
tomorrow NN B-NP
, , O
fail VB B-VP
to TO I-VP
show VB I-VP
a DT B-NP
substantial JJ I-NP
improvement NN I-NP
from IN B-PP
```

### Testing chunk-model with test data

Testing ကို အောက်ပါအတိုင်း လုပ်ခဲ့တယ် ...  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ time python pcrf-test.py testchunk.data chunk-model result.txt | tee test-chunk.log
number of labels: 14
Linear CRF in Python.. ver 0.1 
B features: 289 U features: 1075420 total num: 1075709
Prediction sequence number: 77
Note: If Y is useless, correct rate is also useless.
correct: 1757 error: 139  correct rate: 0.926687763713
Write max(y) to file: result.txt
Test finished in  1.36823821068 seconds. 
 

real	0m1.629s
user	0m1.294s
sys	0m0.449s
```

### Check the result file

result.txt ဖိုင်ကိုလည်း Check လုပ်ရအောင်  

```
(py2.7) ye@ykt-pro:/media/ye/project1/tool/pcrf$ head -30 result.txt 
Confidence NN B-NP B-NP
in IN B-PP B-PP
the DT B-NP B-NP
pound NN I-NP I-NP
is VBZ B-VP B-VP
widely RB I-VP I-VP
expected VBN I-VP I-VP
to TO I-VP I-VP
take VB I-VP I-VP
another DT B-NP B-NP
sharp JJ I-NP I-NP
dive NN I-NP I-NP
if IN B-SBAR B-PP
trade NN B-NP B-NP
figures NNS I-NP I-NP
for IN B-PP B-PP
September NNP B-NP B-NP
, , O O
due JJ B-ADJP B-ADJP
for IN B-PP B-PP
release NN B-NP B-NP
tomorrow NN B-NP I-NP
, , O O
fail VB B-VP B-VP
to TO I-VP I-VP
show VB I-VP I-VP
a DT B-NP B-NP
substantial JJ I-NP I-NP
improvement NN I-NP I-NP
from IN B-PP B-PP
```
