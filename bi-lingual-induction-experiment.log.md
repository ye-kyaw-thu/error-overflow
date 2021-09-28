# Bi-lingual Induction Experiment Log

အရင်ဆုံး ဒေတာ ပြင်ဆင်ခဲ့...  

corpus အတွက်က ASEAN-MT ဒေတာရယ် (en, th, my), TALPCo ဒေတာရယ် (en, th, my), BEST thai corpus ရယ်, myword+para (for my),

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ cp data_eng.txt ../../exp1/en/  
```

```
(base) ye@:/media/ye/SP PHD U3/test-myWord/myWord-main$ python ./myword.py word /home/ye/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus/data_myn.txt /home/ye/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus/data_myn.word.txt
```

ဒါပေမဲ့ myWord နဲ့ ဖြတ်တဲ့ output ထက် manual ဖြတ်ထားပြီးသား ရှိတာမို့ အဲဒါကိုပဲ ယူသုံးဖို့ ဆုံးဖြတ်ခဲ့...  

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ wget https://raw.githubusercontent.com/matbahasa/TALPCo/master/myn/data_myn-token.txt 
--2021-09-26 04:13:59--  https://raw.githubusercontent.com/matbahasa/TALPCo/master/myn/data_myn-token.txt
Resolving raw.githubusercontent.com (raw.githubusercontent.com)... 185.199.111.133, 185.199.110.133, 185.199.109.133, ...
Connecting to raw.githubusercontent.com (raw.githubusercontent.com)|185.199.111.133|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 188242 (184K) [text/plain]
Saving to: ‘data_myn-token.txt’

data_myn-token.txt                    100%[=========================================================================>] 183.83K  --.-KB/s    in 0.1s    

2021-09-26 04:13:59 (1.51 MB/s) - ‘data_myn-token.txt’ saved [188242/188242]

(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head data_myn-token.txt 
1176
မစ္စတာ
တာနာခါ
ဟာ
ကျောင်းသား
မ
ဟုတ်
ပါ
ဘူး
။
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ 
```

column to line conversion:  

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ perl ./col2line.pl ./data_myn-token.txt > ./data_myn-token.txt.line
```

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head ./data_myn-token.txt.line 
1176 မစ္စတာ တာနာခါ ဟာ ကျောင်းသား မ ဟုတ် ပါ ဘူး ။
1178 အဖေ က ကျောင်းဆရာ ပါ ။
1180 ကျောင်း ပိတ် တယ် ။
1194 တိုကျို မှာ နေ သာ တယ် ။
1222 ပန်းခြံ မှာ သစ်ပင် တွေ ရှိ တယ် ။
1229 မစ္စတာ တာနာခါ ဘယ် မှာ ရှိ သ လဲ ။
1233 ပိုက်ဆံ မ ရှိ ဘူး ။
1244 စာရေးခုံ ပေါ် မှာ စာအုပ် ရှိ တယ် ။
1245 စာရေးခုံ အောက် မှာ လွယ်အိတ် ရှိ တယ် ။
1246 အိတ် ထဲ မှာ မှတ်စုစာအုပ် ရှိ တယ် ။
```

Remove line no:  

```
$ sed 's/^ *[0-9]\+.//g' ./data_myn-token.txt.line > ./data_myn-token.txt.line.rm-lineno 
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head ./data_myn-token.txt.line.rm-lineno 
မစ္စတာ တာနာခါ ဟာ ကျောင်းသား မ ဟုတ် ပါ ဘူး ။
အဖေ က ကျောင်းဆရာ ပါ ။
ကျောင်း ပိတ် တယ် ။
တိုကျို မှာ နေ သာ တယ် ။
ပန်းခြံ မှာ သစ်ပင် တွေ ရှိ တယ် ။
မစ္စတာ တာနာခါ ဘယ် မှာ ရှိ သ လဲ ။
ပိုက်ဆံ မ ရှိ ဘူး ။
စာရေးခုံ ပေါ် မှာ စာအုပ် ရှိ တယ် ။
စာရေးခုံ အောက် မှာ လွယ်အိတ် ရှိ တယ် ။
အိတ် ထဲ မှာ မှတ်စုစာအုပ် ရှိ တယ် ။
```

စာလုံးဖြတ်ပြီး ကော်လံအလိုက်ဖြစ်နေတဲ့ ထိုင်း ဖိုင်ကိုလည်း ပုံမှန် left-to-right line တွေအဖြစ် အောက်ပါအတိုင်း ပြောင်းခဲ့...  

```
$ perl ./col2line.pl ./data_tha-token.txt > ./data_tha-token.txt.line 
$ sed 's/^ *[0-9]\+.//g' ./data_tha-token.txt.line > ./data_tha-token.txt.line.rm-lineno

(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings/th-data/TALPCo-parallel-corpus$ head ./data_tha-token.txt.line.rm-lineno 
คุณ ทานากะ ไม่ ใช่ นัก เรียน ครับ
พ่อ เป็น อาจารย์ ครับ
โรง เรียน หยุด ครับ
โตเกียว อากาศ แจ่มใส ครับ
ที่ สวน สาธารณะ มี ต้น ไม้ ครับ
คุณ ทานากะ อยู่ ที่ ไหน ครับ
ไม่ มี เงิน ครับ
บน โต๊ะ มี หนังสือ ครับ
ใต้ โต๊ะ มี กระเป๋า ครับ
ใน กระเป๋า มี สมุด โน้ต ครับ
```

## Downloading UMBC English Corpus

အင်္ဂလိပ်စာကိုလည်း ကိုယ့်စက်ထဲမှာ word2vec နဲ့ fasttext မော်ဒယ်ကို ဆောက်မယ်ဆိုရင် download လုပ်ဖို့ လိုအပ်တယ်။  

```
(base) ye@:/media/ye/project2/data/umbc-en$ wc UMBC_tokenized_full.txt 
    40599164  3337113760 18786225225 UMBC_tokenized_full.txt
```

```
(base) ye@:/media/ye/project2/data/umbc-en$ ll -h  UMBC_tokenized_full.txt 
-rwxr-xr-x 1 ye ye 18G စက်   26 14:45 UMBC_tokenized_full.txt*
```

