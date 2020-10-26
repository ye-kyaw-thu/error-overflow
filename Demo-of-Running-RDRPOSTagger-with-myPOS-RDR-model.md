# Demo of How to make POS tagging with trained myPOS Burmese RDR Tagger

မြန်မာကျောင်းသူ တစ်ယောက်က ကျွန်တော့်ဆီကို myPOS RDR မော်ဒယ်နဲ့ ဗမာစာကြောင်းတွေကို POS tagging လုပ်ဖို့ ကြိုးစားနေတာ အကြိမ်ကြိမ်အခါခါ ရှိပေမဲ့ ခက်ခဲနေတယ်လို့ အီးမေးလ်နဲ့ အကူအညီတောင်းတာကို ကြုံရလို့ ဒီ error-overflow မှာ အကြမ်းရှင်းပြလိုက်ပါတယ်။ ဘယ်နေရာမှာ error တက်နေတယ်ဆိုတာကိုလည်း အီးမေးလ်ထဲမှာက မဖော်ပြထားလို့ အခြေခံအားဖြင့် command line သုံးတဲ့ အတွေ့အကြုံနည်းလို့ သို့မဟုတ် python program ကို run တဲ့နေရာမှာ အောက်မှာ ပြထားသလို error မျိုး တက်နေတာကြောင့်လို့ ယူဆပါတယ်။ နဂို RDR POSTagger python ပရိုဂရမ်ကလည်း original author က သူ့ experiment အတွက်ပဲ အကြမ်းရေးထားတာကြောင့် coding, debugging စတဲ့ အတွေ့အကြုံတွေ သိပ်မရှိလို့ POS tagging လုပ်ဖို့အတွက် ခက်ခဲနေတာလို့ နားလည်ပါတယ်။  

myPOS ကို သုံးဖို့ ကြိုးစားတာကို သိရလို့ ဝမ်းသာရပါတယ်။ အောက်မှာ ပြထားတဲ့ အဆင့်တွေက ပထမဆုံး myPOS RDR model ကိုအသုံးပြုမယ့် သူတွေအတွက် အတိုင်းအတာ တစ်ခုအထိ အသုံးဝင်ပါလိမ့်မယ်။  

## Cloning myPOS

GitHub မှာတင်ထားတဲ့ repository ကို ကိုယ့်စက်ထဲကို download လုပ်တဲ့အဆင့်ဖြစ်ပါတယ်။  
ကိုယ့်စက်ထဲမှာတော့ git command ကို run ဖို့အတွက် မရှိသေးဘူး ဆိုရင်တော့ "sudo apt install git" ဆိုတဲ့ command မျိုးနဲ့ install လုပ်ရပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using$ git clone https://github.com/ye-kyaw-thu/myPOS
Cloning into 'myPOS'...
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 2143 (delta 0), reused 0 (delta 0), pack-reused 2139
Receiving objects: 100% (2143/2143), 89.40 MiB | 503.00 KiB/s, done.
Resolving deltas: 100% (1469/1469), done.
Checking out files: 100% (999/999), done.
```

အထက်ပါ git clone နဲ့ repository ကို ကော်ပီကူးဖို့ အခက်တွေ့နေရင် Download button ကို သုံးပြီးတော့ myPOS repository တစ်ခုလုံးကို ကိုယ့်စက်ထဲကို download လုပ်ရင်လည်း အဆင်ပြေပါလိမ့်မယ်။  

## Move to RDR Model Folder and Check files

Clone လုပ်ပြီး ရရှိလာတဲ့ myPOS ဖိုလ်ဒါထဲကို ဝင်ပြီး ရှိတဲ့ ဖိုင်တွေ၊ ဖိုလ်ဒါတွေကို လေ့လာရင်းနဲ့ RDR model ရှိတဲ့ path အောက်ကို ရောက်အောင် သွားရပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using$ ls
myPOS
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using$ cd myPOS/
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS$ ls
CICLING2017  corpus-draft-ver-0.9  corpus-draft-ver-1.0  README.md
```

