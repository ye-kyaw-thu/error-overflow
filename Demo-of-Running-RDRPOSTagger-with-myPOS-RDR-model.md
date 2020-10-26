
## Preparing a new folder
(base) ye@ykt-pro:/media/ye/project1/4github$ mkdir demo-of-RDR-myPOS-using
(base) ye@ykt-pro:/media/ye/project1/4github$ cd demo-of-RDR-myPOS-using/
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using$ 

## Cloning myPOS
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using$ git clone https://github.com/ye-kyaw-thu/myPOS
Cloning into 'myPOS'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 2143 (delta 0), reused 0 (delta 0), pack-reused 2139
Receiving objects: 100% (2143/2143), 89.40 MiB | 503.00 KiB/s, done.
Resolving deltas: 100% (1469/1469), done.
Checking out files: 100% (999/999), done.

## Check and Move to RDR Model Folder

(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using$ ls
myPOS
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using$ cd myPOS/
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS$ ls
CICLING2017  corpus-draft-ver-0.9  corpus-draft-ver-1.0  README.md
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS$ cd corpus-draft-ver-1.0/
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0$ ls
data         mk-wordtag.pl             mypos-dver.1.0.lcw.txt       mypos-dver.1.0.txt
how2run.txt  model                     mypos-dver.1.0.lcw.uniq.txt  mypos-dver.1.0.word.txt
mk-pair.pl   mypos-dver.1.0.cword.txt  mypos-dver.1.0.tag.txt       Note.txt
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0$ cd model
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model$ ls
3gHMM  crf  kytea  low-resource-pos-tagging-2014  maxent  rdr
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model$ cd rdr
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr$ ls
evaluate-all.sh  otest              pipe2space-all.sh          rdr-train.log  t3  t7           train-rdr-all.sh
evaluate.py      otest.nopipe       prepare-word-files4rdr.sh  t1             t4  t8
mk-wordtag.pl    otest.nopipe.col   rdr-evaluate-results.log   t10            t5  t9
note.txt         otest.nopipe.word  rdr-test.log               t2             t6  test-all.sh
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr$ cd t10
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ ls
ctest10              ctest10.nopipe.word.TAGGED  train10              train10.nopipe.RDR
ctest10.nopipe       otest.nopipe.word           train10.nopipe       train10.nopipe.word
ctest10.nopipe.word  otest.nopipe.word.TAGGED    train10.nopipe.DICT  train10.shuf

## Path of my RDRPOSTagger

(base) ye@ykt-pro:/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger$ ls
double.log          hex2uni.py~  myro            RDRPOSTagger4En.py  RDRPOSTagger.py~  test.sh~          train.sh~
ExtRDRPOSTagger.py  __init__.py  myro.train.out  RDRPOSTagger4Vn.py  romy.train.out    train.myro.slash  train-test.log
hex2uni.py          log          myseg           RDRPOSTagger.py     test.sh           train.sh

## Preparing test file

(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ gedit new-test.txt
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ cat ./new-test.txt
ဘာ နေရာ မှာ ခက် နေ တာ လဲ ။
ကြိုးစား ပါ အဆင်ပြေ ရ မယ်

## Try Tagging with RDRPOSTagger

(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ python /media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger/RDRPOSTagger.py tag ./train10.nopipe.RDR ./train10.nopipe.DICT ./new-test.txt 
Traceback (most recent call last):
  File "/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger/RDRPOSTagger.py", line 9, in <module>
    os.chdir("./pSCRDRtagger")
FileNotFoundError: [Errno 2] No such file or directory: './pSCRDRtagger'

## Try agin

(base) ye@ykt-pro:/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger$ python ./RDRPOSTagger.py tag /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.RDR /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.DICT /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/new-test.txt 

=> Read a POS tagging model from /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.RDR

=> Read a lexicon from /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.DICT

=> Perform POS tagging on /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/new-test.txt

Output file: /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/new-test.txt.TAGGED
(base) ye@ykt-pro:/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger$

## Checked the POS tagged output file

(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ cat ./new-test.txt.TAGGED 
ဘာ/pron နေရာ/n မှာ/ppm ခက်/adj နေ/part တာ/part လဲ/part ။/punc
ကြိုးစား/v ပါ/part အဆင်ပြေ/v ရ/part မယ်/ppm