```
(base) ye@:/media/ye/project2/data/umbc-en$ head ./UMBC_tokenized_full.txt 
Caucasian skin color on the penis can vary , with the glans being darker than the shaft of the penis , primarily due to increased surface vascularity . Scarring and inflammation can leave less pigmented areas on the penile skin which can look like skin color variation . 
If what you are noticing is new to you , it bears an exam to confirm that you do not have a skin infection causing the change . If it has always been that way for you since adolescence , then this is simply your coloration and it is normal . 
This has only happened in the last 3 weeks or so . The end of my penis ( the helmet ) is a white/blue colour . Even when I get an erection the end is still white/blue . On one side it is very rough . The rest of the head goes a normal blood filled red apart from these 2 patches either side . Also my foreskin seems to be a little tighter than usual . 
The following courses are required as the Core for concentrations with a Law , Diversity and Justice emphasis . This Core , combined with other courses through the Fairhaven concentration process and close faculty advisement , provides the basis for varied paths of study exploring the issues of law , diversity and justice in our society . 
This interdisciplinary seminar is an introduction to modern social theory . It employs critical social theories to explore social relationships and examine society from positions of race , class , gender , and sexuality , focusing specifically on the rights , responsibilities and obligations of individuals and communities . Integral to this examination are the experiences of those excluded from the Western ideals of freedom and equality that , arguably , form the basis of liberal democracy . This seminar must be taken either the first quarter or second quarter of enrollment at Fairhaven . 
Study of the American legal system and how it affects individuals and society , the structure and evolving nature of the legal system , and legal reasoning and the role of courts in government . Skill development in reading and analyzing court opinions . 
Study of American ideas of rights and liberties , what they mean in practice , competing principles and ideologies at work in the arena of constitutional rights , the history of our justice system with regard to rights and liberties and an exploration of where it is currently headed . 
Through the Concentration process and in close consultation with faculty advisors , students will add courses to the Core and Focus courses from the Fairhaven and WWU course catalogues to develop a concentration tailored to their career or graduate education goals . Faculty advisors will provide detailed information to their advisees about the courses available to them . 
`` I strongly believe that the underlying structures and philosophy of Fairhaven College , the abilities of my professors and the support they provided , coupled with my own interests and approach to learning were critical components to what made college such a positive experience for me . 
The knowledge and skills of my professors , and their manner of communicating , of questioning , and of teaching has many times served significantly as inspiration and motivation for me to learn more , to push beyond my supposed boundaries , and most importantly , to feel able to make mistakes . I feel very lucky to have attended Fairhaven College and for the education I gained from it . '' 
```

```
(base) ye@:/media/ye/project2/data/umbc-en$ tail ./UMBC_tokenized_full.txt 
Whither went Tammuz ? His destination has already been referred to as `` the bosom of the earth '' , and in the Assyrian version of the `` Descent of Ishtar '' he dwells in `` the house of darkness '' among the dead , `` where dust is their nourishment and their food mud '' , and `` the light is never seen '' -- the gloomy Babylonian Hades . In one of the Sumerian hymns , however , it is stated that Tammuz `` upon the flood was cast out '' . The reference may be to the submarine `` house of Ea '' , or the Blessed Island to which the Babylonian Noah was carried . In this Hades bloomed the nether `` garden of Adonis '' . 
`` I am Sargon , the mighty King of Akkad . My mother was a vestal ( priestess ) , my father an alien , whose brother inhabited the mountain . . . . When my mother had conceived me , she bare me in a hidden place . She laid me in a vessel of rushes , stopped the door thereof with pitch , and cast me adrift on the river . . . . The river floated me to Akki , the water drawer , who , in drawing water , drew me forth . Akki , the water drawer , educated me as his son , and made me his gardener . As a gardener , I was beloved by the goddess Ishtar . '' 
It is unlikely that this story was invented by Sargon . Like the many variants of it found in other countries , it was probably founded on a form of the Tammuz-Adonis myth . Indeed , a new myth would not have suited Sargon 's purpose so well as the adaptation of an old one , which was more likely to make popular appeal when connected with his name . The references to the goddess Ishtar , and Sargon 's early life as a gardener , suggest that the king desired to be remembered as an agricultural Patriarch , if not of divine , at any rate of semi-divine origin . 
Heimdal , watchman of the Teutonic gods , also dwelt for a time among men as `` Rig '' , and had human offspring , his son Thrall being the ancestor of the Thralls , his son Churl of churls , and Jarl of noblemen . 
I spread like a bird my hands . I descend , I descend to the house of darkness , the dwelling of the god Irkalla : To the house out of which there is no exit , To the road from which there is no return : To the house from whose entrance the light is taken , The place where dust is their nourishment and their food mud . Its chiefs also are like birds covered with feathers ; The light is never seen , in darkness they dwell . . . . 
Keeper of the waters , open thy gate , Open thy gate that I may enter . If thou openest not the gate that I may enter I will strike the door , the bolts I will shatter , p. 96 I will strike the threshold and will pass through the doors ; I will raise up the dead to devour the living , Above the living the dead shall exceed in numbers . 
Let me weep over the strong who have left their wives , Let me weep over the handmaidens who have lost the embraces of their husbands , Over the only son let me mourn , who ere his days are come is taken away . 
May I imprison thee in the great prison , May the garbage of the foundations of the city be thy food , May the drains of the city be thy drink , May the darkness of the dungeon be thy dwelling , May the stake be thy seat , May hunger and thirst strike thy offspring . 
Since thou hast not paid a ransom for thy deliverance to her ( Allatu ) , so to her again turn back , For Tammuz the husband of thy youth . The glistening waters ( of life ) pour over him . In splendid clothing dress him , with a ring of crystal adorn him . 
A Sumerian hymn to Tammuz throws light on this narrative . It sets forth that Ishtar descended to Hades to entreat him to be glad and to resume care of his flocks , but Tammuz refused or was unable to return . 
(base) ye@:/media/ye/project2/data/umbc-en$ 
```

--------------

filesize တွေက အရမ်းကြီးလို့ နောက် မော်ဒယ်တွေ ထွက်လာတဲ့ အခါမှာလည်း နေရာယူနိုင်လို့ ဖိုင်တွေကို project2/ HDD အောက်ကို ရွှေ့လိုက်တယ်။  

မြန်မာစာ corpus က အောက်ပါအတိုင်း...   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ cat corpus2-and-para 3_all.my.word data_myn-token.txt.line.rm-lineno > my_corpus.txt
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ wc my_corpus.txt 
   633956  13158666 170988793 my_corpus.txt
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my$ 
```


## Building word2vec and fasttext models

shell script ရေးခဲ့...  

```bash
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ cat ./mk-word2vec-fasttext.sh 
#!/bin/bash

# STEP No. 1: building word2vec and fasttext models
#
# written by Ye Kyaw Thu, LST, NECTEC, Thailand
# Date 25 Sept 2021
# How to run: ./mk-word2vec-fasttext.sh <source-corpus>  <src-output-folder> <target-corpus> <trg-output-folder>
# e.g. ./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/data/umbc-en/UMBC_tokenized_full.txt /media/ye/project2/exp/bilingual-induction/exp1/en/ 2>&1 | tee my-en.exp1.log
#./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/th/ 2>&1 | tee my-th.exp1.log


echo "change python environment...";
#conda activate bilingual-emb

# Building word2vec
# python3 -i src/train_embeddings.py --corpus YOUR-CORPUS --model YOUR-MODEL --output-directory YOUR-OUTPUT-DIR

# for source
echo "start building a word2vec model for SRC language ...  ";
#time python3 src/train_embeddings.py --corpus $1 --model word2vec --output-directory $2

# for target
echo "start building a word2vec model for TRG language ...  ";
time python3 src/train_embeddings.py --corpus $3 --model word2vec --output-directory $4
 
 # Building fasttext