လက်ရှိ တင်ပေးထားတဲ့အထဲမှာ version 1.0 က အမြင့်ဆုံးပါ။ (version 2.0 ကို ဒီနှစ်ကုန်မှာ တင်ပေးနိုင်ဖို့ ပြင်ဆင်နေပါတယ်)  
ver-1.0 အောက်ထဲကို cd command နဲ့ ဝင်ရအောင်...  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS$ cd corpus-draft-ver-1.0/
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0$ ls
data         mk-wordtag.pl             mypos-dver.1.0.lcw.txt       mypos-dver.1.0.txt
how2run.txt  model                     mypos-dver.1.0.lcw.uniq.txt  mypos-dver.1.0.word.txt
mk-pair.pl   mypos-dver.1.0.cword.txt  mypos-dver.1.0.tag.txt       Note.txt
```

model ဆိုတဲ့ ဖိုလ်ဒါအောက်မှာ approach ခြောက်မျိုးနဲ့ training လုပ်ထားတဲ့ ဖိုလ်ဒါတွေကို အောက်ပါအတိုင်း မြင်ရပါလိမ့်မယ်...  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0$ cd model
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model$ ls
3gHMM  crf  kytea  low-resource-pos-tagging-2014  maxent  rdr
```

RDR model ကို သုံးမှာမို့၊ rdr/ ဖိုလ်ဒါအောက်ကို ဝင်ရအောင် ...  
```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model$ cd rdr
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr$ ls
evaluate-all.sh  otest              pipe2space-all.sh          rdr-train.log  t3  t7           train-rdr-all.sh
evaluate.py      otest.nopipe       prepare-word-files4rdr.sh  t1             t4  t8
mk-wordtag.pl    otest.nopipe.col   rdr-evaluate-results.log   t10            t5  t9
note.txt         otest.nopipe.word  rdr-test.log               t2             t6  test-all.sh
```

တကယ်တမ်းက training data နဲ့ မော်ဒယ်ကို တစ်ခါပဲ train လုပ်လို့လည်း ရပေမဲ့ incremental POS tagging experiment လုပ်တာမို့ t{0..10} အထိ ဖိုလ်ဒါ ၁၀ခုကွဲနေပါလိမ့်မယ်။ t0 က training ဒေတာ 1000 စာကြောင်းနဲ့ training လုပ်ထားတာပါ။ t1 က training ဒေတာ 2000 စသည်ဖြင့် ဒေတာကို တစ်ထောင်စီ တိုးတိုးပြီး training လုပ်သွားတာပါ။ ဖိုင်နာမည်တွေက train1, train2 ... train10 ဆိုပြီး ပေးထားခဲ့တာမို့ အဲဒီဖိုင် တစ်ဖိုင်ချင်းစီရဲ့ စာကြောင်းရေအရေအတွက်ကို wc (word count) command နဲ့ ကြည့်ကြည့်ရင် အောက်ပါအတိုင်း တွေ့ရပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr$ for i in {1..10};do wc ./t$i/train$i; done;
  1000  20262 400530 ./t1/train1
  2000  39607 784811 ./t2/train2
   3000   59467 1178131 ./t3/train3
   4000   79198 1570479 ./t4/train4
   5000   98362 1949801 ./t5/train5
   6000  118434 2347169 ./t6/train6
   7000  138387 2738757 ./t7/train7
   8000  157848 3124390 ./t8/train8
   9000  177895 3521510 ./t9/train9
  10000  197625 3912071 ./t10/train10
```

လက်ရှိမှာက t10/ ဖိုလ်ဒါအောက်က train10 နဲ့ training လုပ်ထားတာက အကောင်းဆုံး performance ကို ပေးတာမို့ t10 ဖိုလ်ဒါအောက်ကို သွားရအောင်...  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr$ cd t10
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ ls
ctest10              ctest10.nopipe.word.TAGGED  train10              train10.nopipe.RDR
ctest10.nopipe       otest.nopipe.word           train10.nopipe       train10.nopipe.word
ctest10.nopipe.word  otest.nopipe.word.TAGGED    train10.nopipe.DICT  train10.shuf
```
အထက်မှာ မြင်ရတဲ့ ဖိုင်တွေထဲက ဘာဖိုင်တွေဘာလိမ့်ဆိုပြီး သိချင်တဲ့သူတွေလည်း ရှိနိုင်တာမို့ ဖိုင်တချို့နဲ့ ပတ်သက်ပြီး ရှင်းပြရရင်  
- ctest10 က closed-test 10 ပါ။  
- ctest10.nopipe ဆိုတဲ့ ဖိုင်ကတော့ ctest10 ဖိုင်ထဲကနေ compound word တွေရဲ့ boundary (pipe) ကို ဖြုတ်ထားတဲ့ ဖိုင်ပါ။  
- ctest10.nopipe.word ဆိုတဲ့ ဖိုင်ကတော့ word တွေပဲ ရှိနေပြီး POS tag တွေ မပါတဲ့ ဖိုင်ပါ။
- ctest10.nopipe.word.TAGGED ဆိုတဲ့ ဖိုင်ကတော့ train10 model နဲ့ tagging လုပ်ပြီးထွက်လာတဲ့ output ဖိုင်ဖြစ်ပါတယ်။  
- otest ကတော့ open test ဒေတာဖိုင်ဖြစ်ပါတယ်။  
- train10.nopipe.DICT ကတော့ dictionary ဖိုင် ဖြစ်ပါတယ်။  
- train10.nopipe.RDR ကတော့ RDR model ဖိုင် ဖြစ်ပါတယ်။  

## Path of my RDRPOSTagger