echo "building a fasttext model for SRC language..."
#time python3 src/train_embeddings.py --corpus $1 --model fasttext --output-directory $2;

echo "building a fasttext model for TRG language..."
time python3 src/train_embeddings.py --corpus $3 --model fasttext --output-directory $4;

echo "check for SRC:  see word2vec and fastext models...";
 ls $2;
echo "check for TRG:  see word2vec and fastext models...";
 ls $4;


(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

Run above shell script...  

```
(bilingual-emb)  ye@~/tool/en-cy-bilingual-embeddings$ ./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/data/umbc-en/UMBC_tokenized_full.txt /media/ye/project2/exp/bilingual-induction/exp1/en/
...
...
...
2021-09-26 15:58:31,102 : INFO : PROGRESS: at sentence #10570000, processed 50822549 words, keeping 39505036 word types
2021-09-26 15:58:31,445 : INFO : PROGRESS: at sentence #10580000, processed 50866439 words, keeping 39538482 word types
2021-09-26 15:58:31,928 : INFO : PROGRESS: at sentence #10590000, processed 50910957 words, keeping 39572544 word types
2021-09-26 15:58:32,726 : INFO : PROGRESS: at sentence #10600000, processed 50954727 words, keeping 39606533 word types
./mk-word2vec-fasttext.sh: line 23: 172990 Killed                  python3 src/train_embeddings.py --corpus $3 --model word2vec --output-directory $4

real	6m7.060s
user	4m42.179s
sys	0m15.686s
building a fasttext model for SRC language...
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt
2021-09-26 15:59:52,598 : INFO : resetting layer weights
./mk-word2vec-fasttext.sh: line 27: 173138 Killed                  python3 src/train_embeddings.py --corpus $1 --model fasttext --output-directory $2

real	0m12.280s
user	0m4.140s
sys	0m8.344s
building a fasttext model for TRG language...
Loading corpus: /media/ye/project2/data/umbc-en/UMBC_tokenized_full.txt
2021-09-26 16:00:04,857 : INFO : resetting layer weights
./mk-word2vec-fasttext.sh: line 30: 173169 Killed                  python3 src/train_embeddings.py --corpus $3 --model fasttext --output-directory $4

real	0m6.203s
user	0m4.110s
sys	0m2.202s
check for SRC:  see word2vec and fastext models...
 3_all.my.word	 corpus2-and-para   data_myn-token.txt.line.rm-lineno   my_corpus.txt  'my_corpus.txt_model=word2vec_vectors.vec'
check for TRG:  see word2vec and fastext models...
1_all.en.word  data_eng.txt
```

အထက်မှာ မြင်ရတဲ့အတိုင်းပဲ memory မနိုင်တာကြောင့်လား?! killed ဖြစ်ကုန်တယ်။
မြန်မာစာအတွက် word2vec model တော့ ဆောက်တာ ပြီးသွားတယ်။
အင်္ဂလိပ်စာအတွက် word2vec မဆောက်နိုင်ခဲ့...
ပြီးတော့ မြန်မာစာအတွက် fasttext မဆောက်နိုင်ခဲ့...
ပြီးတော့ အင်္ဂလိပ်စာအတွက် fasttext မော်ဒယ်လည်း မဆောက်နိုင်ခဲ့တာကို တွေ့ရ...  

coding ကို စစ်ရင်းနဲ့ အောက်ပါ စာကြောင်းကို ပြင်ရမယ်ဆိုတာလည်း သွားတွေ့...  

	corpus = data_manager.ExampleCorpus(args.corpus, sep=', ')
	
sep=' ' ဖြစ်ရမယ် မြန်မာစာအတွက်လည်း...  

## Trying with Thai

အင်္ဂလိပ်စာ ဒေတာ က text တင်ပဲ 17GB ယူတော့ လုပ်မယ်ဆိုရင် ဆောက်ပြီးသား word2vec ကိုပဲ သုံးလိုက်တော့မယ်..  
ထိုင်း corpus ဒေတာနဲ့ run ကြည့်ခဲ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./mk-word2vec-fasttext.sh /media/ye/project2/exp/bilingual-induction/exp1/my/my_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt /media/ye/project2/exp/bilingual-induction/exp1/th/ 2>&1 | tee my-th.exp1.log
...
...
...
2021-09-26 22:19:25,736 : INFO : EPOCH 10 - PROGRESS: at 40.37% examples, 333182 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:26,748 : INFO : EPOCH 10 - PROGRESS: at 46.76% examples, 332569 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:27,772 : INFO : EPOCH 10 - PROGRESS: at 51.86% examples, 331631 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:28,784 : INFO : EPOCH 10 - PROGRESS: at 56.06% examples, 330183 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:29,788 : INFO : EPOCH 10 - PROGRESS: at 63.62% examples, 333872 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:30,796 : INFO : EPOCH 10 - PROGRESS: at 74.36% examples, 340404 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:31,798 : INFO : EPOCH 10 - PROGRESS: at 83.27% examples, 345196 words/s, in_qsize 5, out_qsize 0
2021-09-26 22:19:32,445 : INFO : worker thread finished; awaiting finish of 2 more threads
2021-09-26 22:19:32,457 : INFO : worker thread finished; awaiting finish of 1 more threads
2021-09-26 22:19:32,467 : INFO : worker thread finished; awaiting finish of 0 more threads
2021-09-26 22:19:32,467 : INFO : EPOCH - 10 : training on 5230564 raw words (4125830 effective words) took 11.8s, 349305 effective words/s
2021-09-26 22:19:32,467 : INFO : training on a 52305640 raw words (41259675 effective words) took 119.1s, 346492 effective words/s
2021-09-26 22:19:33,229 : INFO : storing 28721x300 projection weights into /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=fasttext_vectors.vec
Loading corpus: /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt
Embeddings saved to /media/ye/project2/exp/bilingual-induction/exp1/th/th_corpus.txt_model=fasttext_vectors.vec

real	2m28.727s
user	7m12.536s
sys	0m5.877s
check for SRC:  see word2vec and fastext models...
3_all.my.word
corpus2-and-para
corpus2-and-para_model=fasttext_vectors.vec
data_myn-token.txt.line.rm-lineno
my_corpus.txt
my_corpus.txt_model=word2vec_vectors.vec
check for TRG:  see word2vec and fastext models...
2_all.th.word
best.clean.corpus
data_tha-token.txt.line.rm-lineno
th_corpus.txt
th_corpus.txt_model=fasttext_vectors.vec
th_corpus.txt_model=word2vec_vectors.vec
```

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/th$ ll -h *
-rwxr-xr-x 1 ye ye 2.1M စက်   26 03:33  2_all.th.word*
-rwxr-xr-x 1 ye ye  62M စက်   26 03:31  best.clean.corpus*
-rwxr-xr-x 1 ye ye 130K စက်   26 04:36  data_tha-token.txt.line.rm-lineno*
-rwxr-xr-x 1 ye ye  64M စက်   26 21:23  th_corpus.txt*
-rwxr-xr-x 1 ye ye  95M စက်   26 22:19 'th_corpus.txt_model=fasttext_vectors.vec'*
-rwxr-xr-x 1 ye ye  99M စက်   26 22:17 'th_corpus.txt_model=word2vec_vectors.vec'*
```

## Do next Step for my-th

မြန်မာ-ထိုင်း run ဖို့ဆိုရင် dictionary လည်း လိုအပ်တယ်။  
အဲဒါကြောင့် အရင်ဆုံး အင်္ဂလိပ်-ထိုင်း အဘိဓာန်ကနေ အင်္ဂလိပ်စာလုံးတွေကိုပဲ ဖြတ်ထုတ်လိုက်ပြီးတော့ google translate နဲ့ manual ဘာသာပြန်ခိုင်းခဲ့...  
copy/paste English --> google translate into Myanmar ---> copy/paste အလုပ်ကို တရက် လောက် လုပ်လိုက်ရ...   
ပြီးသွားတဲ့အခါမှာ English-Myanmar dictionary ရလာခဲ့...   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ paste ./en-th.dict.f1 ./en2my.google.txt > en-my.raw1
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ wc en-my.raw1
 125530  326180 5231117 en-my.raw1
```

တစ်ခုရှိတာက အဲဒီအထဲမှာ အင်္ဂလိပ်စာလုံးတွေကို ဘာသာပြန်မပေးနိုင်လို့ input ထည့်လိုက်တဲ့ အင်္ဂလိပ်စာလုံးအတိုင်းပဲ ထွက်လာတာတွေလည်း ရှိလို့  
အဲဒီလို ဖြစ်နေတဲ့ pair တွေကို အောက်ပါအတိုင်း awk နဲ့ remove လုပ်လို့ရတယ်...    

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ awk '$1 == $2 { next } { print }' ./test.txt 
abstinent	ထင်ရှားသော
aka	(ခေါ်)
halt	ရပ်နား
halt	ရပ်နား
ham	ဝက်ပေါင်ခြောက်
ham	ဝက်ပေါင်ခြောက်
handwrite	လက်ရေး
handwriting	လက်ရေး
handwritten	လက်ရေး
anesthesiologist	မေ့ဆေးဆရာဝန်
haughtily	မာနကြီး
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$
```

နောက်တစ်ခုက uniq လုပ်ဖို့လည်း လိုအပ်တယ်။  
shell script အဖြစ် ရေးခဲ့...  

```bash
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ cat rm-same-column-and-uniq.sh 
#!/bin/bash

# written by Ye, LST, NECTEC, Thailand
# removing if column1 and column2 are the same. make a uniq file.
# Date: 27 Sept 2021
# How to run: ./rm-same-column-and-uniq.sh <input-file>


inputFile=$1;

awk '$1 == $2 { next } { print }' $inputFile > tmp.out
sort ./tmp.out | uniq > $inputFile.clean

rm tmp.out;
#cat $inputFile.clean
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$
```

test file as follows:   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ cat ./test.txt
Aberdeen	Aberdeen
abstinent	ထင်ရှားသော
AJAX	AJAX
aka	(ခေါ်)
halt	ရပ်နား
halt	ရပ်နား
ham	ဝက်ပေါင်ခြောက်
ham	ဝက်ပေါင်ခြောက်
handwrite	လက်ရေး
handwriting	လက်ရေး
handwritten	လက်ရေး
anagram	anagram
anchovy	anchovy
anesthesiologist	မေ့ဆေးဆရာဝန်
haughtily	မာနကြီး
```

test run...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ ./rm-same-column-and-uniq.sh ./test.txt
abstinent	ထင်ရှားသော
aka	(ခေါ်)
anesthesiologist	မေ့ဆေးဆရာဝန်
halt	ရပ်နား
ham	ဝက်ပေါင်ခြောက်
handwrite	လက်ရေး
handwriting	လက်ရေး
handwritten	လက်ရေး
haughtily	မာနကြီး
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$
```

running for the en-my dictionary:   

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ time ./rm-same-column-and-uniq.sh ./en-my.raw1

real	0m0.221s
user	0m0.208s
sys	0m0.025s
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ wc ./en-my.raw1
 125530  326180 5231117 ./en-my.raw1
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ wc ./en-my.raw1.clean 
  57326  173067 2977748 ./en-my.raw1.clean
```

## Prepare my-th dictionary

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ paste ./en2my.google.txt ./en-th.dict.f2 > ./my-th.raw1
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ head ./my-th.raw1 
cheese အကြီးကြီး	เป็นสำนวนแปลว่า คนที่สำคัญมาก
cart la carte	|มีที่มาจากภาษาฝรั่งเศส| การสั่งอาหารที่มีอยู่ในเมนูได้ตามใจชอบ โดยไม่ต้องสั่งเป็นชุดตามที่ร้านอาหารจัดไว้ (ทางประเทศแถบตะวันตก มักมีรายการอาหารเป็นชุดจัดไว้ให้), เมนูหรือรายการอาหารที่มีราคาแยกเฉพาะสำหรับอาหารแต่ละจาน
a la carte ပါ	ดู à la carte (ภาษาฝรั่งเศส), Related: S. à la carte , 
ဝန်တစ်ခု	มาก, มากมาย เช่น a load of rubbish, What a load of muggles.
(တစ်ယောက်) ရဲ့စိတ်တစ်ပိုင်း	คำวิจารณ์หรือตำหนิอย่างตรงไปตรงมาและรุนแรง, เช่น She gave him a piece of her mind. เธอตำหนิเขาตรงๆ อย่างรุนแรง
aardwolf	สัตว์เลี้ยงลูกด้วยนม ออกหากินเวลากลางคืน อาศัยอยู่ในที่ราบตอนใต้ของแอฟริกา กินปลวกและแมลงตัวอ่อนเป็นอาหาร เป็นสัตว์ตระกูลเดียวกับไฮยีน่า
စွန့်လွှတ်ဧကရာဇ်	จักรพรรดิ์ผู้ที่สละราชสมบัติ
Aberdeen	เมืองท่าในตะวันออกเฉียงเหนือของสก็อตแลนด์
ထင်ရှားသော	ที่ค่อยๆกินอย่างไม่มูมมาม, ที่สามารถระงับอารมณ์หรือความอยากได้ดี เช่น the longer the intake, the greater the likelihood that a patient will stay continuously abstinent even after termination of alcohol deterrents.
accordian တံခါး	บานเฟี๊ยม เช่น  The accordion door is pleated with many vertical folds and supported by rollers inserted in a track mounted at the top., Related: S.accordion door 
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ tail ./my-th.raw1 
zootomy	กายวิภาคศาสตร์ที่เกี่ยวกับสัตว์
Zoroaster	ผู้สอนศาสนาชาวเปอร์เซีย
Zoroastrianism	หลักความเชื่อของ Zoroaster
zoster	โรคงูสวัด
ဇူ	เผ่าซูลูในแอฟริกา
ဇူး	เมืองซูริคในประเทศสวิตเซอร์แลนด์
zwitterion	ไอออนซึ่งมีประจุบวกและลบ
zygote	เซลล์ที่เกิดจากการรวมกันของเซลล์เพศสองเซลล์
zygotic ဖြစ်သည်	เกี่ยวกับ zygote
zymurgy	การหมักสุรา
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/dict$ 
```

mk-bilingual-dict-train-test.sh ကို run တော့ error ပေးနေခဲ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./mk-bilingual-dict-train-test.sh /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 /media/ye/project2/exp/bilingual-induction/exp1/my/ /media/ye/project2/exp/bilingual-induction/exp1/th/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec/ 2>&1 | tee my-th.mk-bi-dict.log
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/3_all.my.word
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/corpus2-and-para
Traceback (most recent call last):
  File "/home/ye/tool/en-cy-bilingual-embeddings/src/get_vocab_from_vectors.py", line 34, in <module>
    w = line.split()[0]
IndexError: list index out of range

real	0m3.662s
user	0m0.632s
sys	0m0.033s
source_vocab.txt
target_vocab.txt
Loading source vocab
Source vocab has 0 words
---
Loading target vocab
Target vocab has 0 words
Loading dictionary - Done 1000 of 125516
Loading dictionary - Done 2000 of 125516
Loading dictionary - Done 3000 of 125516
Loading dictionary - Done 4000 of 125516
...
...
...
Loading dictionary - Done 118000 of 125516
Loading dictionary - Done 119000 of 125516
Loading dictionary - Done 120000 of 125516
Loading dictionary - Done 121000 of 125516
Loading dictionary - Done 122000 of 125516
Loading dictionary - Done 123000 of 125516
Loading dictionary - Done 124000 of 125516
Loading dictionary - Done 125000 of 125516
Loaded 0 entries from the original dictionary, which had: 125516
Traceback (most recent call last):
  File "/home/ye/tool/en-cy-bilingual-embeddings/src/split-dictionary.py", line 54, in <module>
    fdf.columns = ['english', 'welsh']
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/generic.py", line 5500, in __setattr__
    return object.__setattr__(self, name, value)
  File "pandas/_libs/properties.pyx", line 70, in pandas._libs.properties.AxisProperty.__set__
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/generic.py", line 766, in _set_axis
    self._mgr.set_axis(axis, labels)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/internals/managers.py", line 216, in set_axis
    self._validate_set_axis(axis, new_labels)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/pandas/core/internals/base.py", line 57, in _validate_set_axis
    raise ValueError(
ValueError: Length mismatch: Expected axis has 0 elements, new values have 2 elements
>>> exit()

real	0m23.072s
user	0m0.832s
sys	0m1.036s
source_vocab.txt
target_vocab.txt
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

အောက်ပါ အတွဲကြောင့်လား?!  

```
zing	้เกิดเสียงดังหวือผ่านไป
```
(vi နဲ့ စစ်ကြည့်တော့ TAB မမြင်ရ)

မဆိုင်ဘူး ပြဿနာက .... mk-bilingual-dict-train-test.sh shell script မှာ note မှတ်ထားခဲ့တဲ့အတိုင်းပါပဲ...   

```
# How to run: ./mk-bilingual-dict-train-test.sh <dictionary> <folder-with-SRC-embeddings> <folder-with-TRG-embeddings> <output-folder-name>
# ./mk-bilingual-dict-train-test.sh /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/ 2>&1 | tee my-th.mk-bi-dict.log
# သတိထားရမှာက $2, $3 argument တွေကို ပေးတဲ့အခါမှာ folder name ပေးရမယ်။ ပြီးတော့ အဲဒီ folder အောက်မှာက word2vec ဆိုရင်လည်း word2vec ဖိုင်ပဲ ရှိသင့်တယ်။
# ထိုနည်းလည်းကောင်း fastext နဲ့ bi-lingual induction experiment လုပ်တာဆိုရင်လည်း fasttext model ဖိုင်ပဲ ရှိသင့်တယ်။ ပေးလိုက်တဲ့ folder path အောက်မှာ တခြားဖိုင်တွေရှိနေရင် error ပေးလိမ့်မယ်
```

ဒီတစ်ခေါက် word2vec folder အောက်မှာ word2vec ဖိုင် တစ်ဖိုင်ပဲ ထားပြီး run တော့ အောက်ပါအတိုင်း OK သွားခဲ့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./mk-bilingual-dict-train-test.sh /media/ye/project2/exp/bilingual-induction/exp1/dict/my-th.raw1 /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/ 2>&1 | tee my-th.mk-bi-dict.log
Processing /media/ye/project2/exp/bilingual-induction/exp1/my/word2vec/my_corpus.txt_model=word2vec_vectors.vec
Processing /media/ye/project2/exp/bilingual-induction/exp1/th/word2vec/th_corpus.txt_model=word2vec_vectors.vec
Source vocab is 56038 tokens
Target vocab is 28721 tokens

real	0m3.034s
user	0m1.849s
sys	0m0.161s
source_vocab.txt
target_vocab.txt
Loading source vocab
Source vocab has 56038 words
---
Loading target vocab
Target vocab has 28721 words
Loading dictionary - Done 1000 of 125516
Loading dictionary - Done 2000 of 125516
Loading dictionary - Done 3000 of 125516
Loading dictionary - Done 4000 of 125516
Loading dictionary - Done 5000 of 125516
Loading dictionary - Done 6000 of 125516
Loading dictionary - Done 7000 of 125516
Loading dictionary - Done 8000 of 125516
Loading dictionary - Done 9000 of 125516
Loading dictionary - Done 10000 of 125516
Loading dictionary - Done 11000 of 125516
Loading dictionary - Done 12000 of 125516
Loading dictionary - Done 13000 of 125516
Loading dictionary - Done 14000 of 125516
Loading dictionary - Done 15000 of 125516
Loading dictionary - Done 16000 of 125516
Loading dictionary - Done 17000 of 125516
Loading dictionary - Done 18000 of 125516
Loading dictionary - Done 19000 of 125516
Loading dictionary - Done 20000 of 125516
Loading dictionary - Done 21000 of 125516
Loading dictionary - Done 22000 of 125516
Loading dictionary - Done 23000 of 125516
Loading dictionary - Done 24000 of 125516
Loading dictionary - Done 25000 of 125516
Loading dictionary - Done 26000 of 125516
Loading dictionary - Done 27000 of 125516
Loading dictionary - Done 28000 of 125516
Loading dictionary - Done 29000 of 125516
Loading dictionary - Done 30000 of 125516
Loading dictionary - Done 31000 of 125516
Loading dictionary - Done 32000 of 125516
Loading dictionary - Done 33000 of 125516
Loading dictionary - Done 34000 of 125516
Loading dictionary - Done 35000 of 125516
Loading dictionary - Done 36000 of 125516
Loading dictionary - Done 37000 of 125516
Loading dictionary - Done 38000 of 125516
Loading dictionary - Done 39000 of 125516
Loading dictionary - Done 40000 of 125516
Loading dictionary - Done 41000 of 125516
Loading dictionary - Done 42000 of 125516
Loading dictionary - Done 43000 of 125516
Loading dictionary - Done 44000 of 125516
Loading dictionary - Done 45000 of 125516
Loading dictionary - Done 46000 of 125516
Loading dictionary - Done 47000 of 125516
Loading dictionary - Done 48000 of 125516
Loading dictionary - Done 49000 of 125516
Loading dictionary - Done 50000 of 125516
Loading dictionary - Done 51000 of 125516
Loading dictionary - Done 52000 of 125516
Loading dictionary - Done 53000 of 125516
Loading dictionary - Done 54000 of 125516
Loading dictionary - Done 55000 of 125516
Loading dictionary - Done 56000 of 125516
Loading dictionary - Done 57000 of 125516
Loading dictionary - Done 58000 of 125516
Loading dictionary - Done 59000 of 125516
Loading dictionary - Done 60000 of 125516
Loading dictionary - Done 61000 of 125516
Loading dictionary - Done 62000 of 125516
Loading dictionary - Done 63000 of 125516
Loading dictionary - Done 64000 of 125516
Loading dictionary - Done 65000 of 125516
Loading dictionary - Done 66000 of 125516
Loading dictionary - Done 67000 of 125516
Loading dictionary - Done 68000 of 125516
Loading dictionary - Done 69000 of 125516
Loading dictionary - Done 70000 of 125516
Loading dictionary - Done 71000 of 125516
Loading dictionary - Done 72000 of 125516
Loading dictionary - Done 73000 of 125516
Loading dictionary - Done 74000 of 125516
Loading dictionary - Done 75000 of 125516
Loading dictionary - Done 76000 of 125516
Loading dictionary - Done 77000 of 125516
Loading dictionary - Done 78000 of 125516
Loading dictionary - Done 79000 of 125516
Loading dictionary - Done 80000 of 125516
Loading dictionary - Done 81000 of 125516
Loading dictionary - Done 82000 of 125516
Loading dictionary - Done 83000 of 125516
Loading dictionary - Done 84000 of 125516
Loading dictionary - Done 85000 of 125516
Loading dictionary - Done 86000 of 125516
Loading dictionary - Done 87000 of 125516
Loading dictionary - Done 88000 of 125516
Loading dictionary - Done 89000 of 125516
Loading dictionary - Done 90000 of 125516
Loading dictionary - Done 91000 of 125516
Loading dictionary - Done 92000 of 125516
Loading dictionary - Done 93000 of 125516
Loading dictionary - Done 94000 of 125516
Loading dictionary - Done 95000 of 125516
Loading dictionary - Done 96000 of 125516
Loading dictionary - Done 97000 of 125516
Loading dictionary - Done 98000 of 125516
Loading dictionary - Done 99000 of 125516
Loading dictionary - Done 100000 of 125516
Loading dictionary - Done 101000 of 125516
Loading dictionary - Done 102000 of 125516
Loading dictionary - Done 103000 of 125516
Loading dictionary - Done 104000 of 125516
Loading dictionary - Done 105000 of 125516
Loading dictionary - Done 106000 of 125516
Loading dictionary - Done 107000 of 125516
Loading dictionary - Done 108000 of 125516
Loading dictionary - Done 109000 of 125516
Loading dictionary - Done 110000 of 125516
Loading dictionary - Done 111000 of 125516
Loading dictionary - Done 112000 of 125516
Loading dictionary - Done 113000 of 125516
Loading dictionary - Done 114000 of 125516
Loading dictionary - Done 115000 of 125516
Loading dictionary - Done 116000 of 125516
Loading dictionary - Done 117000 of 125516
Loading dictionary - Done 118000 of 125516
Loading dictionary - Done 119000 of 125516
Loading dictionary - Done 120000 of 125516
Loading dictionary - Done 121000 of 125516
Loading dictionary - Done 122000 of 125516
Loading dictionary - Done 123000 of 125516
Loading dictionary - Done 124000 of 125516
Loading dictionary - Done 125000 of 125516
Loaded 14801 entries from the original dictionary, which had: 125516
>>> 

```

အထက်ပါအတိုင်းဖြစ်နေရင် exit() နဲ့ ထွက်လိုက်ပါ။  


```
>>> exit()

real	4m29.994s
user	0m0.861s
sys	0m1.075s
source_vocab.txt
target_vocab.txt
test_dict.csv
train_dict.csv
```

check the output folder:  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ ls
source_vocab.txt  target_vocab.txt  test_dict.csv  train_dict.csv
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ wc *
  56038   56038 1335612 source_vocab.txt
  28721   28721  648843 target_vocab.txt
   2360    4720   97988 test_dict.csv
   9436   18872  390844 train_dict.csv
  96555  108351 2473287 total
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ 
```

ဖိုင်အထဲက စာကြောင်းတွေကိုလည်း head command နဲ့ ဝင်ကြည့်ခဲ့...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$ head *
==> source_vocab.txt <==
🤠
ရှာလင်ဘတ်
ပေါ်လွင်
ကာဗွန်ဒိုင်အောက်ဆိုက်
မိုင်းယော
အိစ်
စလင်းကွင်း
အဖြူ
သက်ဆိုး
ဆီးကြို

==> target_vocab.txt <==
คากัน
เออร์วิ่ง
ไพรกว้าง
กรมทพ
เซนต์ปีเตอร์
ภายใต้
ธัช
อพยุหะคีรี
เซอร์เบีย
นายกล้านรงค์

==> test_dict.csv <==
english welsh
သဘာဝ ธาตุแท้
ထုပ်ပိုး ห่อหุ้ม
နေ့လည် เที่ยง
ကျော့ကွင်း กับดัก
တောင်ပို့ โคก
ပတ္တာ บานพับ
တိုင်းပြည် ภูมิลำเนา
ဖိနပ် เกือก
မြောက်ဘက် อุดร

==> train_dict.csv <==
english welsh
အလှဆင် ประดับ
ယဲ့ယဲ့ แบบบาง
ပီကင်း กรุงปักกิ่ง
ပို့စ် แจ้ง
သံသယ พิรุธ
ကြည့် สีหน้า
ဝါး เคี้ยว
ဝမ်းနည်း โศกสลด
ရှေးခေတ် โบราณกาล
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output$
```

## Study on VecMap Tool

GitHub Link: [https://github.com/artetxem/vecmap](https://github.com/artetxem/vecmap)  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ python ./vecmap/map_embeddings.py --help
usage: map_embeddings.py [-h] [--encoding ENCODING] [--precision {fp16,fp32,fp64}] [--cuda] [--batch_size BATCH_SIZE] [--seed SEED]
                         [--supervised DICTIONARY | --semi_supervised DICTIONARY | --identical | --unsupervised | --acl2018 | --aaai2018 DICTIONARY | --acl2017 | --acl2017_seed DICTIONARY | --emnlp2016 DICTIONARY]
                         [-d DICTIONARY | --init_identical | --init_numerals | --init_unsupervised] [--unsupervised_vocab UNSUPERVISED_VOCAB]
                         [--normalize [{unit,center,unitdim,centeremb,none} ...]] [--whiten] [--src_reweight [SRC_REWEIGHT]]
                         [--trg_reweight [TRG_REWEIGHT]] [--src_dewhiten {src,trg}] [--trg_dewhiten {src,trg}] [--dim_reduction DIM_REDUCTION]
                         [-c | -u] [--self_learning] [--vocabulary_cutoff VOCABULARY_CUTOFF] [--direction {forward,backward,union}]
                         [--csls [NEIGHBORHOOD_SIZE]] [--threshold THRESHOLD] [--validation DICTIONARY] [--stochastic_initial STOCHASTIC_INITIAL]
                         [--stochastic_multiplier STOCHASTIC_MULTIPLIER] [--stochastic_interval STOCHASTIC_INTERVAL] [--log LOG] [-v]
                         src_input trg_input src_output trg_output

Map word embeddings in two languages into a shared space

positional arguments:
  src_input             the input source embeddings
  trg_input             the input target embeddings
  src_output            the output source embeddings
  trg_output            the output target embeddings

optional arguments:
  -h, --help            show this help message and exit
  --encoding ENCODING   the character encoding for input/output (defaults to utf-8)
  --precision {fp16,fp32,fp64}
                        the floating-point precision (defaults to fp32)
  --cuda                use cuda (requires cupy)
  --batch_size BATCH_SIZE
                        batch size (defaults to 10000); does not affect results, larger is usually faster but uses more memory
  --seed SEED           the random seed (defaults to 0)

recommended settings:
  Recommended settings for different scenarios

  --supervised DICTIONARY
                        recommended if you have a large training dictionary
  --semi_supervised DICTIONARY
                        recommended if you have a small seed dictionary
  --identical           recommended if you have no seed dictionary but can rely on identical words
  --unsupervised        recommended if you have no seed dictionary and do not want to rely on identical words
  --acl2018             reproduce our ACL 2018 system
  --aaai2018 DICTIONARY
                        reproduce our AAAI 2018 system
  --acl2017             reproduce our ACL 2017 system with numeral initialization
  --acl2017_seed DICTIONARY
                        reproduce our ACL 2017 system with a seed dictionary
  --emnlp2016 DICTIONARY
                        reproduce our EMNLP 2016 system

advanced initialization arguments:
  Advanced initialization arguments

  -d DICTIONARY, --init_dictionary DICTIONARY
                        the training dictionary file (defaults to stdin)
  --init_identical      use identical words as the seed dictionary
  --init_numerals       use latin numerals (i.e. words matching [0-9]+) as the seed dictionary
  --init_unsupervised   use unsupervised initialization
  --unsupervised_vocab UNSUPERVISED_VOCAB
                        restrict the vocabulary to the top k entries for unsupervised initialization

advanced mapping arguments:
  Advanced embedding mapping arguments

  --normalize [{unit,center,unitdim,centeremb,none} ...]
                        the normalization actions to perform in order
  --whiten              whiten the embeddings
  --src_reweight [SRC_REWEIGHT]
                        re-weight the source language embeddings
  --trg_reweight [TRG_REWEIGHT]
                        re-weight the target language embeddings
  --src_dewhiten {src,trg}
                        de-whiten the source language embeddings
  --trg_dewhiten {src,trg}
                        de-whiten the target language embeddings
  --dim_reduction DIM_REDUCTION
                        apply dimensionality reduction
  -c, --orthogonal      use orthogonal constrained mapping
  -u, --unconstrained   use unconstrained mapping

advanced self-learning arguments:
  Advanced arguments for self-learning

  --self_learning       enable self-learning
  --vocabulary_cutoff VOCABULARY_CUTOFF
                        restrict the vocabulary to the top k entries
  --direction {forward,backward,union}
                        the direction for dictionary induction (defaults to union)
  --csls [NEIGHBORHOOD_SIZE]
                        use CSLS for dictionary induction
  --threshold THRESHOLD
                        the convergence threshold (defaults to 0.000001)
  --validation DICTIONARY
                        a dictionary file for validation at each iteration
  --stochastic_initial STOCHASTIC_INITIAL
                        initial keep probability stochastic dictionary induction (defaults to 0.1)
  --stochastic_multiplier STOCHASTIC_MULTIPLIER
                        stochastic dictionary induction multiplier (defaults to 2.0)
  --stochastic_interval STOCHASTIC_INTERVAL
                        stochastic dictionary induction interval (defaults to 50)
  --log LOG             write to a log file in tsv format at each iteration
  -v, --verbose         write log information to stderr at each iteration
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ 
```

## Install CuPy Before Running VeccMap

GPU သုံးမယ်ဆိုရင် လိုအပ်လို့ လက်ရှိ environment မှာ မရှိသေးလို့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ pip install cupy
Collecting cupy
  Downloading cupy-9.4.0.tar.gz (1.7 MB)
     |████████████████████████████████| 1.7 MB 1.8 MB/s 
Requirement already satisfied: numpy<1.24,>=1.17 in /home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages (from cupy) (1.21.2)
Collecting fastrlock>=0.5
  Using cached fastrlock-0.6-cp39-cp39-manylinux1_x86_64.whl (42 kB)
Building wheels for collected packages: cupy
  Building wheel for cupy (setup.py) ... done
  Created wheel for cupy: filename=cupy-9.4.0-cp39-cp39-linux_x86_64.whl size=59578607 sha256=faf3d463d944b6061c5109e920c524d80ffc3fadf05ca3ec7d48bacdee45809f
  Stored in directory: /home/ye/.cache/pip/wheels/26/46/d7/e279499ab39f81388e4b29f0f8d335b5253aa791b68dced02e
Successfully built cupy
Installing collected packages: fastrlock, cupy
Successfully installed cupy-9.4.0 fastrlock-0.6
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ 
```

--cuda option နဲ့ run တဲ့အခါမှာ memory error ဆိုပြီးအောက်ပါအတိုင်း ERROR!   

```
Traceback (most recent call last):
  File "/home/ye/tool/en-cy-bilingual-embeddings/./vecmap/map_embeddings.py", line 422, in <module>
    main()
  File "/home/ye/tool/en-cy-bilingual-embeddings/./vecmap/map_embeddings.py", line 349, in main
    dropout(simfwd[:j-i], 1 - keep_prob).argmax(axis=1, out=trg_indices_forward[i:j])
  File "/home/ye/tool/en-cy-bilingual-embeddings/./vecmap/map_embeddings.py", line 32, in dropout
    mask = xp.random.rand(*m.shape) >= p
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_sample.py", line 44, in rand
    return random_sample(size=size, dtype=dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_sample.py", line 156, in random_sample
    return rs.random_sample(size=size, dtype=dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_generator.py", line 618, in random_sample
    out = self._random_sample_raw(size, dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/random/_generator.py", line 600, in _random_sample_raw
    out = cupy.empty(size, dtype=dtype)
  File "/home/ye/anaconda3/envs/bilingual-emb/lib/python3.9/site-packages/cupy/_creation/basic.py", line 22, in empty
    return cupy.ndarray(shape, dtype, order=order)
  File "cupy/_core/core.pyx", line 163, in cupy._core.core.ndarray.__init__
  File "cupy/cuda/memory.pyx", line 718, in cupy.cuda.memory.alloc
  File "cupy/cuda/memory.pyx", line 1395, in cupy.cuda.memory.MemoryPool.malloc
  File "cupy/cuda/memory.pyx", line 1416, in cupy.cuda.memory.MemoryPool.malloc
  File "cupy/cuda/memory.pyx", line 1096, in cupy.cuda.memory.SingleDeviceMemoryPool.malloc
  File "cupy/cuda/memory.pyx", line 1117, in cupy.cuda.memory.SingleDeviceMemoryPool._malloc
  File "cupy/cuda/memory.pyx", line 1355, in cupy.cuda.memory.SingleDeviceMemoryPool._try_malloc
cupy.cuda.memory.OutOfMemoryError: Out of memory allocating 1,600,000,000 bytes (allocated so far: 2,281,307,136 bytes).

real	0m5.425s
user	0m5.231s
sys	0m1.389s
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$
```

အဲဒါကြောင့် --cuda option ကို ဖြုတ်ပြီး run ခဲ့တယ်...  
Running time က semi ကစပြီး ကြာလိမ့်မယ်။  

## word2vec filenaming

လက်ရှိ word2vec ကို training လုပ်ထားတာက အောက်ပါ settting နဲ့  
(see train_embeddings.py python script)  

```python
	model = modelmap[args.model](size=300, window=5, min_count=3, sentences=corpus, iter=10)
```

အဲဒါကြောင့် ဆောက်ထားတဲ့ word2vec model ကို သတ်မှတ်ထားတဲ့ format အတိုင်း filename ကို ပြောင်းခဲ့...  

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super$ mv src_mapped_supervised.emb word2vec_s300_mc3_w5.vec
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super$ cd ../trg_super/
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super$ mv trg_mapped_supervised.emb word2vec_s300_mc3_w5.vec
```

## Dictionary Induction and Evaluation

ဒီ log မမှတ်ခင် ပထမဆုံး run ကြည့်တုန်းက ပေးတဲ့ error က ဖိုင်နာမည်ကို သူသတ်မှတ်ထားတဲ့အတိုင်း မပေးခဲ့လို့ဆိုတာ coding ဝင်ဖတ်ရင်း သိခဲ့ရလို့...   
ဒီတစ်ခါတော့ ဖိုင်နာမည်တွေကို \_s, \_mc, \_w နောက်မှာ parameter တွေကို ထည့်ပေးတာလုပ်ခဲ့...  

လောလောဆယ်က သူ့ default parameter တွေနဲ့ပဲ word2vec မော်ဒယ်ကို ဆောက်ခဲ့တာမို့...  

```
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ ./experiment1.sh /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/ /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/  /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
run vecmap_launcher.py ...
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec
path:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec
=== CMD ===
python3 vecmap/map_embeddings.py --supervised /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/train_dict.csv "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec"
WARNING: OOV dictionary entry (english - welsh)
run vecmap_eval_launcher.py ...

arguments:  Namespace(testdict='/media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv', source_vectors_folder='/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/', target_vectors_folder='/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/', results_folder='/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/')
envecs:  ['/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec']
welvecs:  ['/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec']
env:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
enprefix:  word2vec_s ens:  300 enmc:  3 enw:  5
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec
RETR:  nn
output result folder: /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
=== CMD ===
python3 vecmap/eval_translation.py "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec" -d /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv --retrieval nn
--------
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec
RETR:  invsoftmax
output result folder: /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
=== CMD ===
python3 vecmap/eval_translation.py "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec" -d /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv --retrieval invsoftmax
--------
EN:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec
WEL:  /media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec
RETR:  csls
output result folder: /media/ye/project2/exp/bilingual-induction/exp1/my-th/induction/
=== CMD ===
python3 vecmap/eval_translation.py "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/src_super/word2vec_s300_mc3_w5.vec_mapped.vec" "/media/ye/project2/exp/bilingual-induction/exp1/my-th/vecmap-output/trg_super/word2vec_s300_mc3_w5.vec_mapped.vec" -d /media/ye/project2/exp/bilingual-induction/exp1/my-th/word2vec-output/test_dict.csv --retrieval csls
--------
(bilingual-emb) ye@:~/tool/en-cy-bilingual-embeddings$ 
```

```
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction$ ls
'model=word2vec_s__retrieval=csls__s=300_mc=3_w=5.txt'        'model=word2vec_s__retrieval=nn__s=300_mc=3_w=5.txt'
'model=word2vec_s__retrieval=invsoftmax__s=300_mc=3_w=5.txt'
(base) ye@:/media/ye/project2/exp/bilingual-induction/exp1/my-th/induction$ cat *
Coverage: 99.94%  Accuracy:  2.50%
Coverage: 99.94%  Accuracy:  2.32%
Coverage: 99.94%  Accuracy:  2.44%
```

Running Process အစအဆုံးတော့ ရသွားပြီ။  

## To Do

- Word2Vec မော်ဒယ်ကို parameter အမျိုးမျိုး ထား model ဆောက်ပြီး evaluation လုပ်ကြည့်ရန်
- fasttext မော်ဒယ်နဲ့လည်း embedding လုပ်ပြီး induction ကို evaluation လုပ်ကြည့်ရန်
- အချိန်ရရင် VecMap mapping ကိုလည်း Supervised, Semi-Supervised, Identical နဲ့ Unsupervised အားလုံးနဲ့ experiment လုပ်ကြည့်ရန်


## Reference

https://github.com/marekrei/convertvec

Do We Really Need Fully Unsupervised Cross-Lingual Embeddings?:  
https://ie.technion.ac.il/~roiri/papers/EMNLP-Ivan-CLWE.pdf

PanLex-based bilingual lexicons for 210 language pairs (15 languages):  
https://github.com/ivulic/panlex-bli

Low Supervision, Low Corpus size, Low Similarity! Challenges in cross-lingual alignment of word embeddings:  
http://uu.diva-portal.org/smash/get/diva2:1365879/FULLTEXT01.pdf

Cross-lingual word and document embeddings:  
https://www.youtube.com/watch?v=2a-D7L8rdko

How to (Properly) Evaluate Cross-Lingual Word Embeddings:
On Strong Baselines, Comparative Analyses, and Some Misconceptions
https://aclanthology.org/P19-1070.pdf

Lost in Embedding Space: Explaining Cross-Lingual Task Performance with Eigenvalue Divergence:  
https://arxiv.org/pdf/2001.11136v1.pdf