ကျွန်တော် train လုပ်ပေးထားတဲ့ RDR model ဖိုင်ကို သုံးဖို့အတွက်က RDRPOSTagger ဆိုတာကို ကိုယ့်စက်ထဲမှာ download လုပ်ထားရပါလိမ့်မယ်။  
- Sourceforge Link ကတော့ [http://rdrpostagger.sourceforge.net/](http://rdrpostagger.sourceforge.net/)  
- GitHub Link ကတော့ [https://github.com/datquocnguyen/RDRPOSTagger](https://github.com/datquocnguyen/RDRPOSTagger)  

ဒီနေရာမှာတော့ download လုပ်တာကို မပြထားပါဘူး။  
သုံးပြမှာက Python program မို့လို့ RDRPOSTaggger ကို သုံးဖို့အတွက် installation လည်းထူးထူးထွေထွေ လုပ်စရာမလိုအပ်ပါဘူး။  
ကျွန်တော့် စက်ထဲမှာ တော့ အောက်မှာ မြင်ရတဲ့အတိုင်း portable HDD တစ်လုံးရဲ့ path တစ်ခုမှာ installation လုပ်ထားပါတယ်။  

```
(base) ye@ykt-pro:/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger$ ls
double.log          hex2uni.py~  myro            RDRPOSTagger4En.py  RDRPOSTagger.py~  test.sh~          train.sh~
ExtRDRPOSTagger.py  __init__.py  myro.train.out  RDRPOSTagger4Vn.py  romy.train.out    train.myro.slash  train-test.log
hex2uni.py          log          myseg           RDRPOSTagger.py     test.sh           train.sh
```

## Preparing test file

POS tagging လုပ်တာကို စမ်းပြဖို့အတွက် test ဖိုင်တစ်ဖိုင်ကို gedit နဲ့ ဝင်ရိုက်ခဲ့ပါတယ်။ အဲဒီရိုက်ခဲ့တဲ့ ဗမာစာကြောင်းတို နှစ်ကြောင်းကိုလည်း cat command နဲ့ရိုက်ပြထားပါတယ်။  
```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ gedit new-test.txt
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ cat ./new-test.txt
ဘာ နေရာ မှာ ခက် နေ တာ လဲ ။
ကြိုးစား ပါ အဆင်ပြေ ရ မယ်
```

## Try Tagging with RDRPOSTagger

တစ်ခု သိထားစေချင်တာက RDRPOSTagger.py ပရိုဂရမ်ဖိုင်က open source အနေနဲ့ တင်ပေးထားတဲ့ ပရိုဂရမ်မို့လို့ နောက်ပြီးတော့ သုတေသနအတွက် သုံးခဲ့တဲ့ ပရိုဂရမ်ကို ရှဲလုပ်ထားတာမို့လို့ end user တွေအတွက် မရည်ရွယ်ထားပါဘူးလို့ နားလည်ပါတယ်။ အဲဒါကြောင့်လို့ထင်ပါတယ် coding က အနုစိပ်ရေးထားတာတော့ မဟုတ်ပါဘူး။ RDR ကို Installation လုပ်ထားတဲ့ path အောက်ကနေ ခေါ်မသုံးပဲနဲ့ စောစောက အထက်မှာပြခဲ့တဲ့ myPOS folder path အောက်ကနေ့ RDRPOSTagger လုပ်ဖို့ ကြိုးစားရင် အောက်ပါအတိုင်း error ပေးပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ python /media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger/RDRPOSTagger.py tag ./train10.nopipe.RDR ./train10.nopipe.DICT ./new-test.txt 
Traceback (most recent call last):
  File "/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger/RDRPOSTagger.py", line 9, in <module>
    os.chdir("./pSCRDRtagger")
FileNotFoundError: [Errno 2] No such file or directory: './pSCRDRtagger'
```
အထက်မှာ မြင်နေရတဲ့ error က os.chdir နဲ့ လက်ရှိရောက်နေတဲ့ path အောက်က pSCRDRtagger ဆိုတဲ့ path ထဲကိုဝင်ဖို့ ကြိုးစားတာကြောင့် ဖြစ်တဲ့ error ပါ။  

## Try agin

ကျွန်တော် run တဲ့ ပုံစံကတော့ RDRPOSTagger ကို download လုပ်ထားတဲ့ path အောက်ကနေပဲ run ပါတယ်။  
အောက်ပါမြင်ရတဲ့အတိုင်းပါပဲ။ RDR model ဖိုင်နဲ့ DICT ဖိုင် ပြီးတော့ test data ပြင်ဆင်ခဲ့တဲ့ ဖိုင်ရှိတဲ့ path တွေကိုတော့ သေသေချာချာ မှန်မှန်ကန်ကန် command line argument ပေးမှ ဖြစ်ပါလိမ့်မယ်။ အဲဒါဆိုရင်တော့ စာကြောင်း ၂ကြောင်း ရိုက်ထားတဲ့ ဖိုင်ကို POS tagging လုပ်ပေးသွားပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger$ python ./RDRPOSTagger.py tag /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.RDR /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.DICT /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/new-test.txt 

=> Read a POS tagging model from /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.RDR

=> Read a lexicon from /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/train10.nopipe.DICT

=> Perform POS tagging on /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/new-test.txt

Output file: /media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10/new-test.txt.TAGGED
(base) ye@ykt-pro:/media/ye/Transcend/tool/RDRPOSTagger/pSCRDRtagger$
```

## Checked the POS tagged output file

POS tagging လုပ်ပေးပြီး ထွက်လာတဲ့ ဖိုင်ကို .TAGGED ဆိုတဲ့ extension နဲ့ သိမ်းပေးတာကြောင့် အဲဒီဖိုင်ထဲက စာကြောင်းတွေကို စစ်ဆေးကြည့်ရင်တော့ POS tagging လုပ်ပေးသွားတာကို မြင်ရပါလိမ့်မယ်။  

```
(base) ye@ykt-pro:/media/ye/project1/4github/demo-of-RDR-myPOS-using/myPOS/corpus-draft-ver-1.0/model/rdr/t10$ cat ./new-test.txt.TAGGED 
ဘာ/pron နေရာ/n မှာ/ppm ခက်/adj နေ/part တာ/part လဲ/part ။/punc
ကြိုးစား/v ပါ/part အဆင်ပြေ/v ရ/part မယ်/ppm
```

**တစ်ခုတော့ ရှိပါတယ်။ ကိုယ်က POS tagging လုပ်ချင်တဲ့ စာကြောင်းတွေကိုတော့ word segmentation ကြိုဖြတ်ပေးထားရပါလိမ့်မယ်။  

